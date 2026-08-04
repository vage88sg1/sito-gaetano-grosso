# Sito Dott. Gaetano Grosso

Sito vetrina (one-page) per il **Dott. Gaetano Grosso** — Cardiologia clinica, studio privato.

Impostazione: **sito informativo, non persuasivo**. L'utenza è adulta e anziana e arriva cercando tre cose — a chi telefonare, cosa si fa in visita, dove si trova lo studio. La pagina le mette tutte a portata di mano, con testi in registro formale e impersonale.

Sito statico: [`index.html`](index.html) con CSS inline, [`privacy.html`](privacy.html), font self-hosted in [`assets/fonts/`](assets/fonts) e marchio in [`assets/logo/`](assets/logo). Nessuna build, nessuna dipendenza, nessun cookie.

**Nessuna prenotazione online**: tutti i pulsanti “Prenota una visita” portano alla sezione Contatti, dove telefono ed email sono cliccabili (`tel:` / `mailto:`). Non ci sono moduli né servizi di terze parti.

## Anteprima in locale

```bash
python3 -m http.server 4522
```

Poi apri http://localhost:4522.

## Struttura della pagina

1. **Testata** sticky con lockup e pulsante di prenotazione (su mobile: telefono e menu, comandi da 44px)
2. **Hero** — occhiello, titolo, sintesi dell'offerta, due azioni, ritratto
3. **Fascia recapiti** — telefono, orari e sede visibili senza scorrere
4. **Prestazioni** — prospetto unico a filetti: prestazione · descrizione e preparazione · durata
5. **Svolgimento della visita** — sequenza verticale numerata in cinque passaggi, più la nota su cosa portare
6. **Lo studio** — testo, curriculum essenziale, ritratto, riquadro dati professionali, dotazione strumentale
7. **Domande frequenti** — sei risposte sempre visibili (impegnativa, costi, referto, accompagnatore, disdetta, accessibilità)
8. **Contatti** — due pannelli d'azione (telefono / email), tabella degli orari, indirizzo, mappa
9. **Footer** su fondo `--ink` con recapiti, dati legali e nota della comunicazione sanitaria

Rispetto al sito della Dott.ssa Grosso — da cui è partita la struttura di base (statico, one-page, CSS inline, font self-hosted) — questo diverge per professione e utenza: niente griglia di riquadri tematici, niente banner di prenotazione, niente animazioni allo scroll né tema scuro; al loro posto un prospetto delle prestazioni, un protocollo di visita numerato, le domande frequenti e i recapiti ripetuti tre volte lungo la pagina (fascia, contatti, footer).

## Stack

- HTML + CSS (inline), zero framework, zero JavaScript di terze parti
- Font **Newsreader** + **IBM Plex Sans** + **IBM Plex Mono**, self-hosted (GDPR-friendly: nessuna chiamata a Google)
- Palette “Acqua chiara”: accento `#2B9AA6` / `#1A6F7C`, inchiostro `#37545C`

## Design system

Il sito applica il pacchetto `design_handoff_sito_vetrina` (copia in [`_sources/`](_sources), fuori dal repo pubblicato). Regole rispettate:

- token di `tokens.css` riportati in `:root` (colori, scala tipografica, spaziature)
- **nessun raggio, nessuna ombra, nessun gradiente decorativo**; le superfici si separano con bordi 1px
- ~90% neutri, ~10% accento; `#2B9AA6` mai per testo sotto i 24px (per il testo colorato si usa `#1A6F7C`)
- nessuna animazione: solo transizioni di colore 120ms in hover
- corpo del testo minimo 17px; breakpoint 1200 / 900 / 600
- lockup di testata ricomposto in HTML (monogramma SVG inline + testo), così il nome resta selezionabile

### Scostamenti dall'handoff (voluti, tutti reversibili)

Il registro richiesto è **formale e istituzionale**, per un professionista affermato e un'utenza anziana. Restano invariati palette, marchio, coppia tipografica, assenza di raggi/ombre/animazioni; cambiano gli stilemi più “editoriali” del mock:

1. **Impiego del colore.** L'handoff tinge tutto il fondo pagina (`#F5FBFC`) e alterna fasce `#E4F2F6`. Qui il fondo è **bianco**, da documento, e la regola è netta:
   - **accento acquamarina = interazione**: pulsanti, link, filetto della voce di nav attiva, focus, monogramma. Nient'altro.
   - **inchiostro `#37545C` = struttura**: occhielli, numeri dei passaggi, trattini del curriculum, filetto della nota, footer.
   - **tinta `#E4F2F6` = una volta sola**, sulla fascia dei recapiti sotto la hero (più i segnaposto delle foto).
   - le sezioni alternate usano il tono più pallido `#F5FBFC` e si distinguono per **filetto**, non per stacco di colore.

   La proporzione neutri/accento sale così ben oltre il 90/10 chiesto dall'handoff. Per tornare all'impostazione originale basta `--bg-page:#F5FBFC` e `.band{background:var(--bg-surface)}`.
