# Guida alla Personalizzazione

Questa guida ti aiuterà a personalizzare completamente il template Amazon Showcase Jekyll per adattarlo alle tue esigenze specifiche.

## Personalizzazione Rapida (5 minuti)

### 1. Informazioni Base del Sito
Modifica `_config.yml`:

```yaml
title: "Il Tuo Nome Sito"
description: "La tua descrizione personalizzata"
logo_text: "TuoBrand"
```

### 2. Sezione Hero
Sempre in `_config.yml`:

```yaml
hero:
  title: "Il Tuo Titolo Principale"
  subtitle: "La tua descrizione accattivante"
  cta_text: "Il Tuo Bottone"
```

### 3. Aggiungere i Tuoi Prodotti
Modifica `_data/products.yml` sostituendo i prodotti di esempio con i tuoi.

## Personalizzazione Avanzata

### Cambiare i Colori del Tema

Nel file `_sass/_variables.scss`:

```scss
// Colore principale (attualmente amber)
$primary-color: #your-color;
$primary-hover: #your-hover-color;

// Esempio per un tema blu:
$primary-color: #3b82f6;
$primary-hover: #2563eb;

// Esempio per un tema verde:
$primary-color: #10b981;
$primary-hover: #059669;
```

### Personalizzare i Font

1. **Cambiare il font principale**:
   
   In `_layouts/default.html`, sostituisci il link Google Fonts:
   ```html
   <link href="https://fonts.googleapis.com/css2?family=TuoFont:wght@300;400;500;600;700&display=swap" rel="stylesheet">
   ```

2. **Aggiornare la variabile CSS**:
   
   In `_sass/_variables.scss`:
   ```scss
   $font-family-base: 'TuoFont', sans-serif;
   ```

### Aggiungere Nuove Categorie

1. **Aggiungi la categoria** in `_data/categories.yml`:
   ```yaml
   - id: "nuova-categoria"
     name: "Nuova Categoria"
     active: false
   ```

2. **Aggiungi prodotti** con la nuova categoria in `_data/products.yml`:
   ```yaml
   - id: 9
     name: "Prodotto Nuova Categoria"
     category: "nuova-categoria"
     # ... altri campi
   ```

### Personalizzare il Layout

#### Modificare l'Header
Edita `_includes/header.html` per:
- Cambiare la struttura della navigazione
- Aggiungere elementi personalizzati
- Modificare il comportamento del menu mobile

#### Personalizzare il Footer
Edita `_includes/footer.html` per:
- Aggiungere nuove sezioni
- Modificare i link
- Cambiare le informazioni di contatto

### Aggiungere Nuove Sezioni

#### Esempio: Sezione Testimonianze

1. **Crea il file dati** `_data/testimonials.yml`:
   ```yaml
   - name: "Mario Rossi"
     text: "Ottimi prodotti e servizio eccellente!"
     rating: 5
     image: "/assets/images/testimonials/mario.jpg"
   ```

2. **Crea l'include** `_includes/testimonials.html`:
   ```html
   <section class="py-16 bg-gray-50">
     <div class="container mx-auto px-4">
       <h2 class="text-3xl font-bold text-center mb-12">Cosa Dicono i Nostri Clienti</h2>
       <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
         {% for testimonial in site.data.testimonials %}
         <div class="bg-white p-6 rounded-lg shadow-md">
           <div class="flex items-center mb-4">
             <img src="{{ testimonial.image }}" alt="{{ testimonial.name }}" class="w-12 h-12 rounded-full mr-4">
             <div>
               <h4 class="font-semibold">{{ testimonial.name }}</h4>
               <div class="flex text-amber-400">
                 {% for i in (1..testimonial.rating) %}
                 <i class="fas fa-star"></i>
                 {% endfor %}
               </div>
             </div>
           </div>
           <p class="text-gray-600">{{ testimonial.text }}</p>
         </div>
         {% endfor %}
       </div>
     </div>
   </section>
   ```

3. **Includi nella homepage** in `index.html`:
   ```html
   {% include hero.html %}
   {% include categories.html %}
   {% include products.html %}
   {% include testimonials.html %}
   {% include newsletter.html %}
   ```

### Personalizzare gli Stili CSS

#### Aggiungere Stili Personalizzati
Crea un nuovo file `_sass/_custom.scss` e importalo in `_sass/main.scss`:

```scss
// In _sass/main.scss
@import "variables";
@import "base";
@import "layout";
@import "custom";  // Il tuo file personalizzato
```

#### Esempio di Stili Personalizzati
```scss
// _sass/_custom.scss

// Animazioni personalizzate
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.fade-in-up {
  animation: fadeInUp 0.6s ease-out;
}

// Stili per card personalizzate
.custom-card {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border-radius: 15px;
  padding: 2rem;
  box-shadow: 0 10px 30px rgba(0,0,0,0.2);
  
  &:hover {
    transform: translateY(-5px);
    box-shadow: 0 15px 40px rgba(0,0,0,0.3);
  }
}
```

### Aggiungere Funzionalità JavaScript

#### Esempio: Wishlist
Aggiungi in `assets/js/main.js`:

