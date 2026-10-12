# All Zone Bd — Firebase starter (free-tier starting point)

## What is included
- Mobile-friendly storefront
- Product list, search and cart
- Admin email/password login
- Admin can add/delete products and update order statuses
- Customer checkout writes an order to Firestore, then opens WhatsApp with the order details
- Firestore rules: public product reads; only the configured admin email can manage products and read/manage orders

## Important limitations
- This is a starter, not yet a launched or audited production shop.
- Firebase project/configuration must be created by the shop owner.
- Sample products are visual demos; add only products you can actually source.
- WhatsApp opens after a successful database write. If the customer closes WhatsApp, the order still exists in Firestore.
- Public checkout can be abused by bots. Before public launch, add App Check / rate limiting / server-side validation and test security rules. Never use “test mode” rules in production.
- Keep supplier cost, profit margin, customer private data and admin-only data out of public product documents.
- Do not collect card details. COD only in this starter; a real bKash/Nagad gateway requires an approved merchant/payment integration.
- Admin email is hard-coded in both the config and rules. Keep the email identical and verified. Only use this account for the shop admin.
- Firebase client config is not a secret; Firestore Security Rules are what protect data. Never put service-account keys in public files.

## Setup steps (phone-friendly)
1. Open https://console.firebase.google.com/ and sign in with the Google account you want to own the shop.
2. Create project `All Zone Bd` (project ID must be globally unique; e.g. `all-zone-bd-shop-xxxx`). For initial testing, Analytics can be skipped.
3. In Project settings > General > Your apps, add a Web app named `All Zone Bd`.
4. Copy the Firebase web config into `public/firebase-config.js`, replacing all `PASTE_...` placeholders.
5. In Build > Authentication > Get started > Sign-in method, enable Email/Password.
6. In Authentication > Users, add/create the admin user with `sukenchakma791@gmail.com`, set a strong password, and verify the email if prompted. Do not share that password.
7. In Build > Firestore Database, create a database. Do not leave test mode open. Open Rules and publish the contents of `firestore.rules`.
8. For hosting, easiest deployment uses Firebase CLI on a computer or Firebase Cloud Shell:
   - Install/use Firebase CLI: https://firebase.google.com/docs/cli
   - Put the `public` folder and `firestore.rules` in a project directory.
   - Run `firebase login`
   - Run `firebase init hosting firestore` and choose the project you created. Set Hosting public directory to `public`, configure as single-page app: No.
   - Ensure firebase.json has hosting.public = "public" and firestore.rules = "firestore.rules".
   - Run `firebase deploy --only hosting,firestore:rules`
9. Open the Hosting URL, login from Admin Login, add real products, then place a test order with your own details.
10. Check the order in Admin Panel and check the WhatsApp message opened on the phone.

## Firestore collections
- `products`: name, price, icon, category, active, createdAt
- `orders`: name, phone, address, payment, items[], total, status, createdAt

## WhatsApp
The provided WhatsApp number is formatted in international format `8801838159073` (Bangladesh +880, remove the leading 0). Update it in `public/firebase-config.js` if needed.
