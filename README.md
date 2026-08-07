# Sito Dott. Gaetano Grosso

Sito vetrina (one-page) per il **Dott. Gaetano Grosso** — Cardiologia clinica, studio privato.

Impostazione: **sito informativo, non persuasivo**. L'utenza è adulta e anziana e arriva cercando tre cose — a chi telefonare, cosa si fa in visita, dove si trova lo studio. La pagina le mette tutte a portata di mano, con testi in registro formale e impersonale.

Sito statico: [`index.html`](index.html) con CSS inline, [`privacy.html`](privacy.html), font self-hosted in [`assets/fonts/`](assets/fonts) e marchio in [`assets/logo/`](assets/logo). Nessuna build, nessuna dipendenza, nessun cookie, nessuna fotografia.

**Nessuna prenotazione online**: tutti i pulsanti “Prenota una visita” portano alla sezione Contatti, dove telefono ed email sono cliccabili (`tel:` / `mailto:`). Non ci sono moduli né servizi di terze parti.

## Anteprima in locale

```bash
python3 -m http.server 4522
```

Poi apri http://localhost:4522.

## Struttura della pagina

1. **Testata** sticky con lockup e pulsante di prenotazione (su mobile: telefono e menu, comandi da 44px)
2. **Hero** — occhiello, titolo, sintesi dell'offerta, due azioni (colonna unica: nessuna fotografia)
3. **Fascia recapiti** — telefono, orari e sede visibili senza scorrere
4. **Prestazioni** — prospetto unico a filetti: prestazione · descrizione e preparazione · durata
5. **Svolgimento della visita** — sequenza verticale numerata in cinque passaggi, più la nota su cosa portare
6. **Lo studio** — curriculum essenziale, riquadro dati professionali, dotazione strumentale
7. **Domande frequenti** — sei risposte sempre visibili (impegnativa, costi, referto, accompagnatore, disdetta, accessibilità)
8. **Contatti** — due pannelli d'azione (telefono / email), posta elettronica, tabella degli orari, le due sedi con mappa a caricamento su richiesta
9. **Footer** su fondo `--ink` con recapiti, dati legali e dichiarazione di conformità deontologica

Rispetto al sito della Dott.ssa Grosso — da cui è partita la struttura di base (statico, one-page, CSS inline, font self-hosted) — questo diverge per professione e utenza: niente griglia di riquadri tematici, niente banner di prenotazione, niente animazioni allo scroll né tema scuro; al loro posto un prospetto delle prestazioni, un protocollo di visita numerato, le domande frequenti e i recapiti ripetuti tre volte lungo la pagina (fascia, contatti, footer).

## Stack

