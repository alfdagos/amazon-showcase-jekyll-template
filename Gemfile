source "https://rubygems.org"

# Usa la gemma github-pages per assicurare la compatibilità
gem "github-pages", group: :jekyll_plugins

# Solo per Windows o JRuby
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1", "< 3"
  gem "tzinfo-data"
end

# Migliora le performance su Windows
gem "wdm", "~> 0.1.1", platforms: [:mingw, :x64_mingw, :mswin]

# Lock specifico per JRuby
gem "http_parser.rb", "~> 0.6.0", platforms: [:jruby]
