# HACK & JUICE 🍹

## 📌 Description du projet

HACK & JUICE est un projet de **pentesting** basé sur l'application volontairement vulnérable **OWASP Juice Shop**.
Cette plateforme regroupe de nombreuses failles de sécurité inspirées de cas réels, couvrant notamment le **OWASP Top 10**.

L’objectif est d’exploiter ces vulnérabilités à travers une série de challenges de difficulté variable afin de développer des compétences en cybersécurité offensive.

---

## 🎯 Objectifs

* S'entraîner et améliorer ses compétences en **pentest**
* Résoudre un maximum de challenges proposés sur la plateforme
* Explorer différentes catégories de vulnérabilités (OWASP Top 10)
* Utiliser divers outils et techniques (OSINT, brute force, analyse de code, etc.)

### 🔢 Exigences

* Chaque membre doit :

  * Résoudre **au moins 10 challenges de difficulté ≥ 3**
  * Documenter ses solutions
* Ne pas se limiter à une seule catégorie de vulnérabilités
* Tester plusieurs approches et outils

---

## 🧪 Plateforme

Les challenges sont accessibles via :
👉 [https://juice.cyber.epitest.eu](https://juice.cyber.epitest.eu)

* Inscription automatique via les groupes Epitech
* Instance individuelle de Juice Shop disponible au lancement du CTF
* Challenges classés par :

  * **Catégorie** (OWASP Top 10)
  * **Tags** (Brute force, OSINT, Code analysis, etc.)
  * **Difficulté**

---

## 📂 Structure du dépôt

À la racine du projet, chaque challenge résolu doit être documenté dans un fichier Markdown respectant la convention suivante :

```
categoryName-difficultyLevel-challengeName.md
```

### ✅ Exemples valides :

* `Broken Access Control-3-CSRF.md`
* `Broken Authentication-4-Login Bjoern.md`

### ❌ Exemples invalides :

* `Cross Site Scripting (XSS)-CSP Bypass-4.md`
* `4_User Credentials_Injection.md`

⚠️ Le non-respect de cette convention peut entraîner des pénalités.

---

## 📝 Contenu attendu des documentations

Chaque fichier `.md` doit contenir :

### 🔍 Méthodologie

* Étapes numérotées (1, 2, 3, …)
* Techniques utilisées :

  * OSINT
  * Enumeration
  * Scan
  * Brute force
* Outils utilisés :

  * Burp Suite
  * SQLmap
  * Scripts bash
  * Dictionnaires de mots de passe
  * etc.

### 🛠️ Vulnérabilités

* Type de vulnérabilité (XSS, injection, misconfiguration, etc.)
* Composants affectés (BDD, authentification, etc.)
* Niveau de sévérité estimé :

  * Low / Medium / High / Critical

### ⚠️ Risques

* Impact business :

  * Fuite de données
  * Atteinte à la réputation
  * Compromission système

### 🛡️ Actions

* Mesures de mitigation
* Correctifs recommandés
* Bonnes pratiques de sécurité

### 📎 (Optionnel)

* Screenshots
* Logs
* Scripts
* Captures réseau

---

## 🚀 Conclusion

Ce projet est une immersion pratique dans le monde du **pentesting**.
Il permet de développer des compétences concrètes en sécurité offensive, tout en adoptant une démarche rigoureuse de documentation et d’analyse.
