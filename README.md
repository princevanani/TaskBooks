# 90-Day Outreach Tracker: GitHub Pages + Firebase (synced)

Files:

- `index.html`: the tracker
- `firebase-config.js`: your Firebase project settings (you fill this in)
- `firestore.rules`: the security rules to paste into Firebase

Your tasks, contacts and daily logs are saved in your own Firebase project and show up on every device where you sign in. The free Spark plan is plenty for this.

## 1. Create the Firebase project (about 10 minutes)

1. Go to https://console.firebase.google.com and sign in with a Google account.
2. **Create a project**, give it a name (for example `outreach-tracker`), and turn Google Analytics off.
3. In the project, click the web icon `</>` (Add app > Web), give it a nickname, and **skip** Firebase Hosting. Copy the `firebaseConfig` values it shows.
4. Open `firebase-config.js` and replace each `PASTE_...` value with your values. Leave `loginDomain` as it is.

## 2. Turn on sign-in and create your user

1. Left menu: **Build > Authentication > Get started**.
2. **Sign-in method**: enable **Email/Password** (leave "Email link" off). Save.
3. **Users > Add user**:
   - Email: `princevanani@outreach-tracker.app` (your username, then `@`, then the `loginDomain` from the config)
   - Password: choose a strong password you don't use anywhere else.
4. Copy the **User UID** that appears in the users list. You need it in the next step.
5. In Authentication > Settings > User actions, if you see **Enable create (sign-up)**, turn it off so nobody else can create accounts.

You then sign in on the site with the username `princevanani` and that password.

## 3. Create the database and lock it

1. Left menu: **Build > Firestore Database > Create database**.
2. Choose **Production mode** and a nearby region (for example `asia-south1` Mumbai). The region can't be changed later.
3. Open the **Rules** tab, replace everything with the contents of `firestore.rules`, put your User UID in place of `PASTE_YOUR_USER_UID`, and click **Publish**.

## 4. Publish on GitHub Pages

1. Create a GitHub repository (for example `outreach-tracker`).
2. Upload `index.html` and `firebase-config.js` to the main branch.
3. **Settings > Pages > Deploy from a branch > main / root > Save**.
4. After a minute, open `https://princevanani.github.io/outreach-tracker/` (use your repository name) and sign in.

If sign-in fails with an "unauthorized domain" message, go to Authentication > Settings > Authorized domains and add `princevanani.github.io`.

## How it behaves

- Changes save within a second and appear on your other devices within a few seconds.
- The page keeps a copy on each device, so it still opens when your connection is poor. Changes sync when you're back online.
- **Progress > Download backup** saves everything to a file. **Restore backup** adds the items from a backup file back into your account.

## Security notes

- The settings in `firebase-config.js` are public by design. What protects your data is the sign-in plus the Firestore rules, which only allow your user ID. Do not skip step 3.
- Use a strong, unique password, and don't share it in chats or documents.
- Optional hardening: in Google Cloud Console > APIs & Services > Credentials, restrict the browser API key to the HTTP referrer `https://princevanani.github.io/*`.
- Don't put sensitive data (bank details, client secrets) in the tracker.
