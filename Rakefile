require 'html-proofer'

task :build do
  sh "jekyll build"
end

task :serve do
  sh "jekyll serve"
end

task :htmlproofer do
  HTML::Proofer.new("./_site",
                    {:href_ignore => [/http(s?):\/\/(.*)\.freifunk-dresden.de/, /^http:\/\/192\.168\..*/]}).run
end

task :trailing_spaces do
  output = `find pages _posts _sass -type f -exec egrep -l \" +$\" {} \\;`
  if output.strip != "" then
    raise "files containing trailing spaces:\n" + output
  end
end

task :test => :build do
  Rake::Task['trailing_spaces'].invoke
  Rake::Task['htmlproofer'].invoke
end

task :clean do
  sh "bundle exec rm -R ./_site || true"
end