- HTML + CSS (inline), zero framework, zero JavaScript di terze parti (l'unico contenuto esterno è la mappa, e solo su richiesta)
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
   - **tinta `#E4F2F6` = una volta sola**, sulla fascia dei recapiti sotto la hero.
   - le sezioni alternate usano il tono più pallido `#F5FBFC` e si distinguono per **filetto**, non per stacco di colore.

   La proporzione neutri/accento sale così ben oltre il 90/10 chiesto dall'handoff. Per tornare all'impostazione originale basta `--bg-page:#F5FBFC` e `.band{background:var(--bg-surface)}`.
2. **Scala tipografica alzata**: corpo 18px (l'handoff indica 17 come minimo), interlinea 1.7, lead 20px, nav 16px, recapiti 23px. Lettura a distanza di braccio.
3. **Occhielli in IBM Plex Sans maiuscoletto** invece che in monospaziato. Il **monospaziato resta solo sui dati** — telefono, email, indirizzo, orari — come da uso previsto per “orari e recapiti”.
4. **Titoli in Newsreader 400** anziché 300: peso più solido, meno da rivista.
5. **Filetto 1px sopra ogni titolo di sezione**: impaginazione da documento.
6. **Numeri dei passaggi in cifre serif** al posto di `01`–`04` monospaziati, e sequenza verticale invece che a quattro colonne.
7. **Prestazioni in prospetto unico** invece della griglia di tre card suggerita dall'handoff: un elenco solo, leggibile come un documento, con durata e preparazione per ogni voce.
8. **Titolo e sottotitolo della hero** riscritti: quelli del brand board erano più brillanti che clinici.
9. **Ordine delle voci di nav**: `Prestazioni · Percorso · Studio · Contatti`, per seguire lo scorrimento della pagina invece dell'ordine del mock (`Studio` per primo).
10. **Menu a tendina già da 900px** (l'handoff lo prevede sotto i 600): a 4 voci più il pulsante, la barra è troppo stretta sui tablet.

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

- **Comunicare la messa online all'Ordine dei Medici di Cosenza**, contestualmente al passaggio sul dominio definitivo: è un adempimento previsto dalla linea-guida FNOMCeO, non una cortesia. Recapiti e dettagli nella sezione *Privacy e comunicazione sanitaria*.
- Le fotografie **non sono previste**: il cliente non desidera né il proprio ritratto né immagini dello studio. La pagina è composta di solo testo, filetti e marchio, e la hero è a colonna unica.

## Correzione al marchio (difetto nei file consegnati)

Gli SVG del pacchetto hanno la **viewBox più stretta del tracciato**: `viewBox="38 6 130 98"` a fronte di un disegno che, incluso lo spessore delle linee, occupa x `37.06 – 165.38` e y `6.14 – 103.86`. Conseguenza: l'anello esterno della G veniva rasato sul lato sinistro e appoggiava esattamente sui bordi superiore e inferiore — a schermo sembrava tagliato e schiacciato.

Nelle copie in `assets/logo/` e nei marchi ricomposti dentro le pagine la viewBox è ora `36 5 131 100`, con circa un'unità di respiro per lato. Nessuna coordinata del disegno è stata toccata.

In `favicon.svg` il marchio non era tagliato ma stava alto nel quadrato (centro a 27.3 invece di 32): corretto il `transform`, e i PNG `favicon-{32,180,512}.png` sono stati rigenerati dal file corretto (i riferimenti nelle pagine sono passati a `?v=2`).

I file originali restano intatti in `_sources/`. **La correzione va riportata anche lì dal grafico**, insieme al passaggio in editor vettoriale già segnalato nel README dell'handoff: il `lockup-orizzontale.png` invece è a posto, il marchio non è tagliato.

## Privacy e comunicazione sanitaria

Due scelte deliberate, per non far dire al sito cose che spettano allo studio.

**Le mappe si caricano solo su richiesta.** Nella sezione contatti ogni sede ha un riquadro con il pulsante *Mostra la mappa*: l'`iframe` di Google viene creato dal JavaScript solo dopo il clic. Prima di quel momento **nessun dato raggiunge Google** e il sito resta senza contatti con terze parti, coerentemente con la scelta di ospitare i font in locale. È il motivo per cui non serve un banner cookie: il consenso è il clic stesso, ed è documentato al punto 3 dell'informativa. Sostituire questo meccanismo con un `iframe` caricato subito comporterebbe cookie di terzi in assenza di consenso.

**L'informativa privacy copre solo il sito.** Il sito non ha moduli, non usa cookie, non ha analytics e i font sono in locale: non raccoglie nulla, quindi non c'è un banner di consenso perché non c'è nulla da consentire. La pagina dichiara il titolare, i due fornitori (hosting e posta), i dati tecnici registrati nei log del server e i diritti dell'interessato. Il trattamento dei **dati sanitari** (art. 9 GDPR) non è descritto qui: avviene nell'ambito della prestazione medica e la relativa informativa lo studio la consegna già al paziente in sede di visita. Duplicarla sul sito avrebbe significato scrivere al posto del cliente affermazioni su conservazione e basi giuridiche che non ci competono.

**Comunicazione sanitaria: tre adempimenti, non uno.** Le fonti sono due e si sommano.

La **legge 145/2018** (art. 1, commi 525 e seguenti) regola il *contenuto*: solo informazioni funzionali alla sicurezza dei trattamenti, senza elementi promozionali o suggestivi. Il sito è conforme per costruzione — nessun superlativo, nessuna promessa di risultato, nessun prezzo presentato come offerta — e riporta i dati identificativi richiesti dalla deontologia: qualifica, specializzazioni, iscrizione all'Ordine, P. IVA.

La **linea-guida FNOMCeO sulla pubblicità dell'informazione sanitaria**, attuativa degli artt. 55–57 del Codice di deontologia medica, aggiunge tre requisiti specifici per i siti internet:

1. **Dichiarazione nel sito**: il professionista dichiara «sotto la propria responsabilità, che il messaggio informativo è diramato nel rispetto della presente linea guida». È la nota in fondo alla pagina — non è decorativa, è l'adempimento.
2. **Comunicazione all'Ordine provinciale** della messa online del sito, dichiarandone la conformità deontologica. **Va fatta al momento del passaggio sul dominio definitivo**, non per l'anteprima su GitHub Pages.
3. **Dominio nazionale o UE**: i siti «devono essere registrati su domini nazionali italiani e/o dell'Unione Europea». `dottorgaetanogrosso.it` soddisfa il requisito; un `.com` no.

Direttore sanitario e autorizzazione sanitaria non si applicano: riguardano le strutture, non lo studio individuale.

**Ordine dei Medici Chirurghi e degli Odontoiatri di Cosenza** — Via Suor Elena Aiello (Palazzo Lucchetta), 87100 Cosenza · tel. 0984 412841 · segreteria@ordinemedici.cosenza.it · PEC segreteria@pec.ordinemedici.cosenza.it. Chiedere alla segreteria il modulo di comunicazione, se ne usano uno proprio.

## Note

- I materiali sorgente del brand sono in `_sources/` ed esclusi dal repo tramite `.gitignore`.
- Se in futuro serve un modulo di contatto, va aggiunta la relativa sezione all'informativa privacy: oggi il sito dichiara di non raccogliere alcun dato.
