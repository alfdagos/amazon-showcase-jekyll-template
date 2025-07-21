# Amazon Showcase Jekyll Template

Un template Jekyll moderno e completamente personalizzabile per siti di affiliazione Amazon, basato su Tailwind CSS e progettato per essere facilmente configurabile e mantenibile.

## Caratteristiche

- **Design Moderno e Responsive**: Interfaccia pulita e professionale che si adatta perfettamente a tutti i dispositivi
- **Architettura Modulare**: Componenti separati e riutilizzabili per una facile manutenzione
- **Gestione Contenuti Semplificata**: Tutti i contenuti sono gestiti tramite file YAML per modifiche rapide
- **Filtraggio Categorie**: Sistema di filtri dinamico per organizzare i prodotti
- **Funzionalità di Ricerca**: Ricerca in tempo reale tra i prodotti
- **Newsletter Integration**: Sezione newsletter pronta per l'integrazione
- **SEO Ottimizzato**: Struttura ottimizzata per i motori di ricerca
- **Performance**: Codice ottimizzato per caricamenti veloci

## Struttura del Progetto

```
amazon-showcase-jekyll-template/
├── _config.yml                 # Configurazione principale del sito
├── _data/
│   ├── categories.yml          # Definizione delle categorie prodotti
│   └── products.yml            # Database dei prodotti
├── _includes/
│   ├── header.html             # Header del sito con navigazione
│   ├── hero.html               # Sezione hero della homepage
│   ├── categories.html         # Tabs delle categorie
│   ├── products.html           # Griglia dei prodotti
│   ├── newsletter.html         # Sezione newsletter
│   └── footer.html             # Footer del sito
├── _layouts/
│   └── default.html            # Layout base del sito
├── _sass/
│   ├── _variables.scss         # Variabili SCSS (colori, font, etc.)
│   ├── _base.scss              # Stili base e tipografia
│   ├── _layout.scss            # Stili per layout e componenti
│   └── main.scss               # File SCSS principale
├── assets/
│   ├── css/
│   │   └── main.scss           # Punto di ingresso per i CSS
│   ├── js/
│   │   └── main.js             # JavaScript per interattività
│   └── images/                 # Cartella per le immagini
├── index.html                  # Homepage del sito
├── Gemfile                     # Dipendenze Ruby/Jekyll
└── README.md                   # Questa documentazione
```

## Installazione e Setup

### Prerequisiti

- Ruby (versione 2.7 o superiore)
- Jekyll
- Bundler

### Installazione

1. **Clona o scarica il template**
   ```bash
   git clone [repository-url] my-affiliate-site
   cd my-affiliate-site
   ```

2. **Installa le dipendenze**
   ```bash
   bundle install
   ```

3. **Avvia il server di sviluppo**
   ```bash
   bundle exec jekyll serve
   ```

4. **Apri il browser**
   Visita `http://localhost:4000` per vedere il sito in azione

## Personalizzazione

### Configurazione Base

Modifica il file `_config.yml` per personalizzare:

- **Informazioni del sito**: titolo, descrizione, URL
- **Branding**: logo e testo del brand
- **Navigazione**: menu principale
- **Sezione Hero**: titolo, sottotitolo e call-to-action
- **Newsletter**: testi e configurazione
- **Footer**: link e informazioni di contatto
- **Social Media**: link ai profili social

### Gestione Prodotti

I prodotti sono gestiti nel file `_data/products.yml`. Ogni prodotto include:

```yaml
- id: 1
  name: "Nome del Prodotto"
  description: "Descrizione breve del prodotto"
  category: "tech"  # Deve corrispondere a una categoria in categories.yml
  rating: 4.5
  reviews: 120
  original_price: 599.99  # Opzionale, per prodotti scontati
  current_price: 479.99
  discount: 20  # Percentuale di sconto
  badge:
    type: "discount"  # discount, bestseller, offer, new
    text: "-20%"
    color: "amber"  # amber, green, red, blue
  amazon_link: "https://amazon.it/..."
  image: "/assets/images/products/product-image.jpg"
```

### Gestione Categorie

Le categorie sono definite in `_data/categories.yml`:

```yaml
- id: "tech"
  name: "Tecnologia"
  active: false  # true per la categoria attiva di default
```

### Personalizzazione Stili

