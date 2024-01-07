## Next.js App Router Course - Starter

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.

## Contenuto Cartelle

/app: contiene tutti i percorsi, i componenti e la logica per la tua applicazione, è da qui che lavorerai principalmente.

/app/lib: contiene funzioni utilizzate nell'applicazione, come funzioni di utilità riutilizzabili e funzioni di recupero dati.

/app/ui: contiene tutti i componenti dell'interfaccia utente per l'applicazione, ad esempio schede, tabelle e moduli. Per risparmiare tempo, abbiamo pre-progettato questi componenti per te.

/public: contiene tutte le risorse statiche per l'applicazione, ad esempio le immagini.

/scripts: contiene uno script di seeding che utilizzerai per popolare il database in un capitolo successivo.

File di configurazione : noterai anche i file di configurazione come next.config.jsnella radice della tua applicazione. La maggior parte di questi file vengono creati e preconfigurati quando si avvia un nuovo progetto utilizzando create-next-app. Non sarà necessario modificarli in questo corso.

## Placeholder data

Quando crei interfacce utente, è utile avere alcuni dati segnaposto. Se un database o un'API non è ancora disponibile, puoi:

Utilizza i dati segnaposto in formato JSON o come oggetti JavaScript.
Utilizza un servizio di terze parti come mockAPI.
Per questo progetto, abbiamo fornito alcuni dati segnaposto in formato app/lib/placeholder-data.js. Ogni oggetto JavaScript nel file rappresenta una tabella nel database.

## TypeScript

Potresti anche notare che la maggior parte dei file ha il suffisso .tso .tsx. Questo perché il progetto è scritto in TypeScript. Volevamo creare un corso che riflettesse il panorama web moderno.

Non è un problema se non conosci TypeScript: forniremo gli snippet di codice TypeScript quando richiesto.

Per ora, dai un'occhiata al /app/lib/definitions.tsfile. Qui definiamo manualmente i tipi che verranno restituiti dal database.

## Stili Globali

Se guardi all'interno della /app/uicartella, vedrai un file chiamato global.css. Puoi utilizzare questo file per aggiungere regole CSS a tutti i percorsi nella tua applicazione, come regole di reimpostazione CSS, stili a livello di sito per elementi HTML come collegamenti e altro ancora.

Puoi importare global.cssqualsiasi componente nella tua applicazione, ma in genere è buona norma aggiungerlo al componente di livello superiore. In Next.js, questo è il layout root (ne parleremo più avanti).

Aggiungi stili globali alla tua applicazione accedendo /app/layout.tsxe importando il global.cssfile:

Con il server di sviluppo ancora in esecuzione, salva le modifiche e visualizzane l'anteprima nel browser.
Verifica la La home page all'indirizzo http://localhost:3000/

## Tailwind

è un framework CSS che accelera il processo di sviluppo consentendoti di scrivere rapidamente classi di utilitàdirettamente nel markup TSX.

In Tailwind puoi definire lo stile degli elementi aggiungendo i nomi delle classi.

Se guardi /app/page.tsx, vedrai che nell'esempio stiamo utilizzando le classi Tailwind.

Giochiamo con Tailwind! Copia il codice qui sotto e incollalo sopra l' <p>elemento in /app/page.tsx:

<div
  className="h-0 w-0 border-b-[30px] border-l-[20px] border-r-[20px] border-b-black border-l-transparent border-r-transparent"
/>

Se preferisci scrivere regole CSS tradizionali o mantenere i tuoi stili separati dal tuo JSX, i moduli CSS sono un'ottima alternativa.

## Moduli Css

I moduli CSS ti consentono di definire l'ambito CSS di un componente creando automaticamente nomi di classe univoci, in modo da non doverti preoccupare anche delle collisioni di stili.

Continueremo a utilizzare Tailwind in questo corso, ma prendiamoci un momento per vedere come è possibile ottenere gli stessi risultati del quiz riportato sopra utilizzando i moduli CSS.

All'interno /app/ui, crea un nuovo file chiamato home.module.css e aggiungi le seguenti regole CSS:

.shape {
height: 0;
width: 0;
border-bottom: 30px solid black;
border-left: 20px solid transparent;
border-right: 20px solid transparent;
}

Quindi, all'interno del tuo /app/page.tsx file importa gli stili e sostituisci i nomi delle classi tailwind con styles.shape:

<div className={styles.shape}></div>;

I moduli Tailwind e CSS sono i due modi più comuni per applicare stili alle applicazioni Next.js. Usare l'uno o l'altro è una questione di preferenza: puoi anche usarli entrambi nella stessa applicazione!

## Utilizzo della clsx libreria per attivare/disattivare i nomi delle classi

