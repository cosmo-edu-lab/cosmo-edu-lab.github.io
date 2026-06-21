source "https://rubygems.org"

# Same gem GitHub Pages uses to build your site, so your local
# preview matches exactly what GitHub will publish.
gem "github-pages", group: :jekyll_plugins

# Windows/JRuby compatibility (harmless to leave in on macOS/Linux)
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", "~> 1.2"
  gem "tzinfo-data"
end

gem "wdm", "~> 0.1.1", :platforms => [:mingw, :x64_mingw, :mswin]

# Lock `http_parser.rb` for Windows, JRuby builds
gem "http_parser.rb", "~> 0.6.0", :platforms => [:jruby]
