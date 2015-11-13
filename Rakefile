require "rubygems"

desc "Deploy to Github Pages"
task :deploy do
  puts "## Deploying to Github Pages"

  puts "## Generating site"
  # system "grunt build"

  system "git checkout master"
  system "rm -rf /tmp/_site"
  system "mkdir /tmp/_site"
  system "jekyll build"
  system "cp -a _site/. /tmp/_site/"

  cd "_site" do
    system "git add -A"

    message = "Site updated at #{Time.now.utc}"
    puts "## Commiting: #{message}"
    system "git commit -m \"#{message}\""

    puts "## Pushing generated site"
    system "git push"

    cd "../" do

      system "git checkout gh-pages"
      system 'ls | grep -v ".git" | xargs rm -rf'

      puts "## Copying gerenated site"
      system "cp -a /tmp/_site/* ./"

      system "git add -A"

      message = "Site updated at #{Time.now.utc}"
      puts "## Commiting: #{message}"
      system "git commit -m \"#{message}\""

      puts "## Pushing generated site"
      system "git push origin gh-pages"

      puts "## Deploy Complete!"
      system "git checkout master"

    end
  end
end

name = ENV["name"] || ""

desc "Create a new post"
task :create do

  header = "---\n"
  header += "layout: post\n"
  header += "title: \n"
  header += "slug: "+name+"\n"
  header += "date:   "+Time.now.strftime("%Y-%m-%d")+" 19:00:00\n"
  header += "categories: \n"
  header += "  - Manutenção\n"
  header += "tags: [fusca]\n"
  header += "images:\n"
  header += "  - images/@stock/blog-4.jpg\n"
  header += "excerpt: \n"
  header += "---"

  File.write('_posts/' + Time.now.strftime("%Y-%m-%d")+'-'+name+'.md', header)

  puts 'Created: _posts/' + Time.now.strftime("%Y-%m-%d")+'-'+name+'.md';

end