Potrebbero esserci casi in cui potrebbe essere necessario definire uno stile condizionale per un elemento in base allo stato o ad altre condizioni.

clsx è una libreria che ti consente di alternare facilmente i nomi delle classi.

Supponiamo di voler creare un InvoiceStatuscomponente che accetti status. Lo stato può essere 'pending'o 'paid'.

Se lo è 'paid', vuoi che il colore sia verde. Se lo è 'pending', vuoi che il colore sia grigio.

## Altre soluzioni di styling

Oltre agli approcci di cui abbiamo discusso, puoi anche definire uno stile per la tua applicazione Next.js con:

- Sass che permette di importare .csse .scssfile.
- Librerie CSS-in-JS come styled-jsx, styled-components, and emotion.
- Dai un'occhiata alla documentazione CSS per ulteriori informazioni.

## Perché ottimizzare i fonts?

I caratteri svolgono un ruolo significativo nella progettazione di un sito Web, ma l'utilizzo di caratteri personalizzati nel progetto può influire sulle prestazioni se è necessario recuperare e caricare i file dei caratteri.

Cumulative Layout Shift è una metrica utilizzata da Google per valutare le prestazioni e l'esperienza dell'utente di un sito web.
Con i fonts, il cambiamento del layout avviene quando il browser esegue inizialmente il rendering del testo in un font di riserva o di sistema e quindi lo sostituisce con un font personalizzato una volta caricato. Questo scambio può causare la modifica della dimensione, della spaziatura o del layout del testo, spostando gli elementi attorno ad esso.

Next.js ottimizza automaticamente i caratteri nell'applicazione quando utilizzi il next/fontmodulo. Scarica i file dei caratteri in fase di creazione e li ospita con le altre risorse statiche. Ciò significa che quando un utente visita la tua applicazione, non ci sono richieste di rete aggiuntive per i caratteri che potrebbero influire sulle prestazioni.

## Aggiunta di un carattere principale

Aggiungiamo un carattere Google personalizzato alla tua applicazione per vedere come funziona!

Nella tua /app/ui cartella, crea un nuovo file chiamato fonts.ts. Utilizzerai questo file per conservare i caratteri che verranno utilizzati nell'applicazione.

Importa il Intercarattere dal next/font/googlemodulo: questo sarà il tuo carattere principale. Quindi, specificare quale subset desideri caricare. In questo caso, 'latin':

import { Inter } from 'next/font/google';

export const inter = Inter({ subsets: ['latin'] });

Infine, aggiungi il font all'elemento <body> in /app/layout.tsx.

Aggiungendo Inter all'elemento <body>, il carattere verrà applicato a tutta l'applicazione.
Qui stai aggiungendo anche Tailwind antialiased classe che leviga il carattere. Non è necessario utilizzare questa classe, ma aggiunge un bel tocco.

Passare al browser, aprire gli strumenti di sviluppo e selezionare l' body elemento. Dovresti vedere Intere Inter_Fallbackora sono applicati sotto gli stili.

Ora è il tuo turno! Nel tuo fonts.ts file, importa un carattere secondario chiamato Lusitana e passalo all'elemento <p> nel tuo /app/page.tsxfile.

Oltre a specificare un sottoinsieme come hai fatto prima, dovrai anche specificare lo spessore del carattere.

Infine, il <AcmeLogo /> componente utilizza anche Lusitana. È stato commentato per evitare errori, ora puoi rimuoverlo dal commento-

Ottimo, hai aggiunto due caratteri personalizzati alla tua applicazione! Successivamente, aggiungiamo un'immagine hero alla home page.

## Perché ottimizzare le immagini?

Next.js può fornire risorse statiche , come immagini, nella /publiccartella di livello superiore. È possibile fare riferimento ai file interni /publicnell'applicazione.

Con il normale HTML, dovresti aggiungere un'immagine come segue:

<img
  src="/hero.png"
  alt="Screenshots of the dashboard project showing desktop version"
/>

Tuttavia, ciò significa che devi manualmente:

Assicurati che la tua immagine sia reattiva su schermi di dimensioni diverse.
Specifica le dimensioni delle immagini per diversi dispositivi.
Evita lo spostamento del layout durante il caricamento delle immagini.
Immagini a caricamento lento che si trovano all'esterno del viewport dell'utente.
L'ottimizzazione delle immagini è un argomento ampio nello sviluppo web che potrebbe essere considerato una specializzazione a sé stante. Invece di implementare manualmente queste ottimizzazioni, puoi utilizzare il next/imagecomponente per ottimizzare automaticamente le tue immagini.

## Il <Image> componente

Il <Image> componente è un'estensione del <img> tag HTML e viene fornito con l'ottimizzazione automatica dell'immagine, come ad esempio:

