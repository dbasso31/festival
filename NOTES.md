# CONTREBANDE.S Festival — notes de projet

Page unique reprenant l'affiche `cover.png`, avec les photos qui défilent derrière l'affiche rouge fixe.

- **Site en ligne** : https://dbasso31.github.io/festival/ (GitHub Pages, branche `main`, racine)
- **Dépôt** : https://github.com/dbasso31/festival (public)
- **Dernière mise à jour** : 2026-11-20

## Structure

| Fichier | Rôle |
|---|---|
| `index.html` | Toute la page (HTML + CSS + un petit script) |
| `img/web/img1-5.jpg` | Photos optimisées (2000 px de large, ~1,5 Mo), utilisées par la page |
| `img/img1-5.jpg` | Originaux (25–49 Mo) — **ignorés par git** |
| `fonts/MuotoTrialVAR.ttf` | Police Muoto variable (axes `wght` 100–900, `wdth` 25–150) |
| `logo/logoBLACK.svg` | Logo source (inliné dans `index.html`, en `currentColor`) |
| `cover.png` | Affiche de référence — **ignorée par git** |
| `.claude/launch.json` | Config d'un serveur local de test (ignoré par git) |

## Principe

- **Photos** : 5 sections de `100svh`, image en `object-fit: cover` (ajustée en largeur, recadrée en hauteur), calque noir `rgba(0,0,0,.4)` par-dessus (`.slide::after`).
- **Affiche** : `.poster` en `position: fixed`, ratio 3:4, centrée, rouge `#FF0000` avec `mix-blend-mode: lighten`. Texte en vrai HTML, logo et filets en SVG.
- **Unité** : `--k = 100cqw / 1170`. Toutes les valeurs sont en « px du visuel d'origine » (1170 de large), ex. `calc(92*var(--k))`.
- **Recentrage** : `.poster > *` reçoit `translate: -7.5k -17.65k` pour centrer le contenu (marges égales).
- **Flèche « Préventes »** : SVG inline `.arrow`, trait ~6,8 px (= trait du logo agrandi). Elle glisse au scroll (script en bas de page : `Math.cos(scrollY / 80)`, amplitude `0.4em`). Désactivée si `prefers-reduced-motion`.

## Styles de texte

| Classe | Taille | Interligne | Variations | Espacement |
|---|---|---|---|---|
| `big` (dates, titre) | 146,4 | 129,6 | wdth 80, wght 600 | -3 % |
| `mid` (infos, préventes) | 74,4 | 69,03 | wdth 80, wght 600 | 0 |
| `sml` (2027, présente, 20:30) | 34,56 | 31,1 | wdth 75, wght 700 | +2 % |

## Positions (px du visuel, `top` de la boîte de texte)

- Filets : haut y=122, milieu y=738, bas y=1473,3 (colonnes 92→410 et 458→1093)
- `dates` / `title` : 236 · `year` / `pres` : 651,6
- Logo : left 92, top 855, largeur 218,4
- `info` : 847,3 (haut des chiffres aligné sur le haut du logo)
- `doors` : 1223,6 · `presales` : 1285,9
- Règles d'espacement : 42 px (bas des lettres → haut des lettres) autour de « 20:30 », et « Préventes » à la même distance des filets du bas que le filet du haut du gros titre.

## Points d'attention

- **Police d'essai** : `MuotoTrialVAR.ttf` est une version trial et elle est publiée avec le dépôt public. À régulariser (licence complète) avant une vraie mise en ligne.
- La police n'a pas de glyphe `→` : la flèche est donc dessinée en SVG.
- Sur écran large, l'affiche garde son format 3:4 au centre, les photos prennent toute la largeur.
- Les positions ont été calculées d'après les métriques de la police (cap-height 0,72 ; ascent 0,96 ; descent 0,24) puis vérifiées sur captures.
- Test en local : `file://` ne charge pas les images dans l'aperçu intégré ; utiliser un serveur local (`python3 -m http.server`) ou la page GitHub Pages (déploiement ≈ 1 min après un push).

## Idées / à faire

- Rendre « Préventes → » cliquable (lien billetterie à fournir).
- Version mobile à vérifier (l'affiche reste en 3:4 centrée).
- Licence de la police Muoto.
