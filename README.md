# Redirection de c-hypnose.net vers hypnose-roulleau.fr

Ce dépôt ne contient pas de site : chaque ancienne adresse de c-hypnose.net renvoie immédiatement vers la page équivalente de **https://hypnose-roulleau.fr** (redirection *meta refresh* à 0 seconde, lien *canonical*, redirection JavaScript de secours et lien « Le site a déménagé »).

| Ancienne adresse | Nouvelle adresse |
|---|---|
| `/` | https://hypnose-roulleau.fr/ |
| `/l-hypnose-c-est-quoi` | https://hypnose-roulleau.fr/l-hypnose-c-est-quoi.html |
| `/indications` | https://hypnose-roulleau.fr/indications.html |
| `/deroulement-d-une-seance` | https://hypnose-roulleau.fr/deroulement-d-une-seance.html |
| `/qui-suis-je` | https://hypnose-roulleau.fr/qui-suis-je.html |
| `/contact` | https://hypnose-roulleau.fr/contact.html |
| toute autre adresse | https://hypnose-roulleau.fr/ (page `404.html`) |

Chaque ancienne adresse a deux fichiers identiques : le dossier `contact/` (avec `index.html`) répond à `/contact` et `/contact/` ; le fichier `contact.html` répond à `/contact.html` et sert de secours pour `/contact`.

---

## 1. Mise en ligne

1. Sur GitHub : **New repository** → nom `redirection-c-hypnose` → **Public** → **Create repository**.
2. Cliquez sur **uploading an existing file**, puis glissez **le contenu** du dossier (dossiers compris, pas le dossier lui-même) → **Commit changes**.
3. Vérifiez que `.nojekyll` apparaît dans la liste des fichiers du dépôt. Sur Mac, ce fichier est masqué et n'est pas glissé : dans ce cas, **Add file → Create new file**, nom `.nojekyll`, contenu vide → **Commit changes**.
4. **Settings → Pages** : **Deploy from a branch**, branche **main**, dossier **/(root)** → **Save**.
5. Une minute plus tard, testez https://squelinki.github.io/redirection-c-hypnose/contact : vous devez arriver sur la page « Tarifs & contact » du nouveau site. Essayez aussi `…/contact/` et `…/nimporte-quoi` (→ accueil).

## 2. Brancher c-hypnose.net

L'ancien site était publié sur **www**.c-hypnose.net : c'est cette adresse qu'il faut déclarer.

1. **Settings → Pages → Custom domain** : saisissez `www.c-hypnose.net` → **Save**. GitHub ajoute alors lui-même un fichier `CNAME` au dépôt : c'est normal, ne le supprimez pas.
2. Dans la **zone DNS de c-hypnose.net** (chez Wix si le domaine y a été acheté, sinon chez son registraire), remplacez les enregistrements qui pointent vers Wix :
   - `www` : un enregistrement **CNAME** vers `squelinki.github.io.` ;
   - `c-hypnose.net` (sans www) : 4 enregistrements **A** : `185.199.108.153` · `185.199.109.153` · `185.199.110.153` · `185.199.111.153` ;
   - ne touchez pas aux autres enregistrements (MX pour les e-mails, TXT de vérification…).

   GitHub renverra alors aussi `c-hypnose.net` (sans www) vers `www.c-hypnose.net`, puis vers le nouveau site.
3. Quand **Settings → Pages** affiche « DNS check successful » (de quelques minutes à 24 h), cochez **Enforce HTTPS** : les anciens liens sont en `https://`.
4. Testez : https://www.c-hypnose.net/contact, https://c-hypnose.net/indications/, http://www.c-hypnose.net/.
5. Ensuite seulement, résiliez l'abonnement du site Wix — **pas le nom de domaine** : renouvelez c-hypnose.net au moins un an, idéalement plus. Sans lui, les redirections s'arrêtent.
6. (Conseillé) Dans les paramètres de votre **compte** GitHub (Settings → Pages), ajoutez et vérifiez `c-hypnose.net` : personne d'autre ne pourra l'utiliser sur GitHub.

## 3. Google

- Google traite une redirection *meta refresh* à 0 seconde comme une redirection permanente : les anciennes pages céderont peu à peu leur place aux nouvelles dans les résultats.
- L'outil **Changement d'adresse** de la Search Console demande une vraie redirection « 301 », que GitHub Pages ne sait pas faire : il refusera probablement. Ce n'est pas bloquant.
- Les adresses inconnues (page `404.html`) renvoient les visiteurs vers l'accueil, mais Google les traite comme des pages en erreur et les oublie : c'est normal. Pour cette raison, la page 404 n'a pas de lien *canonical*.
- Pas de `robots.txt` : son absence autorise tout.
- Si un jour c-hypnose.net passe chez un registraire qui propose une « redirection permanente 301 » en conservant le chemin, ou derrière Cloudflare (gratuit), c'est encore mieux, et ce dépôt deviendra inutile.

## 4. Ajouter une ancienne adresse

Copiez le dossier `contact/` et le fichier `contact.html`, renommez-les avec l'ancienne adresse (par exemple `tarifs/` et `tarifs.html`), puis, dans chacun des deux fichiers, remplacez partout `hypnose-roulleau.fr/contact.html` par la nouvelle destination (Rechercher/Remplacer).