2. **Scala tipografica alzata**: corpo 18px (l'handoff indica 17 come minimo), interlinea 1.7, lead 20px, nav 16px, recapiti 23px. Lettura a distanza di braccio.
2. **Occhielli in IBM Plex Sans maiuscoletto** invece che in monospaziato. Il **monospaziato resta solo sui dati** — telefono, email, indirizzo, orari — come da uso previsto per “orari e recapiti”.
3. **Titoli in Newsreader 400** anziché 300: peso più solido, meno da rivista.
4. **Filetto 1px sopra ogni titolo di sezione**: impaginazione da documento.
5. **Numeri dei passaggi in cifre serif** al posto di `01`–`04` monospaziati, e sequenza verticale invece che a quattro colonne.
5. **Prestazioni in prospetto unico** invece della griglia di tre card suggerita dall'handoff: un elenco solo, leggibile come un documento, con durata e preparazione per ogni voce.
6. **Segnaposto delle foto a campitura piena** `--bg-surface` invece che a righe diagonali.
7. **Titolo della hero** riscritto (`Prevenzione e diagnosi cardiologica`): quello del brand board era più brillante che clinico.
8. **Ordine delle voci di nav**: `Prestazioni · Percorso · Studio · Contatti`, per seguire lo scorrimento della pagina invece dell'ordine del mock (`Studio` per primo).
9. **Menu a tendina già da 900px** (l'handoff lo prevede sotto i 600): a 4 voci più il pulsante, la barra è troppo stretta sui tablet.

Non è previsto il tema scuro: l'handoff definisce una sola palette e vieta un secondo accento.

## Pubblicazione

Il sito è online come **anteprima su GitHub Pages**, servita dalla radice del ramo `main`.

**L'anteprima è esclusa dai motori di ricerca**, in due modi ridondanti:

- `<meta name="robots" content="noindex, nofollow">` in `index.html` e `privacy.html`
- `robots.txt` con `Disallow: /`

`og:url` e `link rel="canonical"` puntano già al dominio definitivo `https://www.dottorgaetanogrosso.it/`, che non è ancora registrato: finché c'è il `noindex` non ha effetti.

### Per andare live sul dominio definitivo

1. Registrare **dottorgaetanogrosso.it** e puntare il DNS a GitHub Pages (record `A` verso gli IP di Pages più `CNAME` per `www`).
2. Aggiungere il dominio in *Settings → Pages → Custom domain* (crea il file `CNAME` nel repo) e attivare *Enforce HTTPS*.
3. **Togliere il `noindex`** dai due file HTML e riportare `robots.txt` a `Allow: /`.
4. Solo allora, eventualmente, aggiungere una `sitemap.xml` e registrare il sito in Search Console.

## Da completare

- **Le due fotografie**: ritratto in studio (apertura) e ritratto del medico (sezione *Lo studio*). Al loro posto ci sono due campiture con didascalia; cercare `Sostituire con` in `index.html`. Esportare in WebP con `width`/`height` espliciti e `loading="lazy"` per quella sotto la piega.
- **Numero civico della sede di Saracena**, oggi indicata come «Via Santa Maria Maddalena» senza civico.
- **Informativa privacy**: è compilata con i dati reali, ma tratta dati sanitari (art. 9 GDPR) e **va fatta validare da un consulente**. Da confermare in particolare i tempi di conservazione, oggi espressi in forma generica.
- **Testo della comunicazione sanitaria** nel footer: la formula attuale è generica, va confermata con l'Ordine dei Medici di Cosenza.
- Eventuale **mappa statica** nelle due sedi: oggi c'è il collegamento alle indicazioni stradali di Google Maps, che non carica nulla da terze parti finché non lo si clicca. Una mappa incorporata comporterebbe cookie di terzi e un banner di consenso.

## Correzione al marchio (difetto nei file consegnati)

Gli SVG del pacchetto hanno la **viewBox più stretta del tracciato**: `viewBox="38 6 130 98"` a fronte di un disegno che, incluso lo spessore delle linee, occupa x `37.06 – 165.38` e y `6.14 – 103.86`. Conseguenza: l'anello esterno della G veniva rasato sul lato sinistro e appoggiava esattamente sui bordi superiore e inferiore — a schermo sembrava tagliato e schiacciato.

Nelle copie in `assets/logo/` e nei marchi ricomposti dentro le pagine la viewBox è ora `36 5 131 100`, con circa un'unità di respiro per lato. Nessuna coordinata del disegno è stata toccata.

In `favicon.svg` il marchio non era tagliato ma stava alto nel quadrato (centro a 27.3 invece di 32): corretto il `transform`, e i PNG `favicon-{32,180,512}.png` sono stati rigenerati dal file corretto (i riferimenti nelle pagine sono passati a `?v=2`).

I file originali restano intatti in `_sources/`. **La correzione va riportata anche lì dal grafico**, insieme al passaggio in editor vettoriale già segnalato nel README dell'handoff: il `lockup-orizzontale.png` invece è a posto, il marchio non è tagliato.

## Note

- I materiali sorgente del brand sono in `_sources/` ed esclusi dal repo tramite `.gitignore`.
- Se in futuro serve un modulo di contatto, va aggiunta la relativa sezione all'informativa privacy: oggi il sito dichiara di non raccogliere alcun dato.
