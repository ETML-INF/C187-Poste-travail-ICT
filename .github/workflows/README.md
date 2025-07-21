# 🛠️ GitHub Actions - Workflow MARP

Ce répertoire contient le workflow GitHub Actions utilisé pour **automatiser la génération et le déploiement des présentations MARP et des exercices PDF** sur **GitHub Pages**.

## 🌜 Description du Workflow

### 📌 Nom : `Build and Deploy All MARP Presentations`
Ce workflow :
- **Déclenche automatiquement la génération et le déploiement des fichiers** lorsqu’un fichier Markdown (`.md`) ou un fichier d'exercice (`.pdf`) est ajouté ou modifié.
- **Génère des fichiers HTML et PDF avec MARP** pour les présentations.
- **Copie les fichiers d'exercices PDF** dans un dossier dédié (`public/exercices/`).
- **Crée une page `index.html`** listant automatiquement toutes les présentations et exercices disponibles, triées de 0 à 99 et sans doublon de nom.
- **Déploie les fichiers générés sur GitHub Pages**.

---

## 🔄 **Déclencheurs du Workflow**
Le workflow s’exécute **automatiquement** lorsque :
1. Un **fichier Markdown (`.md`) est modifié ou ajouté** dans `b-UnitesEnseignement/Support/`
2. Une **image (`.jpg`, `.png`, etc.) est ajoutée** dans `b-UnitesEnseignement/Support/img/`
3. Un **exercice PDF est ajouté ou modifié** dans `b-UnitesEnseignement/Exercices/`
4. Une **Pull Request est ouverte/modifiée** avec ces fichiers

---

## ⚙️ **Explication du fichier `marp.yml`**

### 🔹 1. **Déclencheurs (`on:`)**
```yaml
on:
  push:
    paths:
      - 'b-UnitesEnseignement/Support/**/*.md'  
      - 'b-UnitesEnseignement/Support/img/**'  
      - 'b-UnitesEnseignement/Exercices/*.pdf'  
  pull_request:
    paths:
      - 'b-UnitesEnseignement/Support/**/*.md'
      - 'b-UnitesEnseignement/Support/img/**'
      - 'b-UnitesEnseignement/Exercices/*.pdf'
```
📌 **Déclenche le workflow lorsqu'un fichier correspondant est modifié dans ces répertoires.**

---

### 🔹 2. **Permissions (`permissions:`)**
```yaml
permissions:
  contents: read
  pages: write
  id-token: write
```
📌 **Autorise le workflow à :**
- Lire le contenu du repo
- Écrire sur GitHub Pages pour le déploiement

---

### 🔹 3. **Installation de MARP et Puppeteer**
```yaml
- name: Install Node.js and MARP CLI
  run: |
    npm install -g @marp-team/marp-cli
    npm install puppeteer
```
📌 **Installe MARP CLI** (outil pour générer les slides) et **Puppeteer** (nécessaire pour la génération des PDFs).

---

### 🔹 4. **Création et génération des fichiers MARP**
```bash
readarray -d '' files < <(find b-UnitesEnseignement/Support -type f -name "*.md" -print0)
# Tri numérique des fichiers pour l'index (de 0 à 99)
sorted_files=($(printf '%s\0' "${files[@]}" | sort -z -V | xargs -0 -n1))
for file in "${sorted_files[@]}"; do
  filename=$(basename "$file" .md)
  dirname=$(basename "$(dirname "$file")")
  # Si le nom du dossier et du fichier sont identiques, n'affiche qu'une fois
  if [ "$dirname" = "$filename" ]; then
    outputname="$filename"
  else
    outputname="${dirname}_${filename}"
  fi

  marp "$file" --html --allow-local-files --output "public/${outputname}.html"
  marp "$file" --pdf --allow-local-files --output "public/${outputname}.pdf"
done
```
📌 **Convertit chaque fichier `.md` en :**
- **HTML** (`.html`) pour afficher en ligne
- **PDF** (`.pdf`) pour impression ou partage
- **Noms sans doublon** : si le nom du dossier et du fichier sont identiques, seul le nom du fichier est utilisé.
- **Tri automatique** : les présentations sont listées de 0 à 99 dans l'index.

---

### 🔹 5. **Gestion des fichiers exercices**
```bash
mkdir -p public/exercices
cp b-UnitesEnseignement/Exercices/*.pdf public/exercices/ 2>/dev/null || echo "⚠️ Aucun exercice PDF copié"
```
📌 **Crée le dossier `public/exercices/` et copie les fichiers PDF dedans.**

---

### 🔹 6. **Génération dynamique de l'index HTML**
- Génère une page `index.html` avec TailwindCSS listant toutes les présentations (HTML/PDF) et exercices PDF.
- Les présentations sont triées de 0 à 99 et les noms sont propres (pas de doublon).

---

### 🔹 7. **Déploiement sur GitHub Pages**
```yaml
- name: Upload artifact for deployment
  uses: actions/upload-pages-artifact@v3
  with:
    path: public

- name: Deploy to GitHub Pages
  id: deployment
  uses: actions/deploy-pages@v4
```
📌 **Déploie automatiquement les fichiers générés sur GitHub Pages.**

---

## 🔍 **Comment vérifier que tout fonctionne ?**
### 📌 **1⃣ Vérifier le statut du workflow**
1. Aller sur **GitHub > Actions**.
2. Vérifier si l'exécution du workflow est réussie.
3. Regarder les logs pour s'assurer que `public/` contient les bons fichiers.

### 📌 **2⃣ Vérifier l'URL GitHub Pages**
1. Aller dans **Settings > Pages**.
2. Ouvrir le lien de ton site GitHub Pages et tester :
   ```
   https://ton-repo.github.io/
   ```
   et
   ```
   https://ton-repo.github.io/exercices/nom_du_fichier.pdf
   ```

### 📌 **3⃣ Debug en cas de problème**
- Vérifier **les logs GitHub Actions** (`ls -l public/`).
- Tester **l’URL directe** des fichiers.
- Vérifier que **les fichiers sont bien copiés** dans `public/exercices/`.

---

## 📝 **Résumé**
✅ **Automatisation complète** avec MARP pour générer **HTML & PDF**  
✅ **Déploiement automatique** sur **GitHub Pages**  
✅ **Indexation dynamique** des fichiers dans `index.html` (triés et sans doublon)  
✅ **Maintenance facile** grâce à GitHub Actions

---
📌 **Auteur :** AGR
📅 **Dernière mise à jour :** 21 juillet 2025
