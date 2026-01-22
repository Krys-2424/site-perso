# Documentation Portfolio - Krystal Chapiteau

## Table des matières

1. [Présentation générale](#1-présentation-générale)
2. [Technologies utilisées](#2-technologies-utilisées)
3. [Architecture du projet](#3-architecture-du-projet)
4. [Structure HTML](#4-structure-html)
5. [Système de style CSS](#5-système-de-style-css)
6. [Fonctionnalités JavaScript](#6-fonctionnalités-javascript)
7. [Section Projets](#7-section-projets)
8. [Section Certifications](#8-section-certifications)
9. [Système de gamification](#9-système-de-gamification)
10. [Système multilingue](#10-système-multilingue)
11. [Responsive Design](#11-responsive-design)
12. [Personnalisation](#12-personnalisation)
13. [Déploiement](#13-déploiement)
14. [Maintenance](#14-maintenance)

---

## 1. Présentation générale

### Description
Portfolio personnel gamifié avec un design rétro-futuriste inspiré de l'univers du jeu vidéo. Ce site one-page présente les projets, compétences et certifications de manière interactive et engageante.

### Caractéristiques principales
| Fonctionnalité | Description |
|----------------|-------------|
| Design gamifié | Système d'XP, achievements, niveau |
| Animations cosmiques | Étoiles animées, effets de glow |
| Multilingue | Français / Anglais |
| Responsive | Adapté mobile, tablette, desktop |
| Projets GitHub | Liens directs vers les repos épinglés |
| Téléchargement | Export ZIP de chaque projet |
| Certifications | Section dédiée avec preuves téléchargeables |

### Aperçu des sections
```
┌─────────────────────────────────────┐
│           NAVIGATION                │
├─────────────────────────────────────┤
│           HERO SECTION              │
│    Nom + Titre + Call-to-Action     │
├─────────────────────────────────────┤
│           PROJETS                   │
│    3 cartes avec GitHub/Démo/DL     │
├─────────────────────────────────────┤
│          COMPÉTENCES                │
│    Barres de progression animées    │
├─────────────────────────────────────┤
│         CERTIFICATIONS              │
│    Cartes avec preuves à DL         │
├─────────────────────────────────────┤
│           À PROPOS                  │
│         Présentation perso          │
├─────────────────────────────────────┤
│           CONTACT                   │
│      Email / GitHub / LinkedIn      │
├─────────────────────────────────────┤
│           FOOTER                    │
└─────────────────────────────────────┘
```

---

## 2. Technologies utilisées

### Frontend
| Technologie | Version | Utilisation |
|-------------|---------|-------------|
| HTML5 | - | Structure sémantique |
| CSS3 | - | Styles, animations, responsive |
| JavaScript | ES6+ | Interactivité, gamification |

### Fonctionnalités CSS avancées
- **CSS Variables** : Thème de couleurs centralisé
- **CSS Grid** : Mise en page des cartes projets/certifications
- **Flexbox** : Alignement navigation et boutons
- **Animations @keyframes** : Étoiles, glow, barres de progression
- **Gradients** : Arrière-plans et boutons
- **Backdrop-filter** : Effet blur sur navigation

### Aucune dépendance externe
Le site est 100% autonome, sans CDN ni bibliothèques externes.

---

## 3. Architecture du projet

### Structure des fichiers
```
site-perso/
├── index.html                    # Page principale (tout-en-un)
├── DOCUMENTATION_PORTFOLIO.md    # Cette documentation
├── README.md                     # Présentation rapide
└── assets/                       # (optionnel) Images/fichiers
    └── certifications/           # Preuves PDF des certifications
```

### Architecture monolithique
Tout le code (HTML, CSS, JavaScript) est contenu dans un seul fichier `index.html` pour :
- Déploiement simplifié sur GitHub Pages
- Pas de requêtes HTTP supplémentaires
- Chargement ultra-rapide

---

## 4. Structure HTML

### Sections principales

#### 4.1 En-tête et métadonnées
```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Site personnel gratuit...">
    <meta name="keywords" content="https://github.com/Krys-2424">
    <meta name="author" content="https://github.com/Krys-2424">
    <title>Krystal Chapiteau | Portfolio Dev</title>
</head>
```

#### 4.2 Éléments fixes
```html
<!-- Barre de progression de scroll -->
<div class="scroll-progress" id="scrollProgress"></div>

<!-- Étoiles animées en arrière-plan -->
<div class="stars" id="stars"></div>

<!-- Barre XP -->
<div class="xp-bar">...</div>

<!-- Notification d'achievement -->
<div class="achievement" id="achievement">...</div>

<!-- Badge de niveau -->
<div class="level-badge">...</div>
```

#### 4.3 Navigation
```html
<nav>
    <ul>
        <li><a href="#hero">Accueil</a></li>
        <li><a href="#projects">Projets</a></li>
        <li><a href="#skills">Compétences</a></li>
        <li><a href="#certifications">Certifications</a></li>
        <li><a href="#about">À propos</a></li>
        <li><a href="#contact">Contact</a></li>
    </ul>
</nav>
```

#### 4.4 Sections de contenu
Chaque section suit le pattern :
```html
<section id="nom-section">
    <div class="container">
        <h2>Titre de la section</h2>
        <!-- Contenu -->
    </div>
</section>
```

---

## 5. Système de style CSS

### 5.1 Variables CSS (Thème)
```css
:root {
    /* Couleurs de fond */
    --bg-dark: #1a1a2e;
    --bg-section: #16213e;

    /* Couleurs de texte */
    --text-primary: #f0f0ff;
    --text-secondary: #b8c5d6;

    /* Couleurs d'accent */
    --accent-cyan: #00d9ff;      /* Principal - liens, titres */
    --accent-purple: #b366ff;    /* Secondaire - hover, badges */
    --accent-pink: #ff66b3;      /* Tertiaire - highlights */
    --accent-green: #66ff99;     /* Succès - boutons télécharger */

    /* Effets de glow */
    --glow-blue: rgba(0, 217, 255, 0.4);
    --glow-purple: rgba(179, 102, 255, 0.4);
    --glow-pink: rgba(255, 102, 179, 0.4);
}
```

### 5.2 Classes de boutons
| Classe | Couleur | Utilisation |
|--------|---------|-------------|
| `.btn` | Cyan | Bouton principal (GitHub) |
| `.btn-secondary` | Violet | Bouton secondaire (Démo) |
| `.btn-download` | Vert | Bouton téléchargement |

### 5.3 Animations principales
```css
/* Scintillement des étoiles */
@keyframes twinkle {
    0%, 100% { opacity: 0.4; transform: scale(1); }
    50% { opacity: 1; transform: scale(1.5); }
}

/* Effet glow sur titre */
@keyframes glow {
    0%, 100% { filter: drop-shadow(0 0 20px cyan); }
    33% { filter: drop-shadow(0 0 25px purple); }
    66% { filter: drop-shadow(0 0 25px pink); }
}

/* Flottement du badge niveau */
@keyframes float {
    0%, 100% { transform: translateY(0px); }
    50% { transform: translateY(-10px); }
}

/* Apparition des achievements */
@keyframes slideIn {
    from { transform: translateX(400px); opacity: 0; }
    to { transform: translateX(0); opacity: 1; }
}
```

---

## 6. Fonctionnalités JavaScript

### 6.1 Génération des étoiles
```javascript
function createStars() {
    const starsContainer = document.getElementById('stars');
    const starCount = 100;

    for (let i = 0; i < starCount; i++) {
        const star = document.createElement('div');
        star.className = 'star';
        star.style.left = Math.random() * 100 + '%';
        star.style.top = Math.random() * 100 + '%';
        star.style.animationDelay = Math.random() * 3 + 's';
        starsContainer.appendChild(star);
    }
}
```

### 6.2 Barre de progression de scroll
```javascript
function updateScrollProgress() {
    const scrollProgress = document.getElementById('scrollProgress');
    const scrollTop = window.scrollY;
    const docHeight = document.documentElement.scrollHeight - window.innerHeight;
    const scrollPercent = (scrollTop / docHeight) * 100;
    scrollProgress.style.width = scrollPercent + '%';

    // Mise à jour de l'XP en fonction du scroll
    const xp = Math.floor((scrollPercent / 100) * 350) + 450;
    document.getElementById('xpText').textContent = xp + '/800';
    document.getElementById('xpFill').style.width = ((xp / 800) * 100) + '%';
}
```

### 6.3 Système d'achievements
```javascript
const achievements = {
    scrolled50: { title: '🔍 Explorateur', desc: 'Scroll 50% du site', triggered: false },
    visitedProjects: { title: '⚔️ Chasseur de quêtes', desc: 'Section Projets visitée', triggered: false },
    visitedSkills: { title: '📊 Analyste', desc: 'Section Compétences visitée', triggered: false },
    scrolled100: { title: '🏆 Master Explorer', desc: 'Site complètement exploré', triggered: false }
};

function showAchievement(achievement) {
    const achievementEl = document.getElementById('achievement');
    document.getElementById('achievementTitle').textContent = achievement.title;
    document.getElementById('achievementDesc').textContent = achievement.desc;
    achievementEl.classList.add('show');

    setTimeout(() => {
        achievementEl.classList.remove('show');
    }, 3000);
}
```

### 6.4 Animation des compétences
```javascript
// Dans revealOnScroll()
if (section.id === 'skills') {
    const skillItems = section.querySelectorAll('.skill-item');
    skillItems.forEach(item => item.classList.add('animate'));
}
```

### 6.5 Smooth scroll
```javascript
document.querySelectorAll('a[href^="#"]').forEach(anchor => {
    anchor.addEventListener('click', function (e) {
        e.preventDefault();
        const target = document.querySelector(this.getAttribute('href'));
        if (target) {
            target.scrollIntoView({ behavior: 'smooth', block: 'start' });
        }
    });
});
```

---

## 7. Section Projets

### 7.1 Structure d'une carte projet
```html
<div class="project-card">
    <!-- Badge de statut -->
    <span class="project-status status-complete">⭐ Complété</span>
    <!-- ou -->
    <span class="project-status status-progress">🔄 En cours</span>

    <!-- Titre -->
    <h3>Nom du projet</h3>

    <!-- Description -->
    <p data-fr="Description FR" data-en="Description EN">
        Description FR
    </p>

    <!-- Technologies -->
    <div class="project-tech">
        <span class="tech-tag">Python</span>
        <span class="tech-tag">JavaScript</span>
    </div>

    <!-- Liens -->
    <div class="project-links">
        <a href="URL_GITHUB" class="btn">💻 GitHub</a>
        <a href="URL_DEMO" class="btn btn-secondary">🚀 Démo</a>
        <a href="URL_ZIP" class="btn btn-download">📥 Télécharger</a>
    </div>
</div>
```

### 7.2 Projets actuels (épinglés GitHub)

| Projet | Description | Technologies |
|--------|-------------|--------------|
| **AI_TDAH** | Assistant pédagogique IA pour TDAH | Python, Puter.js, HTML/CSS |
| **DataInsight AI** | Analyse de données multi-format | HTML, JS, Chart.js, SheetJS |
| **Site Personnel** | Portfolio gamifié | HTML, CSS, JavaScript |

### 7.3 Ajouter un nouveau projet
1. Copier un bloc `<div class="project-card">...</div>`
2. Modifier le statut (`status-complete` ou `status-progress`)
3. Changer le titre, description, technologies
4. Mettre à jour les liens GitHub/Démo/Télécharger

### 7.4 URL de téléchargement GitHub
Format : `https://github.com/USERNAME/REPO/archive/refs/heads/main.zip`

---

## 8. Section Certifications

### 8.1 Structure d'une carte certification
```html
<div class="certification-card">
    <!-- Titre -->
    <h3 data-fr="Titre FR" data-en="Title EN">Titre FR</h3>

    <!-- Organisme -->
    <div class="certification-org" data-fr="Organisme FR" data-en="Org EN">
        Organisme FR
    </div>

    <!-- Date -->
    <div class="certification-date" data-fr="📅 Janvier 2025" data-en="📅 January 2025">
        📅 Janvier 2025
    </div>

    <!-- Description -->
    <p class="certification-desc" data-fr="Description FR" data-en="Description EN">
        Description FR
    </p>

    <!-- Bouton télécharger la preuve -->
    <div class="certification-links">
        <a href="URL_PREUVE.pdf" class="btn btn-download" target="_blank">
            📥 Télécharger la preuve
        </a>
    </div>
</div>
```

### 8.2 Ajouter une certification
1. Copier un bloc `<div class="certification-card">...</div>`
2. Remplir : titre, organisme, date, description
3. Uploader la preuve (PDF/image) dans le repo ou en ligne
4. Mettre à jour le lien `href` du bouton

### 8.3 Héberger les preuves
**Option 1 : Dans le repo**
```
site-perso/
└── assets/
    └── certifications/
        ├── certification1.pdf
        └── certification2.pdf
```
Lien : `./assets/certifications/certification1.pdf`

**Option 2 : Google Drive (lien direct)**
1. Uploader sur Google Drive
2. Partager > Obtenir le lien
3. Modifier l'URL : remplacer `/view` par `/export?format=pdf`

**Option 3 : GitHub directement**
Lien vers le fichier raw dans le repo.

---

## 9. Système de gamification

### 9.1 Composants
| Élément | Description |
|---------|-------------|
| **Barre XP** | Progresse avec le scroll (450-800 XP) |
| **Badge niveau** | Affiche le niveau actuel (flottant) |
| **Achievements** | Notifications débloquées par actions |
| **Barre de scroll** | Progression colorée en haut |

### 9.2 Achievements disponibles
| Achievement | Condition | Icône |
|-------------|-----------|-------|
| Explorateur | Scroll 50% | 🔍 |
| Chasseur de quêtes | Visiter Projets | ⚔️ |
| Analyste | Visiter Compétences | 📊 |
| Master Explorer | Scroll 100% | 🏆 |

### 9.3 Personnaliser les achievements
Dans le JavaScript, modifier l'objet `achievements` :
```javascript
const achievements = {
    nouveauAchievement: {
        title: '🎮 Nouveau',
        desc: 'Description',
        triggered: false
    }
};
```

---

## 10. Système multilingue

### 10.1 Fonctionnement
Chaque élément traduisible a deux attributs :
```html
<p data-fr="Texte français" data-en="English text">
    Texte français
</p>
```

### 10.2 Fonction de changement
```javascript
let currentLang = 'fr';

function toggleLanguage() {
    currentLang = currentLang === 'fr' ? 'en' : 'fr';

    document.querySelectorAll('[data-fr]').forEach(el => {
        el.textContent = el.getAttribute('data-' + currentLang);
    });

    document.getElementById('lang-text').textContent =
        currentLang.toUpperCase() + ' / ' + (currentLang === 'fr' ? 'EN' : 'FR');
}
```

### 10.3 Ajouter une traduction
1. Ajouter `data-fr="..."` et `data-en="..."` à l'élément
2. Le contenu initial est en français
3. Le bouton FR/EN basculera automatiquement

---

## 11. Responsive Design

### 11.1 Breakpoints
```css
@media (max-width: 768px) {
    /* Styles mobile/tablette */
}
```

### 11.2 Adaptations mobiles
| Élément | Desktop | Mobile |
|---------|---------|--------|
| Titre h1 | 3.5rem | 2.5rem |
| Titre h2 | 2.5rem | 2rem |
| Navigation | Horizontal | Wrap |
| Grille projets | Multi-colonnes | 1 colonne |
| Badge niveau | 80x80px | 60x60px |
| Barre XP | 200px | 150px |

---

## 12. Personnalisation

### 12.1 Changer les couleurs
Modifier les variables CSS dans `:root` :
```css
:root {
    --accent-cyan: #00d9ff;    /* Votre couleur */
    --accent-purple: #b366ff;  /* Votre couleur */
    --accent-pink: #ff66b3;    /* Votre couleur */
    --accent-green: #66ff99;   /* Votre couleur */
}
```

### 12.2 Changer les informations personnelles
1. **Nom** : Rechercher "Krystal Chapiteau"
2. **Email** : Rechercher "krystalmarylou@outlook.com"
3. **GitHub** : Rechercher "Krys-2424"
4. **Description** : Section `#about`

### 12.3 Modifier les compétences
Dans la section `#skills`, modifier les `--skill-level` :
```html
<div class="skill-progress" style="--skill-level: 75%"></div>
```

---

## 13. Déploiement

### 13.1 GitHub Pages
1. Aller dans Settings > Pages
2. Source : Deploy from branch
3. Branch : main / (root)
4. Save

URL : `https://krys-2424.github.io/site-perso/`

### 13.2 Mise à jour
```bash
git add .
git commit -m "Description des changements"
git push origin main
```

GitHub Pages se met à jour automatiquement.

---

## 14. Maintenance

### 14.1 Checklist mise à jour
- [ ] Ajouter nouveaux projets quand épinglés sur GitHub
- [ ] Mettre à jour les compétences si progression
- [ ] Ajouter les nouvelles certifications
- [ ] Vérifier les liens (GitHub, démos, téléchargements)
- [ ] Tester le responsive sur mobile

### 14.2 Problèmes courants

| Problème | Solution |
|----------|----------|
| Animations lentes | Réduire le nombre d'étoiles (100 → 50) |
| Texte non traduit | Vérifier `data-fr` et `data-en` présents |
| Lien téléchargement cassé | Vérifier format URL GitHub ZIP |
| Achievement ne s'affiche pas | Vérifier `triggered: false` dans l'objet |

### 14.3 Améliorations futures possibles
- [ ] Mode sombre/clair
- [ ] Plus d'achievements
- [ ] Système de sauvegarde XP (localStorage)
- [ ] Section blog/articles
- [ ] Formulaire de contact fonctionnel
- [ ] Intégration API GitHub pour projets dynamiques

---

## Changelog

### v1.0.0 (Janvier 2025)
- Création initiale du portfolio
- Section projets avec 3 repos GitHub épinglés
- Section certifications
- Système de gamification (XP, achievements)
- Support multilingue FR/EN
- Design responsive

---

**Auteur** : Krystal Chapiteau
**GitHub** : [@Krys-2424](https://github.com/Krys-2424)
**Licence** : MIT
