Projet E-commerce
Stack

Frontend : Next.js 15, React 19, TypeScript
Style : Tailwind CSS, Framer Motion
Backend : Firebase (Firestore, Auth, Storage)
Paiement : Stripe (pas encore intégré)
Déploiement : Firebase App Hosting

Structure
app/
  page.tsx                → accueil
  produits/page.tsx       → catalogue produits
  produits/[slug]/page.tsx → page produit individuelle
  panier/page.tsx         → panier
  auth/login/page.tsx     → connexion utilisateur
  api/                    → routes API serveur

components/
  ui/                     → composants génériques (bouton, card, input...)
  shop/                   → composants métier (ProductCard, Navbar, Cart...)

lib/
  firebase.ts             → connexion Firebase côté navigateur
  firebase-admin.ts       → connexion Firebase côté serveur uniquement

types/index.ts            → types TypeScript (Product, CartItem, UserProfile)
apphosting.yaml           → config Firebase App Hosting
Types principaux
typescriptProduct = {
  id, nom, slug, description,
  prix (en centimes),
  images (URLs Firebase Storage),
  stock, categorie, actif
}

CartItem = { produit: Product, quantite: number }

UserProfile = { uid, email, nom }
Règles importantes

Les Server Components fetchent les données directement via firebase-admin
Les Client Components utilisent lib/firebase.ts (jamais firebase-admin)
Les fichiers "use client" uniquement si nécessaire (animations, état local, events)
Les prix sont toujours en centimes dans la DB (ex: 2990 = 29,90€)
Les images sont stockées dans Firebase Storage
Ne jamais exposer les variables FIREBASE_ADMIN_* côté client
Toujours typer avec les types de types/index.ts

Conventions

Composants : PascalCase (ProductCard.tsx)
Fonctions utilitaires : camelCase
Pages : page.tsx dans le dossier correspondant
Langue : français pour les variables métier, anglais pour le code technique

Commandes

Développement : npm run dev
Build : npm run build