Gli stili sono organizzati in file SCSS modulari:

- **`_variables.scss`**: Modifica colori, font e spaziature
- **`_base.scss`**: Stili base per tipografia e elementi HTML
- **`_layout.scss`**: Stili per layout e componenti specifici

#### Personalizzazione Colori

Nel file `_sass/_variables.scss` puoi modificare la palette colori:

```scss
$primary-color: #f59e0b;     // Colore principale (amber)
$primary-hover: #d97706;     // Colore hover
$text-primary: #1f2937;      // Testo principale
$text-secondary: #6b7280;    // Testo secondario
```

### Aggiunta di Nuove Pagine

1. Crea un nuovo file HTML nella root del progetto
2. Aggiungi il front matter:
   ```yaml
   ---
   layout: default
   title: "Titolo Pagina"
   description: "Descrizione per SEO"
   ---
   ```
3. Aggiungi il contenuto della pagina
4. Aggiorna la navigazione in `_config.yml` se necessario

## Funzionalità JavaScript

Il template include diverse funzionalità interattive:

- **Filtraggio Categorie**: Filtra i prodotti per categoria
- **Ricerca**: Cerca prodotti per nome o descrizione
- **Menu Mobile**: Navigazione responsive per dispositivi mobili
- **Newsletter**: Validazione email e feedback utente
- **Smooth Scrolling**: Scorrimento fluido per link interni
- **Notifiche**: Sistema di notifiche per feedback utente

## SEO e Performance

### Ottimizzazioni SEO Incluse

- Meta tag ottimizzati
- Struttura HTML semantica
- Sitemap automatica (tramite jekyll-sitemap)
- Feed RSS (tramite jekyll-feed)
- URL puliti e SEO-friendly

### Ottimizzazioni Performance

- CSS e JavaScript minificati in produzione
- Immagini ottimizzate
- Lazy loading per immagini (implementabile)
- CDN per librerie esterne (Tailwind, Font Awesome)

## Deployment

### GitHub Pages

1. Pusha il codice su un repository GitHub
2. Vai nelle impostazioni del repository
3. Abilita GitHub Pages dalla sezione "Pages"
4. Seleziona la branch main come source

### Netlify

1. Connetti il repository a Netlify
2. Imposta il comando di build: `bundle exec jekyll build`
3. Imposta la cartella di publish: `_site`
4. Deploy automatico ad ogni push

### Server Personalizzato

1. Esegui il build: `bundle exec jekyll build`
2. Carica il contenuto della cartella `_site` sul server
3. Configura il server web per servire i file statici

## Personalizzazioni Avanzate

### Integrazione Analytics

Aggiungi il codice di tracking nel layout `_layouts/default.html`:

```html
{% if jekyll.environment == 'production' %}
<!-- Google Analytics o altro -->
<script>
  // Il tuo codice di tracking
</script>
{% endif %}
```

### Integrazione Newsletter

Per integrare un servizio di newsletter reale:

1. Modifica il form in `_includes/newsletter.html`
2. Aggiorna il JavaScript in `assets/js/main.js`
3. Configura l'endpoint del servizio (Mailchimp, ConvertKit, etc.)

### Aggiunta di Nuove Sezioni

1. Crea un nuovo file in `_includes/`
2. Aggiungi gli stili necessari in `_sass/_layout.scss`
3. Includi la sezione in `index.html` o nelle pagine desiderate

## Supporto e Contributi

Per supporto o per contribuire al progetto:

1. Apri una issue per bug o richieste di funzionalità
2. Fai un fork del progetto per contributi
3. Segui le convenzioni di codice esistenti
4. Testa le modifiche prima di inviare una pull request

## Licenza

Questo template è rilasciato sotto licenza MIT. Sei libero di utilizzarlo, modificarlo e distribuirlo per progetti personali e commerciali.

## Crediti

- **Design**: Ispirato alle migliori pratiche di e-commerce moderno
- **Framework CSS**: Tailwind CSS
- **Icone**: Font Awesome
- **Font**: Inter (Google Fonts)
- **Generatore Sito**: Jekyll

---

**Nota**: Questo template è progettato per siti di affiliazione Amazon. Assicurati di rispettare i termini di servizio di Amazon e le normative locali sulla pubblicità e affiliazione.

