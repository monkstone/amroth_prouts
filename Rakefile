
namespace :book do
  desc 'build basic book formats'
  task :build do

    `cp prout.adoc prout.adoc.bak`
    begin
      version_string = '0.1'
      text = File.read('prout.adoc')
      new_contents = text.gsub("$$VERSION$$", version_string).gsub("$$DATE$$", Time.now.strftime("%Y-%m-%d"))
      File.open("prout.adoc", "w") {|file| file.puts new_contents }

      puts "Converting to HTML..."
      `bundle exec asciidoctor prout.adoc`
      puts " -- HTML output at prout.html"

      puts "Converting to EPub..."
      `bundle exec asciidoctor-epub3 prout.adoc`
      puts " -- Epub output at prout.epub"

      puts "Converting to Mobi (kf8)..."
      `bundle exec asciidoctor-epub3 -a ebook-format=kf8 prout.adoc`
      puts " -- Mobi output at prout.mobi"

      puts "Converting to PDF... (this one takes a while)"
      `bundle exec asciidoctor-pdf prout.adoc 2>/dev/null`
      puts " -- PDF output at prout.pdf"

    ensure
      `mv prout.adoc.bak prout.adoc`
    end
  end
end

task :default => "book:build"