- Prevenire lo spostamento automatico del layout durante il caricamento delle immagini.
- Ridimensionare le immagini per evitare di inviare immagini di grandi dimensioni a dispositivi con un viewport più piccolo.
- Caricamento lento delle immagini per impostazione predefinita (le immagini vengono caricate quando entrano nel viewport).
- Servire immagini in formati moderni, come WebPe AVIF, quando il browser lo supporta.

## Aggiunta dell'immagine Hero del Desktop.

Usiamo il <Image> componente. Se guardi all'interno della /public cartella, vedrai che ci sono due immagini: hero-desktop.pnge hero-mobile.png.
Queste due immagini sono completamente diverse e verranno visualizzate a seconda che il dispositivo dell'utente sia desktop o mobile.

Nel tuo /app/page.tsx file, importa il componente da next/image.
Quindi, aggiungi l'immagine sotto il commento: /_ Add Hero Images Here _/

Qui stai impostando i pixel width da 1000 e height da 760. È buona norma impostare le width e height in proporzione per evitare spostamenti del layout;
queste dovrebbero avere proporzioni identiche all'immagine sorgente.

## Esercizio: aggiungere l'immagine dell'Hero mobile

Ora è il tuo turno! Sotto l'immagine che hai appena aggiunto, aggiungi un altro <Image> componente per hero-mobile.png.

- L'immagine dovrebbe avere un width numero di 560 e height di 620 pixel.
- Dovrebbe essere mostrato sugli schermi dei dispositivi mobili e nascosto sul desktop: puoi utilizzare gli strumenti di sviluppo per verificare se le immagini del desktop e del dispositivo mobile vengono scambiate correttamente.
- Una volta pronto, espandi lo snippet di codice riportato di seguito per visualizzare la soluzione.

Noterai anche la classe hidden per rimuovere l'immagine dal DOM sugli schermi dei dispositivi mobili e md:block per mostrare l'immagine sugli schermi dei desktop.

## Routing nidificato

Next.js utilizza il routing del file system in cui le cartelle vengono utilizzate per creare percorsi nidificati. Ciascuna cartella rappresenta un segmento di percorso mappato a un segmento URL .

Puoi creare interfacce utente separate per ogni percorso utilizzando file layout.tsx e page.tsx.

page.tsxè un file Next.js speciale che esporta un componente React ed è necessario affinché il percorso sia accessibile.
Nella tua applicazione hai già un file di paging: /app/page.tsx - questa è la home page associata al percorso /.

Per creare un percorso nidificato, puoi nidificare le cartelle una dentro l'altra e aggiungere page.tsxfile al loro interno

/app/dashboard/page.tsx è associato al /dashboard percorso. Creiamo la pagina per vedere come funziona!

## Creazione della pagina del dashboard

Crea una nuova cartella chiamata dashboard dentro /app.

Quindi, crea un nuovo page.tsx file all'interno della dashboard cartella con il seguente contenuto:

export default function Page() {

return <p>Dashboard Page</p>;
}

Ora assicurati che il server di sviluppo sia in esecuzione e visita http://localhost:3000/dashboard. Dovresti vedere il testo "Dashboard Page".

Ecco come puoi creare diverse pagine in Next.js: crea un nuovo segmento di percorso utilizzando una cartella e aggiungi un pagefile al suo interno.

Avendo un nome speciale per i files page, Next.js ti consente di collocare componenti dell'interfaccia utente, file di test e altro codice correlato con i tuoi percorsi. Solo il contenuto all'interno del pagefile sarà accessibile pubblicamente.
Ad esempio, le cartelle /ui e /lib sono collocate all'interno della /app cartella insieme ai percorsi.

## Esercizio: Creazione delle pagine del dashboard

Esercitiamoci a creare più percorsi. Nella dashboard, crea altre due pagine:

- Pagina Clienti : la pagina deve essere accessibile su http://localhost:3000/dashboard/customers.
- Per ora, dovrebbe restituire un <p>Customers Page</p> elemento.
- Pagina delle fatture : la pagina delle fatture dovrebbe essere accessibile su http://localhost:3000/dashboard/invoices.
- Per ora, restituisci anche un <p>Invoices Page</p> elemento.

## Creazione del layout del dashboard

Le dashboard hanno una sorta di navigazione condivisa su più pagine.
In Next.js, puoi utilizzare un layout.tsx file speciale per creare un'interfaccia utente condivisa tra più pagine.
Creiamo un layout per le pagine della dashboard!

All'interno della /dashboard cartella, aggiungi un nuovo file chiamato layout.tsxe incolla il seguente codice:

import SideNav from '@/app/ui/dashboard/sidenav';

