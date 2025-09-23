# 🤖 Guide de Configuration du Bot Starlink

## 📋 Table des Matières

1. [Prérequis](#prérequis)
2. [Commandes de Configuration](#commandes-de-configuration)
3. [Commandes Utilisateur](#commandes-utilisateur)
4. [Systèmes Automatiques](#systèmes-automatiques)
5. [Guide Étape par Étape](#guide-étape-par-étape)

---

## ⚡ Prérequis

### Permissions Discord
- **Le bot doit avoir le rôle Administrateur sur votre serveur Discord**
- C'est le seul prérequis technique nécessaire

---

## ⚙️ Commandes de Configuration

### 🎫 1. Système de Tickets (`/setup-ticket`)

**À quoi ça sert :** Créer un système de support avec tickets privés

**Paramètres obligatoires :**
- `salon` : Le salon textuel où apparaîtra le bouton "Ouvrir un ticket"
- `categorie` : La catégorie où seront créés les salons de tickets
- `recruteur_1` : Premier rôle autorisé à réclamer les tickets
- `message` : Le message affiché au-dessus du bouton

**Paramètres optionnels :**
- `recruteur_2` : Deuxième rôle autorisé (optionnel)
- `recruteur_3` : Troisième rôle autorisé (optionnel)

**Exemple :**
```
/setup-ticket salon:#support categorie:📋│TICKETS recruteur_1:@Support message:"Cliquez pour ouvrir un ticket"
```

**Ce qui se passe :**
- Le bot envoie un message avec un bouton dans le salon choisi
- Quand quelqu'un clique, un salon privé se crée automatiquement
- Seuls les rôles recruteurs peuvent "réclamer" le ticket
- Le ticket peut être fermé et sera supprimé automatiquement

---

### 📊 2. Système de Logs (`/setup-logs`)

**À quoi ça sert :** Avoir un historique de tout ce qui se passe sur le serveur

**Paramètres obligatoires :**
- `salon` : Le salon textuel où seront envoyés tous les logs

**Exemple :**
```
/setup-logs salon:#logs
```

**Ce qui sera loggé :**
- Messages supprimés/modifiés
- Membres qui rejoignent/quittent
- Sanctions appliquées
- Changements de rôles
- Activité vocale

---

### 🎭 3. Système de Rôles (`/setup-role`)

**À quoi ça sert :** Permettre aux membres de s'attribuer des rôles via la commande `/role`

**Paramètres obligatoires :**
- `salon` : Le salon textuel où la commande `/role` sera autorisée

**Exemple :**
```
/setup-role salon:#roles
```

**Comment ça marche :**
- Une fois configuré, les membres peuvent utiliser `/role` dans ce salon
- Ils peuvent s'attribuer ou se retirer des rôles autorisés

---

### 👋 4. Système d'Accueil (`/setup-welcome`)

**À quoi ça sert :** Accueillir automatiquement les nouveaux membres

**Paramètres obligatoires :**
- `salon` : Le salon textuel où seront envoyés les messages de bienvenue
- `message` : Le message d'accueil personnalisé

**Variable disponible :**
- `{user}` : Sera remplacé par la mention du nouveau membre

**Exemple :**
```
/setup-welcome salon:#bienvenue message:"Bienvenue {user} dans notre serveur !"
```

---

### 🔊 5. Salons Vocaux Temporaires (`/setup-vocal`)

**À quoi ça sert :** Créer des salons vocaux qui se créent/suppriment automatiquement

**Paramètres obligatoires :**
- `salon` : Le salon vocal "déclencheur" (quand quelqu'un s'y connecte, ça crée un nouveau salon)

**Paramètres optionnels :**
- `nom` : Modèle de nom pour les salons créés (défaut: "Salon de {user}")

**Exemple :**
```
/setup-vocal salon:#➕│créer-vocal nom:"Vocal de {user}"
```

**Comment ça marche :**
- Quelqu'un rejoint le salon déclencheur
- Un nouveau salon vocal se crée automatiquement avec le nom personnalisé
- La personne est déplacée dans ce nouveau salon
- Quand le salon devient vide, il se supprime automatiquement

---

### ⚠️ 6. Système d'Avertissements (`/setup-warn`)

**À quoi ça sert :** Définir qui peut donner des avertissements avec `/warn`

**Paramètres obligatoires :**
- `role1` : Premier rôle autorisé à utiliser `/warn`

**Paramètres optionnels :**
- `role2` : Deuxième rôle autorisé (optionnel)
- `role3` : Troisième rôle autorisé (optionnel)

**Exemple :**
```
/setup-warn role1:@Modérateur role2:@Staff
```

### 🏆 7. Système d'Activité (`/setup-activite`)

**À quoi ça sert :** Tracker automatiquement l'activité des membres et faire des rapports

**Paramètres obligatoires :**

- `salon-rapport` : Le salon où seront envoyés les rapports hebdomadaires automatiques
- `role-inactif` : Le rôle qui sera donné automatiquement aux membres inactifs

**Paramètres optionnels :**
- `salon-afk` : Un salon vocal AFK à ignorer du tracking (optionnel)
- `jours-inactivite` : Nombre de jours avant d'être considéré inactif (défaut: 30 jours)

**Exemple :**
```
/setup-activite salon-rapport:#activité role-inactif:@Inactif jours-inactivite:30
```

**Ce qui se passe automatiquement :**
- Le bot compte les points d'activité (messages: +1pt, vocal: +0.1pt/min, réactions: +0.5pt)
- Rapport hebdomadaire automatique tous les dimanches à 20h
- **Retrait automatique** du rôle inactif quand quelqu'un revient (écrit un message ou rejoint un vocal)
- ~~Attribution automatique du rôle inactif~~ : **DÉSACTIVÉ** (à faire manuellement avec `/inactif scan`)

**Commandes utilisateur liées :**
- `/activite` : Voir le classement et ses stats
- `/stats-activite` : Statistiques générales du serveur

---

### 💰 8. Système de Trésorerie (`/setup-tresorerie`)

**À quoi ça sert :** Gérer les finances de votre organisation/guilde

**Cette commande a plusieurs sous-commandes :**

**Pour créer une trésorerie :**
```
/setup-tresorerie creer nom:"Générale" gestionnaire1:@User1 gestionnaire2:@User2
```

**Pour ajouter un gestionnaire :**
```
/setup-tresorerie ajouter nom:"Générale" gestionnaire:@User3
```

**Pour retirer un gestionnaire :**
```
/setup-tresorerie retirer nom:"Générale" gestionnaire:@User3
```

**Comment ça marche :**
- Vous pouvez créer plusieurs trésoreries avec des noms différents
- Seuls les gestionnaires définis peuvent modifier les montants
- Historique automatique de toutes les transactions

**Commandes utilisateur liées :**
- `/tresorerie` : Consulter ou modifier les fonds (si gestionnaire)
- `/tresorery-historique` : Voir l'historique des transactions

---

### 🌌 9. Tracker Star Citizen (`/citizen-tracker`)

**À quoi ça sert :** Voir en temps réel qui joue à Star Citizen sur votre serveur

**Sous-commandes disponibles :**

**Pour activer :**
```
/citizen-tracker enable
```

**Pour désactiver :**
```
/citizen-tracker disable
```

**Pour voir le statut :**
```
/citizen-tracker status
```

**Comment ça marche :**
- Le bot créé automatiquement un salon "🌌-live-citizens"
- Il détecte qui joue à Star Citizen et met à jour le salon toutes les 5 minutes
- Les joueurs sont classés par temps de jeu avec des catégories fun
- Le salon et la config sont supprimés avec `disable`

---

## 🌟 Systèmes Avancés (Plus Complexes)

### 🏅 10. Système de Badges

**À quoi ça sert :** Créer et attribuer des badges de récompense aux membres

**Commandes admin disponibles :**
- `/badge-create` : Créer un nouveau badge
- `/badge-give` : Donner un badge à quelqu'un
- `/badge-remove` : Retirer un badge à quelqu'un
- `/badge-list` : Lister tous les badges existants
- `/badge-del` : Supprimer définitivement un badge

**Commande utilisateur :**
- `/badge` : Voir ses badges ou ceux d'un autre membre

---

### 📅 11. Système d'Événements

**Commandes de configuration :**
- `/setup-event` : Configurer le système d'événements
- `/setup-retour-event` : Configurer le système de feedback
- `/setup-edt` : Configuration des emplois du temps d'événements

**Commandes utilisateur :**
- `/evenement` : Créer un événement
- `/retour-event` : Laisser un feedback sur un événement

---

### 🔧 12. Réponses Automatiques (`/autoresponse`)

**À quoi ça sert :** Le bot répond automatiquement quand quelqu'un écrit certains mots

**Sous-commandes :**
- `/autoresponse add trigger:"mot" response:"réponse"` : Ajouter une réponse auto
- `/autoresponse remove trigger:"mot"` : Supprimer une réponse
- `/autoresponse list` : Voir toutes les réponses configurées
- `/autoresponse clear` : Supprimer toutes les réponses

**Exemple :**
```
/autoresponse add trigger:"salut" response:"Bonjour ! 👋"
```

---

### 🎵 13. Bot Musical

**À quoi ça sert :** Écouter de la musique YouTube dans les salons vocaux

**Commandes disponibles :**
- `/play chanson:"nom de la chanson"` : Jouer une musique
- `/pause` : Mettre en pause
- `/resume` : Reprendre la lecture
- `/skip` : Passer à la chanson suivante
- `/stop` : Arrêter complètement
- `/queue` : Voir la file d'attente

---

### 😴 14. Système AFK

**Commandes utilisateur :**
- `/afk raison:"Je mange"` : Se mettre absent avec une raison
- Retour automatique quand on écrit un message

**Commande admin :**
- `/afk-admin` : Gérer les statuts AFK des membres

**Comment ça marche :**
- Quand quelqu'un vous mentionne, le bot dit que vous êtes AFK
- Vous revenez automatiquement quand vous écrivez un message

## 📋 Commandes Utilisateur (Non-Admin)

### 👤 Commandes d'Information
- `/ping` : Voir la latence du bot
- `/help` : Afficher l'aide générale
- `/moi planning` : Voir son planning personnel d'événements
- `/infos` : Informations du serveur
- `/support` : Contacter le support
- `/embeb salon:#annonces` : Créateur d'embeds personnalisés via MP

### 🎭 Commandes d'Interaction
- `/role` : S'attribuer/retirer des rôles (dans le salon configuré)
- `/afk raison:"motif"` : Se mettre absent
- `/waring membre:@user` : Consulter l'historique des avertissements
- `/unwarn membre:@user` : Retirer un avertissement

### 📊 Commandes de Statistiques
- `/activite` : Voir le classement d'activité
- `/stats-activite` : Statistiques générales du serveur
- `/badge` : Voir ses badges ou ceux d'un autre
- `/tresorerie` : Consulter les trésoreries (ou les modifier si gestionnaire)
- `/tresorery-historique` : Historique des transactions

### 🎵 Commandes Musicales
- `/play chanson:"titre"` : Jouer une musique
- `/pause` : Mettre en pause
- `/resume` : Reprendre
- `/skip` : Passer à la suivante
- `/stop` : Arrêter
- `/queue` : Voir la file d'attente

### 📅 Commandes d'Événements
- `/evenement` : Créer un événement
- `/retour-event` : Laisser un feedback

### 🔍 Commandes de Recherche et Gestion
- `/check-player pseudo:"nomjoueur"` : Vérifier un joueur Star Citizen
- `/inactif scan` : Scanner les membres inactifs
- `/FindRole` : Recherche avancée de membres par rôles

---

## 🔧 Commandes Admin Utilitaires

### 🛠️ Gestion des Membres
- `/warn membre:@user raison:"motif"` : Donner un avertissement
- `/moove salon:@vocal` : Déplacer des membres
- `/clean nombre:10` : Supprimer des messages
- `/afk-admin` : Gérer les statuts AFK

### 📊 Gestion de l'Activité
- `/rapport-activity` : Générer un rapport manuel
- `/whitelist` : Gérer les exemptions d'activité

### 🏅 Gestion des Badges
- `/badge-create` : Créer un badge
- `/badge-give` : Attribuer un badge
- `/badge-remove` : Retirer un badge
- `/badge-list` : Lister tous les badges
- `/badge-del` : Supprimer un badge

---

## ⚙️ Systèmes Automatiques

### 🔄 Tâches qui se Font Toutes Seules
- **Rapports d'activité** : Tous les dimanches à 20h dans le salon configuré
- **Retrait rôle inactif** : Automatique quand quelqu'un revient (message/vocal)
- **Mise à jour Star Citizen** : Toutes les 5 minutes
- **Nettoyage AFK** : Retour automatique quand on écrit
- **Gestion vocaux temporaires** : Création/suppression automatique
- **Réponses automatiques** : Réaction aux mots-clés

### ⚠️ Tâches Manuelles (Désactivées)
- **Attribution rôle inactif** : Utilisez `/inactif scan` pour scanner et attribuer manuellement

### 🎯 Détections Automatiques
- **Messages supprimés/modifiés** → Loggés
- **Membres qui arrivent/partent** → Message d'accueil/logs
- **Sanctions appliquées** → Loggés et timeout automatique
- **Activité des membres** → Points comptés automatiquement

---

## 📝 Guide Étape par Étape

### 🚀 Configuration Minimale (Pour Commencer)

1. **Inviter le bot** avec le rôle **Administrateur**
2. **Configurer les logs** :
   ```
   /setup-logs salon:#logs
   ```
3. **Configurer l'accueil** :
   ```
   /setup-welcome salon:#bienvenue message:"Bienvenue {user} !"
   ```

### 🌟 Configuration Recommandée (Serveur Actif)

4. **Système de tickets** :
   ```
   /setup-ticket salon:#support categorie:📋│TICKETS recruteur_1:@Support message:"Cliquez pour de l'aide"
   ```
5. **Système d'avertissements** :
   ```
   /setup-warn role1:@Modérateur
   ```
6. **Système d'activité** :
   ```
   /setup-activite salon-rapport:#activité role-inactif:@Inactif
   ```

### 🎯 Configuration Avancée (Serveur Gaming/Organisation)

7. **Vocaux temporaires** :
   ```
   /setup-vocal salon:#créer-vocal nom:"Vocal de {user}"
   ```
8. **Star Citizen tracker** :
   ```
   /citizen-tracker enable
   ```
9. **Trésorerie** :
   ```
   /setup-tresorerie creer nom:"Principale" gestionnaire1:@TonPseudo
   ```
10. **Réponses automatiques** :
    ```
    /autoresponse add trigger:"salut" response:"Bonjour ! 👋"
    ```

---

## 🆘 FAQ et Dépannage

### ❓ Questions Fréquentes

**Q: Le bot ne répond pas à mes commandes ?**
R: Vérifiez qu'il a bien le rôle Administrateur sur votre serveur.

**Q: Le système d'activité ne fonctionne pas ?**
R: Vérifiez que le bot peut envoyer des messages dans le salon de rapport configuré.

**Q: Les vocaux temporaires ne se créent pas ?**
R: Vérifiez que le bot a les permissions "Gérer les salons" et "Déplacer des membres".

### 🔧 Résolution de Problèmes

**Bot en ligne mais ne répond pas :**
- Vérifier les permissions Administrateur

**Erreurs de configuration :**
- Recommencer la commande setup avec les bons paramètres
- Vérifier que les salons/rôles mentionnés existent bien

**Fonctionnalités qui ne marchent plus :**
- Vérifier que les salons configurés existent toujours
- Vérifier que les rôles configurés existent toujours

---

## ✅ Checklist de Configuration

### 🏁 Configuration de Base (Obligatoire)
- [ ] Bot invité avec rôle **Administrateur**
- [ ] `/setup-logs salon:#logs` configuré
- [ ] `/setup-welcome salon:#bienvenue message:"..."` configuré

### 🌟 Configuration Standard (Recommandée)
- [ ] `/setup-ticket` configuré pour le support
- [ ] `/setup-warn` configuré pour la modération
- [ ] `/setup-role salon:#roles` configuré
- [ ] `/setup-activite` configuré

### 🎯 Configuration Complète (Optionnelle)
- [ ] `/setup-vocal` pour les salons temporaires
- [ ] `/citizen-tracker enable` pour Star Citizen
- [ ] `/setup-tresorerie creer` pour les finances
- [ ] `/autoresponse` pour les réponses auto
- [ ] Badges créés avec `/badge-create`

---

**🎉 Votre bot Starlink est maintenant configuré ! Il va dynamiser votre serveur Discord avec tous ces systèmes automatiques.**

> 💡 **Conseil :** Commencez par la configuration de base, puis ajoutez progressivement les autres systèmes selon vos besoins.