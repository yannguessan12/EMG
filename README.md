# EMG Portail — APK avec notifications

## 1. GitHub
1. Créez un dépôt, envoyez-y tout ce dossier (branche `main`).
2. Settings > Pages > Source : **GitHub Actions**.

## 2. Firebase
1. console.firebase.google.com > nouveau projet > ajouter une app **Android**, nom de package : `com.excellencemedical.portail`.
2. Téléchargez `google-services.json`.
3. Paramètres du projet > Comptes de service > **Générer une clé privée** (fichier JSON, pour Supabase).

## 3. Secrets GitHub (Settings > Secrets and variables > Actions)
- `GOOGLE_SERVICES_JSON` : contenu complet de google-services.json
- Pour un APK signé (facultatif, sinon APK de test) : `KEYSTORE_BASE64`, `KEYSTORE_PASSWORD`, `KEY_ALIAS`

## 4. Supabase
1. SQL Editor : exécutez `supabase/notifications.sql`.
2. Déployez la fonction `envoyer-notification` et définissez ses secrets :
   - `FCM_SERVICE_ACCOUNT` : contenu du JSON de clé privée Firebase
   - `PUSH_SECRET` : un mot de passe long de votre choix

## 5. Récupérer l'APK
Onglet **Actions** > « Compiler l'APK » > Artifacts > `emg-portail-apk`.

## Tester l'envoi
curl -X POST https://<projet>.supabase.co/functions/v1/envoyer-notification \
  -H "x-push-secret: <PUSH_SECRET>" -H "Content-Type: application/json" \
  -d '{"cible":"tous","titre":"Test","corps":"Bonjour","page":"accueil"}'
