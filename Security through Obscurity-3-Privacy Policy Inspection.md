Méthodologie

    Lecture Attentive de la Politique de Confidentialité

        Navigué vers la page "Privacy Policy" de l'application

        Lu attentivement l'intégralité du texte

        Noté que certaines parties du texte semblaient interactives

    Examen Visuel et Interaction

        Passé le curseur de la souris sur tout le texte de la politique

        Observé que certains mots ou phrases changeaient d'apparence au survol

        Identifié des éléments qui s'"illuminaient" ou changeaient de couleur

    Inspection du Code Source HTML

        Clic droit → "Inspecter l'élément" sur les parties interactives

        Observé que certains mots étaient entourés de balises <a> (liens)

        Noté que les liens avaient des attributs href inhabituels

    Découverte du Lien Caché

        Identifié un lien spécifique qui pointait vers :
        text

https://ctf.juice.cyber.epitest.eu/we/may/also/instruct/you/to/refuse/all/reasonably/necessary/responsibility/

        Remarqué que l'URL semblait former une phrase complète

    Navigation vers le Lien

        Cliqué sur le lien ou copié/collé l'URL dans la barre d'adresse

        Accédé à la page cible

        Observé le contenu de la page : une erreur 404 avec des détails techniques

    Analyse de la Réponse du Serveur

        Page affichée contenait :

            "OWASP Juice Shop (Express ^4.21.0)"

            "404 Error: ENOENT: no such file or directory"

            Chemin du fichier manquant : /juice-shop/frontend/dist/frontend/assets/private/thank-you.jpg

        Noté que l'erreur révélait des informations sur la structure du projet

    Interprétation de l'Échec

        Compris que l'accès à cette URL démontrait la lecture attentive

        Réalisé que l'erreur 404 était intentionnelle et faisait partie du challenge

        Le simple fait d'accéder à l'URL cachée validait le challenge

Outils Utilisés

    Navigateur web avec fonctionnalités standards

    Inspection visuelle manuelle du texte

    Outils de développement (Inspecteur d'éléments) pour analyse HTML

    Navigation web standard vers les URLs

Vulnérabilités Identifiées
Vulnérabilité Principale

    Nom : Contenu Caché / Easter Eggs dans les Documents Officiels

    Type : CWE-200: Information Exposure / CWE-530: Exposure of Backup File

    Composants Affectés :

        Pages de contenu statique (politique de confidentialité)

        Mise en œuvre HTML/CSS

        Gestion des erreurs côté serveur

Niveau de Sévérité

    Évaluation : Faible (Low) à Moyen (Medium)

    Justification :

        Exposition d'informations sur la structure du projet

        Révélation de chemins de fichiers internes

        Peut aider à la reconnaissance pour d'autres attaques

        Bien que l'information soit limitée, elle réduit l'opacité du système

Impacts et Risques
Impact Business

    Exposition d'Informations Techniques :

        Révélation de la stack technologique (Express.js 4.21.0)

        Exposition de la structure des répertoires du projet

        Informations pouvant aider à d'autres attaques

    Problèmes de Conformité :

        Les politiques de confidentialité ne devraient pas contenir de contenu caché

        Potentielle violation des principes de transparence

        Risque de confusion pour les utilisateurs légitimes

    Reconnaissance Facilitation :

        Les attaquants peuvent utiliser ces informations pour :

            Identifier des versions vulnérables

            Comprendre l'architecture de l'application

            Trouver d'autres chemins ou fichiers sensibles

    Érosion de la Confiance :

        Les utilisateurs pourraient se méfier des documents officiels

        Perception de malhonnêteté ou de tromperie

        Impact sur la crédibilité de l'organisation

Actions Correctives
Stratégies d'Atténuation des Risques

    Transparence Complète :

        Éviter tout contenu caché dans les documents officiels

        Les politiques doivent être claires et sans surprises

    Gestion Appropriée des Erreurs :

        Les pages d'erreur ne devraient pas révéler d'informations techniques

        Implémenter des pages d'erreur génériques en production
