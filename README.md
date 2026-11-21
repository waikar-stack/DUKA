# Duka Stock Manager

Inventory and point-of-sale for a small fast-moving-goods shop. The site is hosted on **GitHub Pages**; data and Google sign-in run on **Firebase**. Everything is set up in the browser, with nothing to install.

| File | What it is |
|---|---|
| `index.html` | The whole app |
| `firebase-config.js` | Your Firebase web config (paste it in) |
| `firestore.rules` | Security rules (copy them into the Firebase console) |
| `manifest.json`, `icon.svg` | Lets phones "Add to Home screen" |
| `.nojekyll` | Tells GitHub Pages to serve the files as they are |

## A. Firebase (data + sign-in)

1. Go to https://console.firebase.google.com and click **Add project** (for example `duka-stock`).
2. **Firestore Database** › **Create database** › **Production mode** › pick a location (for Kenya: `africa-south1` or `europe-west1`).
3. Open the **Rules** tab in Firestore. Delete what's there, paste the contents of `firestore.rules`, change `owner@gmail.com` to **your Google email (lowercase)**, then click **Publish**.
4. **Authentication** › **Get started** › **Sign-in method** › **Google** › Enable › Save.
5. **Project settings** (gear icon) › **Your apps** › **Web `</>`** › register the app. Keep the `firebaseConfig` values open; you need them in step B3.

## B. GitHub (hosting)

1. On github.com, click **New repository** › name it `duka-stock` › **Public** › Create. (GitHub Pages on a free account needs a public repo. The data stays private in Firebase; the code holds no secrets.)
2. Click **uploading an existing file**. Drag in **all the files from this folder**, including `.nojekyll`, then **Commit changes**.
   - On Windows and Mac, `.nojekyll` is hidden. If it doesn't upload, use **Add file › Create new file**, name it `.nojekyll`, leave it empty and commit.
3. Open `firebase-config.js` in the repo › pencil icon (Edit) › replace the placeholder values with your `firebaseConfig` › **Commit changes**.
4. **Settings** › **Pages** › Source: **Deploy from a branch** › Branch: `main`, folder `/ (root)` › **Save**. After a minute the address appears: `https://<your-username>.github.io/duka-stock/`.

## C. Connect the two

In Firebase › **Authentication** › **Settings** › **Authorized domains**, click **Add domain** and enter `<your-username>.github.io`.

Open your site and sign in with the owner email. Then go to **Settings › Staff** to add your staff's Google emails.

## Updating the app later

Upload the new `index.html` to the repo (Add file › Upload files) and commit. GitHub Pages updates in about a minute. Your data in Firebase is not touched.

## Good to know

- **Offline:** sales and stock changes save on the device without internet and sync when it's back.
- **Example data:** Settings › Example data › Load, to explore. Clear removes only the examples.
- **Demo without Firebase:** add `?demo` to the address. Nothing is saved.
- **Cost:** the free Firebase Spark plan (50,000 reads and 20,000 writes per day) is plenty for a small shop. GitHub Pages is free.
- **Security:** the values in `firebase-config.js` are public identifiers, not passwords. Only the owner email and approved staff can read or write data, because of the rules you published in step A3.
