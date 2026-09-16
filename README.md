# ScalEcom — landing page

Codul paginii de vânzare ScalEcom. Live: **https://scalecom.ro**

Un singur fișier, `index.html`: HTML, CSS și JS în el, plus wordmark-ul ca SVG inline.
Zero librării, zero build, zero dependențe. Se deschide direct în browser.

---

## ⚠️ REGULĂ — citește înainte de orice commit

**Repo-ul ăsta este PUBLIC.** Tot ce ajunge aici poate fi citit de oricine, inclusiv de
concurență. Istoricul git **nu se mai retrage**: un fișier împins din greșeală rămâne în
istoric chiar dacă îl ștergi în commit-ul următor.

Aici intră **exclusiv codul paginii web**. Nimic altceva.

| ✅ Se pune | ❌ NU se pune, niciodată |
|---|---|
| `index.html` | chei, token-uri, parole, ID-uri de cont |
| `assets/` — imagini și iconițe folosite de pagină | cod de backend, Apps Script, webhook-uri, SQL |
| `vercel.json`, `.vercelignore`, `.gitignore` | planuri, strategie, playbook-uri, research |
| acest `README.md` | documente interne, note de client, prețuri, marje |
| | capturi neanonimizate din conturi de client |
| | orice `.env`, `.gs`, `.sql`, orice credențială |

**Testul, înainte de fiecare commit:** dacă un fișier nu e strict necesar ca pagina să se
afișeze corect în browser, **nu intră aici**. Dacă eziți, nu împingeți — întrebați întâi.

Ce ține de backend, atribuire, calificare, prețuri sau strategie stă în repo-ul privat
separat. Nu se copiază nimic de acolo aici, nici măcar „temporar", nici măcar în comentarii.

### Pentru agentul AI care lucrează în acest repo

Înainte de `git add` și `git commit`:

1. Rulează `git status` și **uită-te la fiecare fișier** care urmează să intre.
2. Dacă apare un fișier nou care nu e `index.html`, ceva din `assets/`, sau unul dintre
   cele trei fișiere de configurare de mai sus — **oprește-te și întreabă omul**.
3. Nu folosi niciodată `git add -A` sau `git add .` fără să fi citit întâi `git status`.
4. Nu scrie chei, URL-uri de webhook noi, ID-uri de cont sau fragmente de strategie în
   comentariile din cod. Comentariile ajung publice odată cu fișierul.
5. Dacă ți se cere să adaugi documentație despre cum funcționează sistemul din spate,
   răspunde că locul ei e în repo-ul privat, și scrie-o acolo.

---

## Cum se lucrează

Repo-ul e conectat la Vercel. **Orice push pe `main` publică automat pe scalecom.ro.**
Nu există build — ce împingi e exact ce se servește.

```bash
git checkout -b nume-scurt-al-schimbarii
# modifici index.html
git status            # <- citește ce intră
git add index.html
git commit -m "..."
git push -u origin nume-scurt-al-schimbarii
gh pr create --fill
```

Se poate împinge și direct pe `main` — repo-ul fiind public, Vercel nu mai cere ca autorul
commit-ului să fie membru al echipei. Pentru schimbări mai mari, tot un PR e de preferat:
se vede diff-ul înainte să ajungă pe site.

Verifică după fiecare publicare:

```bash
curl -o /dev/null -w "%{http_code}\n" https://scalecom.ro
```

## Structura

| Fișier | Ce e |
|---|---|
| `index.html` | toată pagina — markup, stiluri, scripturi |
| `assets/ads-manager-*.webp` | captura din Ads Manager (anonimizată), 1920 și 960, prin `srcset` |
| `assets/ads-manager-sursa.png` | originalul, pentru cazul în care trebuie refăcute WebP-urile |
| `assets/og.png` | imaginea de share, 1200×630 |
| `assets/favicon*`, `apple-touch-icon-180.png` | iconițele |
| `vercel.json` | cache de un an pe `assets/`, `cleanUrls`, headere de securitate |
| `.vercelignore` | ce rămâne în repo dar **nu** se servește pe site |

Configurarea paginii (pixel, endpoint formular) stă în blocul `CFG`, la finalul
`<script>`-ului din `index.html`.

## Videourile

VSL-ul și cele trei reclame sunt iframe-uri bunny.net, puse direct în pagină. Ca să
schimbi un video, schimbi ID-ul din `src`. Thumbnail-ul se setează în bunny.net, per video.