export default function Layout({ children }: { children: React.ReactNode }) {
return (

  <div className="flex h-screen flex-col md:flex-row md:overflow-hidden">
    <div className="w-full flex-none md:w-64">
      <SideNav />
    </div>
    <div className="flex-grow p-6 md:overflow-y-auto md:p-12">{children}</div>
  </div>
);
}

Innanzitutto, stai importando il <SideNav /> componente nel tuo layout. Tutti i componenti importati in questo file faranno parte del layout.

Il <Layout />componente riceve un children sostegno.
Questo elemento secondario può essere una pagina o un altro layout.
Verifica che tutto funzioni correttamente salvando le modifiche e controllando http://localhost:3000/dashboard

Un vantaggio dell'utilizzo dei layout in Next.js è che durante la navigazione, solo i componenti della pagina si aggiornano mentre il layout non verrà nuovamente visualizzato. Questo si chiama rendering parziale.

## Disposizione della radice

Nel Capitolo 3 avete importato il Inter carattere in un altro layout: /app/layout.tsx.

Questo è chiamato layout root ed è obbligatorio. Qualsiasi interfaccia utente aggiunta al layout root verrà condivisa su tutte le pagine dell'applicazione.
Puoi utilizzare il layout root per modificare i tag <html> e <body> e aggiungere metadati (imparerai di più sui metadati in un capitolo successivo ).

Poiché il nuovo layout che hai appena creato ( /app/dashboard/layout.tsx) è unico per le pagine del dashboard, non è necessario aggiungere alcuna interfaccia utente al layout principale sopra.

## Perchè ottimizzare la navigazione?

Per collegare le pagine, utilizzeresti tradizionalmente l' <a>elemento HTML. Al momento, i collegamenti della barra laterale utilizzano <a>elementi, ma nota cosa succede quando navighi tra le pagine Home, Fatture e Clienti sul tuo browser.

L'hai visto?

C'è un aggiornamento completo della pagina in ogni navigazione della pagina!

## Il <Link> componente

In Next.js, puoi utilizzare il <Link /> componente per collegare le pagine nella tua applicazione.

<Link> ti consente di eseguire la navigazione lato client con JavaScript.

Per utilizzare il <Link /> componente, aprire /app/ui/dashboard/nav-links.tsx e importare il Link componente da next/link.

Quindi, sostituisci il <a> tag con <Link>.

Come puoi vedere, il Link componente è simile all'uso <a> dei tag, ma invece di <a href="…">, usi <Link href="…">.

Salva le modifiche e controlla se funziona nel tuo localhost.
Ora dovresti essere in grado di navigare tra le pagine senza visualizzare un aggiornamento completo.
Sebbene parti della tua applicazione vengano renderizzate sul server, non è previsto l'aggiornamento dell'intera pagina, facendola sembrare un'app Web.
Perché?

## Suddivisione e precaricamento automatici del codice

Per migliorare l'esperienza di navigazione, il codice Next.js divide automaticamente la tua applicazione in segmenti di percorso. Questo è diverso da una React SPA tradizionale, dove il browser carica tutto il codice dell'applicazione al caricamento iniziale.

Suddividere il codice per percorsi significa che le pagine vengono isolate.

Se una determinata pagina genera un errore, il resto dell'applicazione continuerà a funzionare.

Inoltre, in produzione, ogni volta che <Link> i componenti appaiono nel viewport del browser, Next.js precarica automaticamente il codice per il percorso collegato in background.
Nel momento in cui l'utente fa clic sul collegamento, il codice per la pagina di destinazione sarà già caricato in background, e questo è ciò che rende la transizione della pagina quasi istantanea!

## Modello: visualizzazione dei collegamenti attivi

Uno schema comune dell'interfaccia utente consiste nel mostrare un collegamento attivo per indicare all'utente in quale pagina si trova attualmente. Per fare ciò, è necessario ottenere il percorso corrente dell'utente dall'URL.
Next.js fornisce un hook chiamato usePathname() che puoi utilizzare per controllare il percorso e implementare questo modello.

Dato che usePathname() è un hook, dovrai trasformare nav-links.tsx in un componente client.
Aggiungi la direttiva di React "use client" all'inizio del file, quindi importa usePathname() da next/navigation.

Successivamente, assegna il percorso a una variabile chiamata pathname all'interno del tuo <NavLinks /> componente.

È possibile utilizzare la clsx libreria introdotta nel capitolo sullo stile CSS per applicare in modo condizionale i nomi delle classi quando il collegamento è attivo.

Quando link.href corrisponde a pathname, il collegamento dovrebbe essere visualizzato con testo blu e sfondo azzurro.

Salva e controlla il tuo host locale. Ora dovresti vedere il collegamento attivo evidenziato in blu.
