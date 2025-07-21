# Cartella Immagini

Questa cartella contiene tutte le immagini utilizzate nel template.

## Struttura Consigliata

```
assets/images/
├── products/           # Immagini dei prodotti
│   ├── smartphone-xyz-pro.jpg
│   ├── robot-aspirapolvere.jpg
│   └── ...
├── logos/              # Loghi e branding
│   ├── logo.png
│   └── favicon.ico
├── hero/               # Immagini per la sezione hero
│   └── hero-bg.jpg
└── misc/               # Altre immagini
    └── placeholder.jpg
```

## Linee Guida per le Immagini

### Immagini Prodotti
- **Formato**: JPG o PNG
- **Dimensioni**: 400x400px (quadrate) per consistenza
- **Qualità**: Ottimizzate per web (< 100KB quando possibile)
- **Naming**: Usa nomi descrittivi con trattini (es: `smartphone-xyz-pro.jpg`)

### Ottimizzazione
- Comprimi le immagini prima dell'upload
- Usa formati moderni come WebP quando supportato
- Considera l'implementazione di lazy loading per performance

### Placeholder
Se non hai immagini specifiche, il template mostrerà automaticamente un'icona placeholder SVG.

## Note
- Aggiorna i percorsi delle immagini nel file `_data/products.yml`
- Assicurati che i nomi dei file corrispondano esattamente a quelli specificati nei dati
- Per immagini di grandi dimensioni, considera l'uso di un CDN

