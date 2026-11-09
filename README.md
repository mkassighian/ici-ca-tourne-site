Ce dépôt publie les pages légales de l'appli Ici ça tourne.
Les sources vivent dans le dépôt privé de l'appli (`site/`).
L'action `keepalive` maintient le projet Supabase éveillé.

## Republier après une modification

Depuis le dépôt de l'appli (`gh` doit avoir le droit `workflow` : `gh auth refresh -h github.com -s workflow`) :

```bash
tmp=$(mktemp -d) && gh repo clone mkassighian/ici-ca-tourne-site "$tmp" -- -q
rsync -a --delete --exclude .git site/ "$tmp"/
git -C "$tmp" add -A && git -C "$tmp" commit -m "Mise à jour des pages" && git -C "$tmp" push
```

GitHub Pages republie en une à deux minutes : https://mkassighian.github.io/ici-ca-tourne-site/

Secrets du dépôt public (pour `keepalive`) : `SUPABASE_URL` et `SUPABASE_ANON_KEY` (clé publique de l'appli).
