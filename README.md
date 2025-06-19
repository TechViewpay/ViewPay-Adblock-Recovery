# Documentation d'Intégration ViewPay GFC

## Vue d'ensemble

L'intégration ViewPay Google Adblock Recovery (anciennement Google Funding Choices) ajoute un bouton "Regarder une pub" aux popups de consentement Google Adblock Recovery existants, permettant aux utilisateurs d'obtenir des sessions de navigation sans publicité en regardant des publicités vidéo.

## Installation

Ajoutez simplement **un seul script** à votre page :

```html
<script src="//cdn.jokerly.com/scripts/ViewPay_GFC_standalone.js?site_id=VOTRE_SITE_ID&pub_id=VOTRE_PUB_ID&video_duration=1800&debug_mode=false" defer></script>
```

**C'est tout !** Le script s'occupe automatiquement de :
- Charger les dépendances ViewPay requises
- Créer les éléments HTML nécessaires
- Initialiser l'intégration

## Paramètres de Configuration

| Paramètre | Obligatoire | Description | Exemple |
|-----------|-------------|-------------|---------|
| `site_id` | **Oui** | Votre identifiant de site ViewPay | `site_id=1234567890` |
| `video_duration` | Non | Durée de la session sans Adblock Recovery en secondes | `video_duration=1800` (30 min) |
| `debug_mode` | Non | Activer les logs de la console | `debug_mode=true` |
| `hide_close` | Non | Activer l'option pour cacher la croix quand une publicité est disponible | `hide_close=false` |

### Notes sur les paramètres

- **site_id** : Fourni par ViewPay lors de la configuration de votre compte
- **video_duration** : Valeur par défaut de 60 secondes. Valeurs < 10000 considérées comme des secondes, sinon millisecondes
- **debug_mode** : Valeur par défaut `false`. Les valeurs acceptées sont `true|false` ou `1|0`. À désactiver en production (`debug_mode=false`)
- **hide_close** : Valeur par défaut `true`. Les valeurs acceptées sont `true|false`ou `1|0`

## Comment ça fonctionne

1. **Visite utilisateur** : Le popup Google Adblock Recovery apparaît (géré par l'éditeur)
2. **Injection automatique** : Le script injecte automatiquement les dépendances et éléments HTML
3. **Ajout du bouton ViewPay** : L'intégration ajoute le bouton "Regarder une pub" au popup
4. **Visionnage de la pub** : Cliquer sur le bouton affiche la publicité vidéo ViewPay
5. **Session sans Adblock Recovery** : Après avoir terminé la vidéo, l'utilisateur obtient une navigation sans blocage pendant la durée configurée
6. **Gestion des sessions** : Les futurs popups Adblock Recovery sont supprimés pendant les sessions sans pub actives

## Prérequis

- Google Adblock Recovery doit être configuré par l'éditeur
- Compte ViewPay et configuration du site
- Navigateur moderne avec support localStorage

## Exemple d'Intégration Complète

```html
<!DOCTYPE html>
<html>
<head>
  <title>Mon Site</title>
  
  <!-- Configuration Google Funding Choices existante -->
  <script src="https://fundingchoicesmessages.google.com/i/pub-VOTRE_PUB_ID?ers=1"></script>
  
  <!-- ViewPay GFC - UNE SEULE LIGNE NÉCESSAIRE -->
  <script src="//cdn.jokerly.com/scripts/ViewPay_GFC_standalone.js?site_id=1234&pub_id=5678&video_duration=1800&debug_mode=false" defer></script>
</head>
<body>
  <!-- Votre contenu -->
  <h1>Bienvenue sur mon site</h1>
  <p>Contenu de votre site...</p>
  
  <!-- Les éléments ViewPay sont maintenant créés automatiquement -->
</body>
</html>
```

## Debugging et Support

### Mode Debug

Activez le mode debug pour diagnostiquer les problèmes :
```html
<script src="//cdn.jokerly.com/scripts/ViewPay_GFC_standalone.js?site_id=1234&pub_id=5678&debug_mode=true" defer></script>
```

Les logs apparaîtront dans la console du navigateur avec le préfixe `[ViewPay GFC]`.

### Messages de Debug Typiques

- `Configuration loaded from script URL` : Confirmation du chargement des paramètres
- `ViewPay script loaded successfully` : Dépendance chargée avec succès
- `ViewPay HTML elements injected successfully` : Éléments HTML créés
- `Active video session detected` : Session sans Adblock Recovery active
- `Video button activated successfully` : Bouton prêt à l'utilisation

## Notes Importantes

- L'intégration ajoute uniquement la fonctionnalité ViewPay aux popups GFC existants
- Les éditeurs conservent le contrôle total sur quand et comment les popups GFC apparaissent  
- Les sessions sans Adblock Recovery sont stockées dans le localStorage du navigateur
- Le mode debug doit être désactivé en production (`debug_mode=false`)

## Support Technique

Pour tout problème d'intégration :
1. Vérifiez que vos paramètres `site_id` et `pub_id` sont corrects
2. Activez le mode debug pour voir les logs détaillés
3. Assurez-vous que Google Adblock Recovery fonctionne correctement avant d'ajouter ViewPay
4. Contactez le support ViewPay avec les logs de debug si nécessaire
