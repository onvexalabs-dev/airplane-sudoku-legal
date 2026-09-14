# Publishing the legal pages on GitHub Pages

These pages are **generated** from the legal texts inside the app:

```
cd sudoku-tools
python make_legal_site.py
```

Do not edit the HTML by hand. Edit `app/src/main/res/raw/legal_*.txt` and
`res/raw-de/legal_*.txt`, then regenerate. Google compares the hosted policy
with the in-app one if anyone complains, and generating one from the other is
the only reliable way to keep them identical.

---

## Already filled in

The pages carry the real publisher details and there are no placeholders left.
Nothing needs editing before you push.

| | |
|---|---|
| Publisher | Manfred Uschan |
| Address | Unterneuberg 136, 8225 Pöllau, Austria |
| Contact | onvexalabs@gmail.com |
| Governing law | Austria |
| Audience | General (not Designed for Families) |
| Last updated | 14 September 2026 |

The imprint states explicitly that the publisher is a private individual with
no commercial register entry, VAT number or trade authority, and cites
ECG section 5 and MedienG section 25. That is the correct shape for a private
person in Austria; a business would need the register lines instead.

**If any of this changes**, edit the source texts in
`app/src/main/res/raw/` and `res/raw-de/`, regenerate, and push. Do not edit
the HTML — it is overwritten on every run.

Update the date line whenever the content changes: a privacy policy whose
"last updated" date predates a feature that collects data looks careless.

## Why a separate repository

Your app repo is **private**. GitHub Pages only serves from a private
repository on a paid plan. A public repo containing four legal documents is
the simplest route, and it keeps your source closed.

---

## Step by step

### 1. Create the public repository

github.com/new, on the `onvexalabs-dev` account.

- Name: `airplane-sudoku-legal`
- **Public**
- Do not add a README, .gitignore or licence

### 2. Push the site

```powershell
cd E:\AND_AirplaneSudoku\legal-site
git init
git add -A
git commit -m "Legal pages for Airplane Sudoku"
git branch -M main
git remote add origin https://github.com/onvexalabs-dev/airplane-sudoku-legal.git
git push -u origin main
```

This is a second, separate repository. Your app repo is untouched.

### 3. Turn Pages on

Repository → **Settings** → **Pages** (left sidebar).

- **Source:** *Deploy from a branch*
- **Branch:** `main`, folder `/ (root)`
- **Save**

Give it one to two minutes. The page then shows the live URL:

```
https://onvexalabs-dev.github.io/airplane-sudoku-legal/
```

Refresh the Settings → Pages screen until the URL appears with a green tick.
The first build is the slow one; later pushes go live in seconds.

### 4. Check it

Open the URL. You should see the landing page with English and German links.
Click through all eight pages. Check on a phone too — the pages are responsive
and follow the system dark mode.

### 5. Put the URL in Play Console

The one Google needs is the **privacy policy** page, not the landing page:

```
https://onvexalabs-dev.github.io/airplane-sudoku-legal/en/privacy.html
```

Paste it in two places:

- **Policy → App content → Privacy policy**
- The **Data safety** form, which asks for it separately

The German version lives at `/de/privacy.html`. Play takes one URL; English is
the right choice for the Console field, and the page links to the German one.

---

## Updating later

```powershell
cd E:\AND_AirplaneSudoku\sudoku-tools
python make_legal_site.py
cd ..\legal-site
git add -A
git commit -m "Update legal texts"
git push
```

Live within a minute. **Update the date line whenever the content changes** —
a privacy policy whose "last updated" date predates a feature that collects
data looks careless.

---

## If the URL 404s

- Pages can take a couple of minutes on the first build.
- Check Settings → Pages shows branch `main` and folder `/ (root)`.
- Check `index.html` is at the **root** of the repo, not inside a
  `legal-site/` folder. If you pushed the parent directory by mistake, the URL
  would be `.../airplane-sudoku-legal/legal-site/`.
- The repository must be **Public**. A private repo on a free plan shows Pages
  as unavailable.
