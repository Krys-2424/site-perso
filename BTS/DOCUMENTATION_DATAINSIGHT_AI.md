# Documentation Complète - DataInsight AI

## Analyse Intelligente de Données 100% Local

---

## Table des matières

1. [Présentation du projet](#1-présentation-du-projet)
2. [Architecture technique](#2-architecture-technique)
3. [Structure du fichier HTML](#3-structure-du-fichier-html)
4. [Les variables CSS (Thèmes)](#4-les-variables-css-thèmes)
5. [Les composants visuels](#5-les-composants-visuels)
6. [Le JavaScript - Variables globales](#6-le-javascript---variables-globales)
7. [Import multi-format](#7-import-multi-format)
8. [Export et conversion](#8-export-et-conversion)
9. [Fonctionnalités détaillées](#9-fonctionnalités-détaillées)
10. [Les algorithmes de prédiction](#10-les-algorithmes-de-prédiction)
11. [La détection d'anomalies](#11-la-détection-danomalies)
12. [L'assistant IA (NLP)](#12-lassistant-ia-nlp)
13. [Guide de reproduction pas à pas](#13-guide-de-reproduction-pas-à-pas)
14. [Améliorations possibles](#14-améliorations-possibles)

---

## 1. Présentation du projet

### Objectif
DataInsight AI est une application web d'analyse de données qui fonctionne **entièrement dans le navigateur**, sans serveur backend ni API externe. Elle permet d'analyser des fichiers de données avec :

- **Import multi-format** : CSV, Excel (.xlsx, .xls), SQLite (.db, .sqlite), JSON, XML
- **Export/Conversion** : Convertir vos données vers 6 formats différents
- Statistiques descriptives automatiques
- Détection d'anomalies (3 méthodes)
- Prédictions (3 algorithmes)
- Visualisations interactives (6 types de graphiques)
- Assistant IA en langage naturel

### Formats supportés

| Format | Extensions | Import | Export |
|--------|------------|:------:|:------:|
| CSV | `.csv` | ✅ | ✅ |
| Excel | `.xlsx`, `.xls` | ✅ | ✅ |
| SQLite | `.db`, `.sqlite`, `.sqlite3` | ✅ | - |
| JSON | `.json` | ✅ | ✅ |
| XML | `.xml` | ✅ | ✅ |
| SQL | `.sql` | - | ✅ |
| HTML | `.html` | - | ✅ |

### Technologies utilisées
- **HTML5** : Structure de la page
- **CSS3** : Styles avec variables CSS pour les thèmes
- **JavaScript ES6** : Logique applicative
- **Chart.js 4.4.0** : Bibliothèque de graphiques (CDN)
- **SheetJS (xlsx) 0.18.5** : Lecture/écriture de fichiers Excel (CDN)
- **sql.js 1.8.0** : Lecture de bases de données SQLite dans le navigateur (CDN)

### Avantages
- ✅ Aucune installation requise
- ✅ Fonctionne hors ligne (après chargement initial)
- ✅ Données confidentielles (rien n'est envoyé sur internet)
- ✅ Gratuit et open source
- ✅ Conversion entre formats de données

---

## 2. Architecture technique

```
┌──────────────────────────────────────────────────────────────────┐
│                         index.html                                │
├──────────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌──────────────────────────┐ │
│  │   <style>   │  │   <body>    │  │       <script>           │ │
│  │             │  │             │  │                          │ │
│  │ - Variables │  │ - Header    │  │ - Variables globales     │ │
│  │   CSS       │  │ - Upload    │  │ - Event Listeners        │ │
│  │ - Thèmes    │  │ - Export    │  │ - Parsers (CSV, Excel,   │ │
│  │ - Classes   │  │ - Results   │  │   SQLite, JSON, XML)     │ │
│  │ - Export    │  │ - Tabs      │  │ - Exporters (6 formats)  │ │
│  │   buttons   │  │ - Footer    │  │ - Statistiques           │ │
│  │             │  │             │  │ - Prédictions            │ │
│  │             │  │             │  │ - Anomalies              │ │
│  │             │  │             │  │ - NLP                    │ │
│  └─────────────┘  └─────────────┘  └──────────────────────────┘ │
└──────────────────────────────────────────────────────────────────┘
                              │
          ┌───────────────────┼───────────────────┐
          ▼                   ▼                   ▼
┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐
│   Chart.js CDN  │ │  SheetJS CDN    │ │   sql.js CDN    │
│   (graphiques)  │ │  (Excel)        │ │   (SQLite)      │
└─────────────────┘ └─────────────────┘ └─────────────────┘
```

### Flux de données

```
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│   Fichier   │ ──▶ │   Parser     │ ──▶ │  csvData[]  │
│   source    │     │  approprié   │     │  headers[]  │
└─────────────┘     └──────────────┘     └─────────────┘
      │                                         │
      │  .csv  ──▶ parseCSV()                   │
      │  .xlsx ──▶ parseExcel()                 ▼
      │  .db   ──▶ parseSQLite()        ┌─────────────┐
      │  .json ──▶ parseJSON()          │  Analyse &  │
      │  .xml  ──▶ parseXML()           │  Affichage  │
                                        └─────────────┘
                                               │
                                               ▼
                                        ┌─────────────┐
                                        │   Export    │
                                        │  (6 formats)│
                                        └─────────────┘
```

---

## 3. Structure du fichier HTML

### 3.1 En-tête (Head)
```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>DataInsight AI - Analyse Intelligente de Données</title>
    <style>
        /* CSS ici */
    </style>
    <script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>
</head>
```

**Explications :**
- `charset="UTF-8"` : Supporte les caractères français (accents)
- `viewport` : Rend la page responsive (mobile-friendly)
- Chart.js : Chargé depuis un CDN (Content Delivery Network)

### 3.2 Structure du Body
```html
<body>
    <!-- 1. Bouton de thème (fixe en haut à droite) -->
    <div class="theme-toggle" id="themeToggle">...</div>

    <!-- 2. En-tête avec titre -->
    <header class="header">...</header>

    <!-- 3. Contenu principal -->
    <main class="container">
        <!-- Section d'upload -->
        <section id="uploadSection">...</section>

        <!-- Section de chargement -->
        <section id="loadingSection">...</section>

        <!-- Section des résultats (4 onglets) -->
        <section id="resultsSection">...</section>
    </main>

    <!-- 4. Pied de page -->
    <footer class="footer">...</footer>

    <!-- 5. JavaScript -->
    <script>
        // Code JS ici
    </script>
</body>
```

---

## 4. Les variables CSS (Thèmes)

### 4.1 Définition des variables
```css
:root {
    /* Couleurs principales */
    --primary: #667eea;      /* Violet/bleu - couleur principale */
    --secondary: #764ba2;    /* Violet foncé - couleur secondaire */
    --success: #48bb78;      /* Vert - succès/positif */
    --warning: #ed8936;      /* Orange - avertissement */
    --danger: #f56565;       /* Rouge - erreur/danger */

    /* Couleurs de fond et texte (mode clair) */
    --bg-main: #f7fafc;      /* Fond principal */
    --bg-card: #ffffff;      /* Fond des cartes */
    --text-main: #2d3748;    /* Texte principal */
    --text-muted: #a0aec0;   /* Texte secondaire */
    --border-color: #e2e8f0; /* Bordures */
}
```

### 4.2 Thème sombre
```css
[data-theme="dark"] {
    --bg-main: #1a202c;      /* Fond sombre */
    --bg-card: #2d3748;      /* Cartes sombres */
    --text-main: #f7fafc;    /* Texte clair */
    --text-muted: #a0aec0;   /* Texte secondaire */
    --border-color: #4a5568; /* Bordures sombres */
}
```

### 4.3 Comment fonctionne le changement de thème
```javascript
// Quand on clique sur le toggle
themeToggle.addEventListener('click', () => {
    const currentTheme = document.documentElement.getAttribute('data-theme');
    if (currentTheme === 'dark') {
        // Passer en mode clair
        document.documentElement.removeAttribute('data-theme');
        localStorage.setItem('theme', 'light');
    } else {
        // Passer en mode sombre
        document.documentElement.setAttribute('data-theme', 'dark');
        localStorage.setItem('theme', 'dark');
    }
});
```

**Principe :**
1. On ajoute `data-theme="dark"` à `<html>`
2. Le CSS avec `[data-theme="dark"]` s'applique
3. Toutes les variables sont redéfinies
4. Les éléments utilisant `var(--variable)` changent automatiquement

---

## 5. Les composants visuels

### 5.1 Les cartes (Cards)
```css
.card {
    background: var(--bg-card);      /* Utilise la variable */
    border-radius: 12px;              /* Coins arrondis */
    padding: 2rem;                    /* Espacement interne */
    box-shadow: 0 2px 8px rgba(0,0,0,0.1); /* Ombre légère */
    margin-bottom: 1.5rem;
    transition: background 0.3s;      /* Animation douce */
}
```

### 5.2 Zone d'upload (Drag & Drop)
```css
.upload-area {
    border: 3px dashed var(--primary); /* Bordure en pointillés */
    border-radius: 12px;
    padding: 3rem;
    text-align: center;
    cursor: pointer;
    transition: all 0.3s;
}

.upload-area:hover {
    background: rgba(102, 126, 234, 0.05); /* Fond légèrement coloré */
    border-color: var(--secondary);
}
```

### 5.3 Les onglets (Tabs)
```css
.tabs {
    display: flex;
    gap: 0.5rem;
    border-bottom: 2px solid var(--border-color);
}

.tab {
    background: none;
    border: none;
    padding: 1rem 1.5rem;
    cursor: pointer;
    border-bottom: 3px solid transparent; /* Ligne invisible */
}

.tab.active {
    color: var(--primary);
    border-bottom-color: var(--primary); /* Ligne visible */
}
```

### 5.4 Les boutons
```css
.btn {
    padding: 0.75rem 1.5rem;
    border: none;
    border-radius: 8px;
    font-size: 1rem;
    cursor: pointer;
    transition: all 0.3s;
}

.btn-primary {
    /* Dégradé de couleurs */
    background: linear-gradient(135deg, var(--primary) 0%, var(--secondary) 100%);
    color: white;
}

.btn-primary:hover {
    transform: translateY(-2px);  /* Monte légèrement */
    box-shadow: 0 4px 12px rgba(102, 126, 234, 0.4); /* Ombre */
}
```

---

## 6. Le JavaScript - Variables globales

```javascript
// Données du fichier CSV
let csvData = null;        // Tableau d'objets [{col1: val1, col2: val2}, ...]
let headers = [];          // Noms des colonnes ["col1", "col2", ...]
let numericColumns = [];   // Colonnes numériques seulement

// Graphiques
let currentChart = null;       // Instance Chart.js actuelle
let currentChartType = 'line'; // Type de graphique sélectionné
let currentChartColumn = null; // Colonne affichée dans le graphique

// Statistiques calculées
let allStats = {};  // {colonne: {mean, median, std, min, max, ...}}
```

---

## 7. Import multi-format

L'application supporte l'import de 5 formats de fichiers différents. Chaque format a son propre parser.

### 7.1 Gestion des fichiers

```javascript
function handleFile(file) {
    const validExtensions = ['.csv', '.xlsx', '.xls', '.db', '.sqlite', '.sqlite3', '.json', '.xml'];
    const ext = '.' + file.name.split('.').pop().toLowerCase();

    if (!validExtensions.includes(ext)) {
        alert('Format non supporté');
        return;
    }

    window.selectedFile = file;
    window.fileExtension = ext;
}
```

### 7.2 Parser CSV

```javascript
function parseCSV(text) {
    const lines = text.trim().split('\n');
    // Supporte virgule (,) ou point-virgule (;)
    headers = lines[0].split(/[,;]/).map(h => h.trim().replace(/"/g, ''));
    csvData = [];

    for (let i = 1; i < lines.length; i++) {
        const values = lines[i].split(/[,;]/).map(v => v.trim().replace(/"/g, ''));
        if (values.length === headers.length) {
            const row = {};
            headers.forEach((h, idx) => {
                const val = values[idx];
                row[h] = isNaN(parseFloat(val)) ? val : parseFloat(val);
            });
            csvData.push(row);
        }
    }
    detectNumericColumns();
}
```

### 7.3 Parser Excel (SheetJS)

```javascript
function parseExcel(arrayBuffer) {
    // Lire le fichier avec SheetJS
    const workbook = XLSX.read(arrayBuffer, { type: 'array' });
    const firstSheetName = workbook.SheetNames[0];
    const worksheet = workbook.Sheets[firstSheetName];

    // Convertir en tableau JSON
    const jsonData = XLSX.utils.sheet_to_json(worksheet, { header: 1 });

    // La première ligne contient les en-têtes
    headers = jsonData[0].map(h => String(h || 'Colonne').trim());
    csvData = [];

    // Parcourir les lignes de données
    for (let i = 1; i < jsonData.length; i++) {
        const values = jsonData[i];
        if (values && values.length > 0) {
            const row = {};
            headers.forEach((h, idx) => {
                const val = values[idx];
                if (typeof val === 'number') {
                    row[h] = val;
                } else {
                    const parsed = parseFloat(val);
                    row[h] = isNaN(parsed) ? val : parsed;
                }
            });
            csvData.push(row);
        }
    }
    detectNumericColumns();
}
```

### 7.4 Parser SQLite (sql.js)

```javascript
async function parseSQLite(arrayBuffer) {
    // Initialiser sql.js
    const SQL = await initSqlJs({
        locateFile: file => `https://cdn.jsdelivr.net/npm/sql.js@1.8.0/dist/${file}`
    });

    // Ouvrir la base de données
    const db = new SQL.Database(new Uint8Array(arrayBuffer));

    // Lister les tables disponibles
    const tables = db.exec("SELECT name FROM sqlite_master WHERE type='table'");
    const tableNames = tables[0].values.map(t => t[0]);

    // Si plusieurs tables, demander à l'utilisateur
    let selectedTable = tableNames[0];
    if (tableNames.length > 1) {
        selectedTable = prompt('Choisissez une table:', tableNames[0]);
    }

    // Exécuter la requête SELECT
    const result = db.exec(`SELECT * FROM "${selectedTable}"`);

    headers = result[0].columns;
    csvData = result[0].values.map(row => {
        const rowObj = {};
        headers.forEach((h, idx) => {
            rowObj[h] = row[idx];
        });
        return rowObj;
    });

    db.close();
    detectNumericColumns();
}
```

### 7.5 Parser JSON

```javascript
function parseJSON(text) {
    let data = JSON.parse(text);

    // Si c'est un objet avec une clé contenant un tableau
    if (!Array.isArray(data)) {
        for (const key of Object.keys(data)) {
            if (Array.isArray(data[key])) {
                data = data[key];
                break;
            }
        }
    }

    // Extraire les en-têtes de tous les objets
    const allKeys = new Set();
    data.forEach(item => {
        Object.keys(item).forEach(k => allKeys.add(k));
    });

    headers = Array.from(allKeys);
    csvData = data.map(item => {
        const row = {};
        headers.forEach(h => {
            const val = item[h];
            if (typeof val === 'number') {
                row[h] = val;
            } else if (typeof val === 'string') {
                const parsed = parseFloat(val);
                row[h] = isNaN(parsed) ? val : parsed;
            } else {
                row[h] = val;
            }
        });
        return row;
    });

    detectNumericColumns();
}
```

### 7.6 Parser XML

```javascript
function parseXML(text) {
    const parser = new DOMParser();
    const xmlDoc = parser.parseFromString(text, 'text/xml');
    const root = xmlDoc.documentElement;
    const children = Array.from(root.children);

    // Trouver le tag le plus fréquent (= enregistrements)
    const tagCounts = {};
    children.forEach(child => {
        tagCounts[child.tagName] = (tagCounts[child.tagName] || 0) + 1;
    });
    const dataTag = Object.keys(tagCounts).reduce((a, b) =>
        tagCounts[a] > tagCounts[b] ? a : b
    );
    const dataElements = children.filter(c => c.tagName === dataTag);

    // Extraire les en-têtes (attributs + éléments enfants)
    const allKeys = new Set();
    dataElements.forEach(el => {
        Array.from(el.attributes).forEach(attr => allKeys.add('@' + attr.name));
        Array.from(el.children).forEach(child => allKeys.add(child.tagName));
    });

    headers = Array.from(allKeys);
    csvData = dataElements.map(el => {
        const row = {};
        headers.forEach(h => {
            let val = null;
            if (h.startsWith('@')) {
                val = el.getAttribute(h.substring(1));
            } else {
                const child = el.querySelector(h);
                val = child ? child.textContent.trim() : null;
            }
            const parsed = parseFloat(val);
            row[h] = isNaN(parsed) ? val : parsed;
        });
        return row;
    });

    detectNumericColumns();
}
```

---

## 8. Export et conversion

Une fois les données chargées, elles peuvent être exportées vers 6 formats différents.

### 8.1 Interface d'export

```html
<div class="export-buttons">
    <button class="btn btn-export" data-format="csv">📊 CSV</button>
    <button class="btn btn-export" data-format="xlsx">📗 Excel</button>
    <button class="btn btn-export" data-format="json">📋 JSON</button>
    <button class="btn btn-export" data-format="xml">📄 XML</button>
    <button class="btn btn-export" data-format="sql">🗄️ SQL</button>
    <button class="btn btn-export" data-format="html">🌐 HTML</button>
</div>
```

### 8.2 Fonction utilitaire de téléchargement

```javascript
function downloadFile(content, filename, mimeType) {
    const blob = new Blob([content], { type: mimeType });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = filename;
    document.body.appendChild(a);
    a.click();
    document.body.removeChild(a);
    URL.revokeObjectURL(url);
}
```

### 8.3 Export CSV

```javascript
function exportToCSV() {
    let csv = headers.join(';') + '\n';
    csvData.forEach(row => {
        const values = headers.map(h => {
            const val = row[h];
            if (val === null) return '';
            // Échapper les valeurs contenant des séparateurs
            if (typeof val === 'string' && val.includes(';')) {
                return '"' + val.replace(/"/g, '""') + '"';
            }
            return val;
        });
        csv += values.join(';') + '\n';
    });
    downloadFile(csv, 'export_donnees.csv', 'text/csv;charset=utf-8');
}
```

### 8.4 Export Excel

```javascript
function exportToExcel() {
    // Créer les données pour la feuille
    const wsData = [headers];
    csvData.forEach(row => {
        wsData.push(headers.map(h => row[h] || ''));
    });

    // Créer le workbook avec SheetJS
    const ws = XLSX.utils.aoa_to_sheet(wsData);
    const wb = XLSX.utils.book_new();
    XLSX.utils.book_append_sheet(wb, ws, 'Donnees');

    // Télécharger
    XLSX.writeFile(wb, 'export_donnees.xlsx');
}
```

### 8.5 Export JSON

```javascript
function exportToJSON() {
    const jsonContent = JSON.stringify(csvData, null, 2);
    downloadFile(jsonContent, 'export_donnees.json', 'application/json');
}
```

### 8.6 Export XML

```javascript
function exportToXML() {
    let xml = '<?xml version="1.0" encoding="UTF-8"?>\n<data>\n';

    csvData.forEach((row, index) => {
        xml += '  <record id="' + (index + 1) + '">\n';
        headers.forEach(h => {
            // Créer un nom de tag valide
            const safeTag = h.replace(/[^a-zA-Z0-9_]/g, '_');
            const val = row[h];
            // Échapper les caractères spéciaux XML
            const safeVal = val ? String(val)
                .replace(/&/g, '&amp;')
                .replace(/</g, '&lt;')
                .replace(/>/g, '&gt;') : '';
            xml += '    <' + safeTag + '>' + safeVal + '</' + safeTag + '>\n';
        });
        xml += '  </record>\n';
    });

    xml += '</data>';
    downloadFile(xml, 'export_donnees.xml', 'application/xml');
}
```

### 8.7 Export SQL

```javascript
function exportToSQL() {
    const tableName = 'donnees_exportees';
    let sql = '-- Script SQL généré par DataInsight AI\n\n';

    // CREATE TABLE avec détection automatique des types
    sql += 'CREATE TABLE IF NOT EXISTS ' + tableName + ' (\n';
    sql += '  id INTEGER PRIMARY KEY AUTOINCREMENT,\n';

    const columnDefs = headers.map(h => {
        const safeCol = h.replace(/[^a-zA-Z0-9_]/g, '_');
        // Détecter le type de données
        const values = csvData.map(r => r[h]).filter(v => v !== null);
        const isNumeric = values.every(v => typeof v === 'number');
        const hasDecimals = isNumeric && values.some(v => !Number.isInteger(v));

        let type = 'TEXT';
        if (isNumeric) type = hasDecimals ? 'REAL' : 'INTEGER';
        return '  ' + safeCol + ' ' + type;
    });
    sql += columnDefs.join(',\n') + '\n);\n\n';

    // INSERT statements
    csvData.forEach(row => {
        const safeCols = headers.map(h => h.replace(/[^a-zA-Z0-9_]/g, '_'));
        const values = headers.map(h => {
            const val = row[h];
            if (val === null) return 'NULL';
            if (typeof val === 'number') return val;
            return "'" + String(val).replace(/'/g, "''") + "'";
        });
        sql += 'INSERT INTO ' + tableName + ' (' + safeCols.join(', ') +
               ') VALUES (' + values.join(', ') + ');\n';
    });

    downloadFile(sql, 'export_donnees.sql', 'text/plain');
}
```

### 8.8 Export HTML

```javascript
function exportToHTML() {
    let html = `<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Export Données</title>
    <style>
        table { border-collapse: collapse; width: 100%; }
        th { background: #667eea; color: white; padding: 12px; }
        td { padding: 10px; border-bottom: 1px solid #e2e8f0; }
        tr:hover { background: #f0f4ff; }
    </style>
</head>
<body>
    <h1>Export de données</h1>
    <table>
        <thead><tr>${headers.map(h => '<th>' + h + '</th>').join('')}</tr></thead>
        <tbody>`;

    csvData.forEach(row => {
        html += '<tr>';
        headers.forEach(h => {
            const val = row[h] || '';
            html += '<td>' + String(val).replace(/</g, '&lt;') + '</td>';
        });
        html += '</tr>';
    });

    html += '</tbody></table></body></html>';
    downloadFile(html, 'export_donnees.html', 'text/html');
}
```

### 8.9 Gestionnaire d'export

```javascript
// Écouteur sur les boutons d'export
document.querySelectorAll('.btn-export').forEach(btn => {
    btn.addEventListener('click', () => {
        const format = btn.dataset.format;
        handleExport(format);
    });
});

function handleExport(format) {
    switch(format) {
        case 'csv': exportToCSV(); break;
        case 'xlsx': exportToExcel(); break;
        case 'json': exportToJSON(); break;
        case 'xml': exportToXML(); break;
        case 'sql': exportToSQL(); break;
        case 'html': exportToHTML(); break;
    }
}
```

---

## 9. Fonctionnalités détaillées

### 9.1 Calcul des statistiques

```javascript
// Pour chaque colonne numérique
numericColumns.forEach(col => {
    // Extraire les valeurs numériques valides
    const values = csvData.map(r => r[col])
                          .filter(v => typeof v === 'number' && !isNaN(v));

    if (values.length > 0) {
        // MOYENNE : somme / nombre d'éléments
        const mean = values.reduce((a, b) => a + b, 0) / values.length;

        // MÉDIANE : valeur du milieu quand triées
        const sorted = [...values].sort((a, b) => a - b);
        const median = sorted[Math.floor(sorted.length / 2)];

        // ÉCART-TYPE : mesure de dispersion
        const std = Math.sqrt(
            values.reduce((sum, v) => sum + Math.pow(v - mean, 2), 0) / values.length
        );

        // MIN et MAX
        const min = Math.min(...values);
        const max = Math.max(...values);

        // QUARTILES (pour IQR)
        const q1 = sorted[Math.floor(sorted.length * 0.25)]; // 25%
        const q3 = sorted[Math.floor(sorted.length * 0.75)]; // 75%
        const iqr = q3 - q1; // Écart interquartile

        // Stocker les stats
        allStats[col] = { mean, median, std, min, max, q1, q3, iqr, values };
    }
});
```

### 9.2 Calcul des corrélations

```javascript
function calculateCorrelation(col1, col2) {
    // 1. Récupérer les paires de valeurs valides
    const pairs = csvData.filter(r =>
        typeof r[col1] === 'number' && typeof r[col2] === 'number'
    );

    if (pairs.length < 3) return 0; // Pas assez de données

    const x = pairs.map(r => r[col1]);
    const y = pairs.map(r => r[col2]);
    const n = x.length;

    // 2. Calculer les sommes nécessaires
    const sumX = x.reduce((a, b) => a + b, 0);
    const sumY = y.reduce((a, b) => a + b, 0);
    const sumXY = x.reduce((sum, xi, i) => sum + xi * y[i], 0);
    const sumX2 = x.reduce((sum, xi) => sum + xi * xi, 0);
    const sumY2 = y.reduce((sum, yi) => sum + yi * yi, 0);

    // 3. Formule de corrélation de Pearson
    const numerateur = n * sumXY - sumX * sumY;
    const denominateur = Math.sqrt(
        (n * sumX2 - sumX * sumX) * (n * sumY2 - sumY * sumY)
    );

    return denominateur === 0 ? 0 : numerateur / denominateur;
}
```

**Interprétation de la corrélation :**
- **+1** : Corrélation positive parfaite (quand X augmente, Y augmente)
- **0** : Aucune corrélation linéaire
- **-1** : Corrélation négative parfaite (quand X augmente, Y diminue)
- **|r| > 0.7** : Corrélation forte
- **|r| > 0.5** : Corrélation modérée
- **|r| > 0.3** : Corrélation faible

---

## 10. Les algorithmes de prédiction

### 10.1 Régression linéaire

**Principe :** Trouver la droite Y = aX + b qui passe au mieux par les points.

```javascript
function predictLinearRegression(values, steps) {
    const n = values.length;
    let sumX = 0, sumY = 0, sumXY = 0, sumX2 = 0;

    // X = index (0, 1, 2, ...), Y = valeur
    for (let i = 0; i < n; i++) {
        sumX += i;
        sumY += values[i];
        sumXY += i * values[i];
        sumX2 += i * i;
    }

    // Formule des moindres carrés
    // pente (a) = (n*ΣXY - ΣX*ΣY) / (n*ΣX² - (ΣX)²)
    const slope = (n * sumXY - sumX * sumY) / (n * sumX2 - sumX * sumX);

    // ordonnée à l'origine (b) = (ΣY - a*ΣX) / n
    const intercept = (sumY - slope * sumX) / n;

    // Générer les prédictions futures
    const predictions = [];
    for (let i = 0; i < steps; i++) {
        // Y = a * X + b, où X = n + i (point futur)
        predictions.push(slope * (n + i) + intercept);
    }

    return {
        predictions,
        slope,      // Pente de la droite
        intercept,  // Ordonnée à l'origine
        trend: slope > 0 ? 'hausse' : slope < 0 ? 'baisse' : 'stable'
    };
}
```

**Exemple visuel :**
```
Valeurs : [10, 12, 15, 18, 20]

20 |           *
18 |         *   ----→ Prédictions
15 |       *
12 |     *
10 |   *
   +---------------
     0  1  2  3  4  5  6  7
```

### 10.2 Moyenne mobile simple

**Principe :** Utiliser la moyenne des dernières valeurs pour prédire.

```javascript
function predictMovingAverage(values, steps, windowSize = 5) {
    // Ajuster la fenêtre si pas assez de données
    windowSize = Math.min(windowSize, Math.floor(values.length / 2));

    // Prendre les dernières valeurs
    const lastValues = values.slice(-windowSize);

    // Calculer leur moyenne
    const avg = lastValues.reduce((a, b) => a + b, 0) / lastValues.length;

    // Calculer la tendance récente
    const recentTrend = (values[values.length - 1] - values[values.length - windowSize]) / windowSize;

    // Générer les prédictions
    const predictions = [];
    for (let i = 0; i < steps; i++) {
        predictions.push(avg + recentTrend * i);
    }

    return { predictions, average: avg, trend: ... };
}
```

**Exemple :**
```
Valeurs : [10, 12, 15, 18, 20]
Fenêtre = 3 dernières valeurs : [15, 18, 20]
Moyenne = (15 + 18 + 20) / 3 = 17.67
Tendance = (20 - 15) / 3 = 1.67 par point

Prédictions : 17.67, 19.34, 21.01, ...
```

### 10.3 Moyenne mobile exponentielle (EMA)

**Principe :** Donner plus de poids aux valeurs récentes.

```javascript
function predictEMA(values, steps, alpha = 0.3) {
    // Initialiser l'EMA avec la première valeur
    let ema = values[0];

    // Calculer l'EMA progressivement
    // EMA = α * valeur_actuelle + (1 - α) * EMA_précédent
    for (let i = 1; i < values.length; i++) {
        ema = alpha * values[i] + (1 - alpha) * ema;
    }

    // Calculer la tendance sur les 5 dernières valeurs
    const recentValues = values.slice(-5);
    const trend = (recentValues[recentValues.length - 1] - recentValues[0]) / recentValues.length;

    // Générer les prédictions
    const predictions = [];
    let currentEma = ema;
    for (let i = 0; i < steps; i++) {
        currentEma = currentEma + trend;
        predictions.push(currentEma);
    }

    return { predictions, lastEma: ema, trend: ... };
}
```

**Paramètre α (alpha) :**
- α proche de 1 : réagit vite aux changements récents
- α proche de 0 : lisse davantage, moins sensible aux fluctuations

---

## 11. La détection d'anomalies

### 11.1 Méthode Z-Score

**Principe :** Une valeur est anormale si elle est à plus de 3 écarts-types de la moyenne.

```javascript
// Calculer le Z-Score pour chaque valeur
const zscoreAnomalies = values.map((v, i) => ({
    value: v,
    index: i,
    zscore: (v - mean) / std  // Z = (valeur - moyenne) / écart-type
})).filter(item => Math.abs(item.zscore) > 3);  // |Z| > 3 = anomalie
```

**Interprétation :**
```
Distribution normale :
                    │
      ▄▄▄▄██████▄▄▄▄│
   ▄██              ██▄
 ▄█                    █▄
─────────────────────────────
     -3σ  -2σ  -σ  μ  +σ +2σ +3σ

- 68% des données sont entre -1σ et +1σ
- 95% des données sont entre -2σ et +2σ
- 99.7% des données sont entre -3σ et +3σ

→ Une valeur au-delà de ±3σ est très rare (0.3%)
```

### 11.2 Méthode IQR (Interquartile Range)

**Principe :** Utiliser les quartiles pour définir les bornes normales.

```javascript
// Calculer les quartiles
const q1 = sorted[Math.floor(sorted.length * 0.25)];  // 25%
const q3 = sorted[Math.floor(sorted.length * 0.75)];  // 75%
const iqr = q3 - q1;

// Définir les bornes
const lowerBound = q1 - 1.5 * iqr;  // Borne inférieure
const upperBound = q3 + 1.5 * iqr;  // Borne supérieure

// Détecter les anomalies
const iqrAnomalies = values.filter(v => v < lowerBound || v > upperBound);
```

**Représentation (Box Plot) :**
```
           Anomalie
              │
     ┌────────┼────────┐
─────┤   ▓▓▓▓▓█▓▓▓▓▓   ├─────
     └────────┼────────┘
              │
     Borne    │    Borne
     inf.     │    sup.
              │
  Q1-1.5*IQR Q1  Q3  Q3+1.5*IQR
```

### 11.3 Méthode Isolation Forest (simplifiée)

**Principe :** Les anomalies sont des points "isolés" loin de la majorité.

```javascript
// Version simplifiée : écart à la médiane
const threshold = std * 2.5;
const isolationAnomalies = values.filter(v =>
    Math.abs(v - median) > threshold
);
```

---

## 12. L'assistant IA (NLP)

### 12.1 Normalisation du texte

```javascript
function normalizeText(text) {
    return text.toLowerCase()           // minuscules
        .normalize('NFD')               // décomposer les accents
        .replace(/[\u0300-\u036f]/g, '') // supprimer les accents
        .trim();                        // supprimer espaces
}

// Exemple :
// "Créé" → "cree"
// "Prédis" → "predis"
// "Détecte" → "detecte"
```

### 12.2 Détection des intentions

```javascript
function processNLPQuery() {
    const query = normalizeText(rawQuery);

    // 1. Graphique ?
    if (query.includes('graphique') || query.includes('graph')) {
        const chartType = detectChartType(query);
        const column = detectColumn(query);
        updateChart(chartType, column);
    }

    // 2. Prédiction ?
    else if (query.includes('predi') || query.includes('prevoir')) {
        const column = detectColumn(query);
        const steps = extractNumber(query) || 10;
        generatePredictions();
    }

    // 3. Anomalies ?
    else if (query.includes('anomalie')) {
        displayAnomalies('all');
    }

    // 4. Corrélations ?
    else if (query.includes('correlation')) {
        // Afficher les corrélations
    }

    // 5. Statistiques ?
    else if (query.includes('statistique') || query.includes('analyse')) {
        // Afficher les stats
    }
}
```

### 12.3 Détection du type de graphique

```javascript
function detectChartType(query) {
    if (query.includes('barre')) return 'bar';
    if (query.includes('camembert')) return 'pie';
    if (query.includes('anneau')) return 'doughnut';
    if (query.includes('radar')) return 'radar';
    if (query.includes('polaire')) return 'polarArea';
    return 'line';  // Par défaut
}
```

### 12.4 Détection de la colonne

```javascript
function detectColumn(query) {
    // Chercher si une colonne est mentionnée
    for (const col of numericColumns) {
        if (query.includes(col.toLowerCase())) {
            return col;
        }
    }
    // Sinon, utiliser la première colonne numérique
    return numericColumns[0] || null;
}
```

### 12.5 Extraction de nombre

```javascript
function extractNumber(query) {
    const match = query.match(/(\d+)/);  // Chercher un nombre
    return match ? parseInt(match[1]) : null;
}

// Exemples :
// "pour les 5 prochains mois" → 5
// "10 points" → 10
```

---

## 13. Guide de reproduction pas à pas

### Étape 1 : Créer le fichier HTML de base

```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mon Analyseur de Données</title>
</head>
<body>
    <h1>Analyseur de données</h1>
</body>
</html>
```

### Étape 2 : Ajouter les variables CSS

```html
<style>
    :root {
        --primary: #667eea;
        --bg-main: #f7fafc;
        --bg-card: #ffffff;
        --text-main: #2d3748;
    }

    * { margin: 0; padding: 0; box-sizing: border-box; }

    body {
        font-family: 'Segoe UI', sans-serif;
        background: var(--bg-main);
        color: var(--text-main);
    }
</style>
```

### Étape 3 : Créer la zone d'upload

```html
<div class="upload-area" id="uploadArea">
    <p>Glissez votre fichier CSV ici</p>
    <input type="file" id="fileInput" accept=".csv" hidden>
</div>

<script>
    const uploadArea = document.getElementById('uploadArea');
    const fileInput = document.getElementById('fileInput');

    uploadArea.addEventListener('click', () => fileInput.click());

    fileInput.addEventListener('change', (e) => {
        if (e.target.files.length > 0) {
            handleFile(e.target.files[0]);
        }
    });
</script>
```

### Étape 4 : Lire le fichier CSV

```javascript
function handleFile(file) {
    const reader = new FileReader();
    reader.onload = function(e) {
        parseCSV(e.target.result);
    };
    reader.readAsText(file);
}

function parseCSV(text) {
    const lines = text.trim().split('\n');
    const headers = lines[0].split(',');
    // ... reste du parsing
}
```

### Étape 5 : Ajouter Chart.js

```html
<script src="https://cdn.jsdelivr.net/npm/chart.js@4.4.0/dist/chart.umd.min.js"></script>

<canvas id="myChart"></canvas>

<script>
    function createChart(data) {
        const ctx = document.getElementById('myChart');
        new Chart(ctx, {
            type: 'line',
            data: {
                labels: data.map((_, i) => i + 1),
                datasets: [{
                    label: 'Mes données',
                    data: data,
                    borderColor: '#667eea'
                }]
            }
        });
    }
</script>
```

### Étape 6 : Ajouter les onglets

```html
<div class="tabs">
    <button class="tab active" data-tab="overview">Vue d'ensemble</button>
    <button class="tab" data-tab="predictions">Prédictions</button>
</div>

<div id="overviewTab" class="tab-content active">...</div>
<div id="predictionsTab" class="tab-content">...</div>

<script>
    document.querySelectorAll('.tab').forEach(tab => {
        tab.addEventListener('click', () => {
            // Désactiver tous les onglets
            document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
            document.querySelectorAll('.tab-content').forEach(tc => tc.classList.remove('active'));

            // Activer l'onglet cliqué
            tab.classList.add('active');
            document.getElementById(tab.dataset.tab + 'Tab').classList.add('active');
        });
    });
</script>
```

### Étape 7 : Ajouter le thème sombre

```css
[data-theme="dark"] {
    --bg-main: #1a202c;
    --bg-card: #2d3748;
    --text-main: #f7fafc;
}
```

```javascript
document.getElementById('themeToggle').addEventListener('click', () => {
    const html = document.documentElement;
    if (html.getAttribute('data-theme') === 'dark') {
        html.removeAttribute('data-theme');
    } else {
        html.setAttribute('data-theme', 'dark');
    }
});
```

---

## 14. Améliorations possibles

### 14.1 Fonctionnalités réalisées
- [x] Support des fichiers Excel (.xlsx, .xls) via SheetJS
- [x] Support des bases de données SQLite (.db, .sqlite) via sql.js
- [x] Support des fichiers JSON et XML
- [x] Export vers 6 formats (CSV, Excel, JSON, XML, SQL, HTML)
- [x] Conversion entre formats de données

### 14.2 Fonctionnalités à ajouter
- [ ] Export des résultats en PDF
- [ ] Export des graphiques en image
- [ ] Filtrage des données
- [ ] Plus de types de graphiques (histogramme, scatter plot)
- [ ] Sauvegarde des analyses en local (localStorage)
- [ ] Prévisualisation des données avant import

### 14.3 Algorithmes supplémentaires
- [ ] Régression polynomiale
- [ ] Clustering (K-means)
- [ ] Détection de saisonnalité
- [ ] ARIMA pour les séries temporelles

### 14.4 Améliorations UX
- [ ] Tutoriel interactif
- [ ] Tooltips d'aide
- [ ] Raccourcis clavier
- [ ] Mode plein écran pour les graphiques
- [ ] Sélection de feuille pour fichiers Excel multi-feuilles

---

## Glossaire

| Terme | Définition |
|-------|------------|
| **CSV** | Comma-Separated Values - format de fichier texte avec des valeurs séparées par des virgules |
| **CDN** | Content Delivery Network - serveur distant pour charger des librairies |
| **DOM** | Document Object Model - représentation de la page HTML en JavaScript |
| **EMA** | Exponential Moving Average - moyenne mobile exponentielle |
| **IQR** | Interquartile Range - écart entre le 1er et 3ème quartile |
| **JSON** | JavaScript Object Notation - format de données texte léger et lisible |
| **NLP** | Natural Language Processing - traitement du langage naturel |
| **Régression** | Méthode statistique pour trouver une relation entre variables |
| **SheetJS** | Bibliothèque JavaScript pour lire/écrire des fichiers Excel |
| **sql.js** | Portage de SQLite en JavaScript via WebAssembly |
| **SQLite** | Base de données relationnelle légère stockée dans un fichier |
| **XML** | eXtensible Markup Language - format de données structuré avec balises |
| **Z-Score** | Nombre d'écarts-types entre une valeur et la moyenne |

---

## Ressources

- [Chart.js Documentation](https://www.chartjs.org/docs/)
- [SheetJS Documentation](https://docs.sheetjs.com/)
- [sql.js Documentation](https://sql.js.org/)
- [MDN Web Docs - JavaScript](https://developer.mozilla.org/fr/docs/Web/JavaScript)
- [CSS Variables](https://developer.mozilla.org/fr/docs/Web/CSS/Using_CSS_custom_properties)

---


