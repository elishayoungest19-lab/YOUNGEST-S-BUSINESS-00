# Mise en ligne des actualités — YOUNGEST’S BUSINESS V5.1

Cette version utilise **Firebase Authentication + Cloud Firestore uniquement**. Elle n’utilise PAS Cloud Storage, donc vous n’avez pas besoin d’activer le forfait Blaze pour publier les actualités et leurs petites images.

## 1. Firebase

1. Créer le projet Firebase.
2. Ajouter l’application Web.
3. Copier la configuration Web dans `firebase-config.js`.
4. Activer **Authentication → Sign-in method → Email/Password**.
5. Créer votre compte administrateur dans **Authentication → Users**.
6. Créer **Cloud Firestore** en mode Standard et en mode production.

## 2. Sécuriser Firestore

Dans **Firestore → Règles**, utiliser le contenu de `firestore.rules` et remplacer l’UID administrateur si nécessaire.

Les règles prévues sont :
- le public peut lire uniquement les documents `news` dont `published` vaut `true` ;
- seul l’UID administrateur peut créer, modifier et supprimer les actualités.

## 3. Images sans Storage

Dans `admin.html`, une image choisie sur le téléphone est automatiquement redimensionnée et compressée dans le navigateur avant d’être enregistrée dans le document Firestore.

Limites pratiques de cette version : les images sont réduites à environ 1000 px sur leur plus grand côté et à une taille de données raisonnable pour Firestore. Pour un très grand volume d’images, Cloud Storage serait préférable, mais il nécessite aujourd’hui le forfait Blaze.

## 4. Tester

1. Ouvrir `admin.html`.
2. Se connecter avec le compte administrateur.
3. Renseigner titre, date et contenu.
4. Choisir éventuellement une image.
5. Appuyer sur **Publier pour tous**.
6. Ouvrir `index.html` dans un autre navigateur/appareil : l’actualité doit apparaître.

## 5. Important

Ne pas activer Firebase Storage uniquement pour cette version. Votre projet peut rester sur Spark tant que vous restez dans les quotas gratuits de Firestore. Firebase indique actuellement 50 000 lectures/jour, 20 000 écritures/jour, 20 000 suppressions/jour, 1 Gio de données stockées et 10 Gio/mois de transfert sortant pour la base gratuite.
