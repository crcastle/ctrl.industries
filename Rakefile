require "rubygems"
require "bundler/setup"

git_repo       = "git@github.com:crcastle/ctrl.industries.git"
deploy_default = "push"
deploy_branch  = "gh-pages"

## -- Misc Configs -- ##

public_dir      = "_site"       # compiled site directory
source_dir      = "."           # source file directory
deploy_dir      = "_deploy"     # deploy directory (for Github pages deployment)
blog_index_dir  = 'source'      # directory for your blog's index page (if you put your index in source/blog/index.html, set this to 'source/blog')
stash_dir       = "_stash"      # directory to stash posts for speedy generation
posts_dir       = "_posts"      # directory for blog files

deploy_path     = "#{ENV['TMPDIR']}#{deploy_dir}"

desc "Generate jekyll site"
task :generate do
  # raise "### You haven't set anything up yet. First run `rake install` to set up an Octopress theme." unless File.directory?(source_dir)
  puts "## Generating Site with Jekyll"
  # system "compass compile --css-dir #{source_dir}/stylesheets"
  system "bin/jekyll build --source #{source_dir} --destination #{public_dir}"
end

desc "Default deploy task"
task :deploy do
  # Rake::Task[:copydot].invoke(source_dir, public_dir)
  Rake::Task["#{deploy_default}"].execute
end

desc "Generate website and deploy"
task :gen_deploy => [:generate, :deploy] do
end

desc "deploy public directory to github pages"
multitask :push do
  puts "## Deploying branch to Github Pages "
  puts "## Cloning current Github Pages repo "
  rm_rf "#{deploy_path}"
  mkdir_p "#{deploy_path}"
  cd "#{deploy_path}" do
    Bundler.with_clean_env do
      system "git clone #{git_repo} jekyll-deploy"
    end
  end
  # (Dir["#{deploy_dir}/*"]).each { |f| rm_rf(f) }
  # Rake::Task[:copydot].invoke(public_dir, deploy_dir)
  puts "\n## Copying #{public_dir} to #{deploy_path}"
  cd "#{deploy_path}/jekyll-deploy" do
    system "git checkout #{deploy_branch}"
    cp_r "#{public_dir}/.", "."
    system "git add -A"
    host = system("scutil --get LocalHostName")
    message = "Site updated at #{Time.now.utc} from #{host}"
    puts "\n## Committing: #{message}"
    system "git commit -m \"#{message}\""
    puts "\n## Pushing generated #{deploy_path} website"
    Bundler.with_clean_env { system "git push origin #{deploy_branch}" }
    puts "\n## Github Pages deploy complete"
  end
end