```javascript
// Funzionalità Wishlist
function initWishlist() {
    const wishlistButtons = document.querySelectorAll('.wishlist-btn');
    let wishlist = JSON.parse(localStorage.getItem('wishlist')) || [];
    
    wishlistButtons.forEach(btn => {
        const productId = btn.getAttribute('data-product-id');
        
        // Aggiorna stato visuale
        if (wishlist.includes(productId)) {
            btn.classList.add('active');
        }
        
        btn.addEventListener('click', (e) => {
            e.preventDefault();
            
            if (wishlist.includes(productId)) {
                // Rimuovi dalla wishlist
                wishlist = wishlist.filter(id => id !== productId);
                btn.classList.remove('active');
                showNotification('Rimosso dalla wishlist', 'info');
            } else {
                // Aggiungi alla wishlist
                wishlist.push(productId);
                btn.classList.add('active');
                showNotification('Aggiunto alla wishlist', 'success');
            }
            
            localStorage.setItem('wishlist', JSON.stringify(wishlist));
        });
    });
}

// Aggiungi alla funzione DOMContentLoaded
document.addEventListener('DOMContentLoaded', function() {
    // ... altre inizializzazioni
    initWishlist();
});
```

### Integrazione con Servizi Esterni

#### Google Analytics
In `_layouts/default.html`:

```html
{% if jekyll.environment == 'production' %}
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=GA_TRACKING_ID"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'GA_TRACKING_ID');
</script>
{% endif %}
```

#### Mailchimp Newsletter
Modifica `_includes/newsletter.html`:

```html
<form action="https://your-mailchimp-url" method="post" id="mc-embedded-subscribe-form" name="mc-embedded-subscribe-form" class="flex" target="_blank" novalidate>
    <input type="email" value="" name="EMAIL" placeholder="{{ site.newsletter.placeholder }}" class="flex-grow px-4 py-3 rounded-l-lg border-t border-b border-l border-gray-300 focus:outline-none focus:ring-2 focus:ring-amber-500 focus:border-transparent" required>
    <button type="submit" name="subscribe" class="bg-amber-500 hover:bg-amber-600 text-white px-6 py-3 rounded-r-lg font-medium transition duration-300">
        {{ site.newsletter.button_text }}
    </button>
</form>
```

### Ottimizzazioni SEO Avanzate

#### Meta Tag Personalizzati
In `_layouts/default.html`:

```html
<head>
    <!-- Meta tag base -->
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    
    <!-- SEO Meta Tags -->
    <title>{% if page.title %}{{ page.title }} - {% endif %}{{ site.title }}</title>
    <meta name="description" content="{% if page.description %}{{ page.description }}{% else %}{{ site.description }}{% endif %}">
    <meta name="keywords" content="{% if page.keywords %}{{ page.keywords }}{% else %}{{ site.keywords }}{% endif %}">
    
    <!-- Open Graph -->
    <meta property="og:title" content="{% if page.title %}{{ page.title }} - {% endif %}{{ site.title }}">
    <meta property="og:description" content="{% if page.description %}{{ page.description }}{% else %}{{ site.description }}{% endif %}">
    <meta property="og:image" content="{% if page.image %}{{ page.image | absolute_url }}{% else %}{{ '/assets/images/og-image.jpg' | absolute_url }}{% endif %}">
    <meta property="og:url" content="{{ page.url | absolute_url }}">
    
    <!-- Twitter Card -->
    <meta name="twitter:card" content="summary_large_image">
    <meta name="twitter:title" content="{% if page.title %}{{ page.title }} - {% endif %}{{ site.title }}">
    <meta name="twitter:description" content="{% if page.description %}{{ page.description }}{% else %}{{ site.description }}{% endif %}">
    <meta name="twitter:image" content="{% if page.image %}{{ page.image | absolute_url }}{% else %}{{ '/assets/images/og-image.jpg' | absolute_url }}{% endif %}">
</head>
```

### Performance e Ottimizzazioni

#### Lazy Loading Immagini
Aggiungi in `assets/js/main.js`:

```javascript
// Lazy loading per immagini
function initLazyLoading() {
    const images = document.querySelectorAll('img[data-src]');
    
    const imageObserver = new IntersectionObserver((entries, observer) => {
        entries.forEach(entry => {
            if (entry.isIntersecting) {
                const img = entry.target;
                img.src = img.dataset.src;
                img.classList.remove('lazy');
                imageObserver.unobserve(img);
            }
        });
    });
    
    images.forEach(img => imageObserver.observe(img));
}
```

#### Minificazione CSS/JS
Per la produzione, aggiungi in `_config.yml`:

```yaml
# Minificazione per produzione
sass:
  style: compressed

# Plugin per minificazione
plugins:
  - jekyll-feed
  - jekyll-sitemap
  - jekyll-minifier  # Aggiungi al Gemfile
```

## Risoluzione Problemi Comuni

### Il sito non si carica
1. Verifica che tutte le dipendenze siano installate: `bundle install`
2. Controlla la sintassi YAML nei file di configurazione
3. Verifica i percorsi delle immagini

### Gli stili non si applicano
1. Assicurati che il file `assets/css/main.scss` abbia il front matter
2. Controlla la sintassi SCSS
3. Verifica l'ordine di importazione dei file

### JavaScript non funziona
1. Controlla la console del browser per errori
2. Verifica che jQuery o altre dipendenze siano caricate
3. Assicurati che il DOM sia completamente caricato

## Supporto

Per ulteriore supporto:
1. Consulta la documentazione Jekyll ufficiale
2. Verifica i file di esempio inclusi nel template
3. Testa sempre le modifiche in locale prima del deploy

