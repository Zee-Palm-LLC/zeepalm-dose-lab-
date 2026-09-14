# Deploy steps

Everything below is run by you. Nothing here has been executed.

## 1. Confirm the right GitHub account

    gh auth status

If it is not `hiba0900`:

    gh auth switch --user hiba0900     # if already logged in
    gh auth login                      # otherwise

## 2. First commit

    cd /Users/apple/zeepalm-dose-lab
    git init -b main
    git add .
    git commit -m "$(cat <<'MSG'
Dose Lab: see what a supplement label actually contains

An interactive 3D study of supplement dosing. Each ingredient is a vial
filled to the fraction of its own effective dose that is present, with an
etched ring at one full dose and a red column showing the shortfall.

21 CFR 101.36 requires proprietary blend ingredients to be listed in
descending order by weight, so the kth ingredient is at most total/k.
Where that ceiling falls below the researched dose, the shortfall is
arithmetic rather than opinion, and the panel shows the derivation.

Adds a formula-level mass check: one effective dose of every active
compared against the declared weight and the serving size.

Co-Authored-By: Claude Opus 5 <noreply@anthropic.com>
MSG
)"

## 3. Create the repo under the Zee Palm org and push

    gh repo create Zee-Palm-LLC/zeepalm-dose-lab \
      --public \
      --source=. \
      --remote=origin \
      --push \
      --description "See what a supplement label actually contains. An interactive 3D study from Zee Palm Labs."

If the org blocks repo creation for your account, create it empty in the
GitHub UI under Zee-Palm-LLC, then:

    git remote add origin git@github.com:Zee-Palm-LLC/zeepalm-dose-lab.git
    git push -u origin main

## 4. Deploy to Vercel

    npm i -g vercel        # only if you don't have it
    cd /Users/apple/zeepalm-dose-lab
    vercel                 # preview build, answer the prompts
    vercel --prod          # production

Static site, no build step and no framework — accept the defaults.
Output directory: leave blank (repo root). Build command: leave blank.

Alternative: import the GitHub repo at vercel.com/new, which gives you
automatic deploys on every push.

## 5. Point the metadata at the live URL

Four placeholders. With your real domain:

    cd /Users/apple/zeepalm-dose-lab
    sed -i '' 's|REPLACE-WITH-LIVE-URL|zeepalm-dose-lab.vercel.app|g' index.html
    git commit -am "Point canonical and social metadata at the live URL

Co-Authored-By: Claude Opus 5 <noreply@anthropic.com>"
    git push
    vercel --prod

## 6. Social preview image

`og-image.png` is referenced but does not exist yet, so LinkedIn and
Facebook previews will be blank until you add it.

1. Open the live site in a 1512-wide window
2. Let the ▶ tour run to the point where L-Citrulline is selected
3. Screenshot, crop to exactly 1200 x 630
4. Save as `og-image.png` in the repo root, commit, push

## 7. Check it

    curl -sI https://YOUR-URL/ | head -1
    curl -s https://YOUR-URL/ | grep -c 'og:image'

Then paste the URL into the LinkedIn Post Inspector to refresh the preview cache.
