namespace :book do
  desc 'prepare build'
  task :prebuild do
    Dir.mkdir 'images' unless Dir.exists? 'images'
    Dir.glob("book/*/images/*").each do |image|
      FileUtils.copy(image, "images/" + File.basename(image))
    end
  end

  desc 'build basic book formats'
  task :build => :prebuild do
    puts "Converting to HTML..."
    `bundle exec asciidoctor css-3d-effects.asciidoc`
    puts " -- HTML output at css-3d-effects.html"

    puts "Converting to EPub..."
    `bundle exec asciidoctor-epub3 css-3d-effects.asciidoc`
    puts " -- Epub output at css-3d-effects.epub"

    puts "Converting to Mobi (kf8)..."
    `bundle exec asciidoctor-epub3 -a ebook-format=kf8 css-3d-effects.asciidoc`
    puts " -- Mobi output at css-3d-effects.mobi"

    puts "Converting to PDF... (this one takes a while)"
    `bundle exec asciidoctor-pdf css-3d-effects.asciidoc 2>/dev/null`
    puts " -- PDF  output at css-3d-effects.pdf"
  end
end

task :default => "book:build"