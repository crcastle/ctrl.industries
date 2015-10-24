require "rubygems"
require "bundler/setup"

git_repo       = "git@github.com:crcastle/ctrl.industries.git"
deploy_branch  = "gh-pages"
public_dir      = "_site"       # compiled site directory
source_dir      = "."           # source file directory
deploy_dir      = "_deploy"     # deploy directory (for Github pages deployment)

deploy_path     = "#{ENV['TMPDIR']}#{deploy_dir}"

desc "Generate jekyll site"
task :generate do
  # raise "### You haven't set anything up yet. First run `rake install` to set up an Octopress theme." unless File.directory?(source_dir)
  puts "## Generating Site with Jekyll"
  # system "compass compile --css-dir #{source_dir}/stylesheets"
  system "bin/jekyll build --source #{source_dir} --destination #{public_dir}"
end

desc "Generate website and deploy"
task :gen_deploy => [:generate, :deploy] do
end

desc "Deploy public directory to github pages"
multitask :deploy do
  puts "## Deploying branch to Github Pages "
  puts "## Cloning current Github Pages repo "
  rm_rf "#{deploy_path}"
  mkdir_p "#{deploy_path}"
  cd "#{deploy_path}" do
    Bundler.with_clean_env do
      system "git clone #{git_repo} jekyll-deploy"
    end
  end
  puts "\n## Copying #{public_dir} to #{deploy_path}/jekyll-deploy"
  cd "#{deploy_path}/jekyll-deploy" do
    system "git checkout #{deploy_branch}"
    cp_r "#{Rake.application.original_dir}/#{public_dir}/.", "."
    system "git add -A"
    host = `scutil --get LocalHostName`
    message = "Site updated at #{Time.now.utc} from #{host}"
    puts "\n## Committing: #{message}"
    system "git commit -m \"#{message}\""
    puts "\n## Pushing generated #{deploy_path} website"
    Bundler.with_clean_env { system "git push origin #{deploy_branch}" }
    puts "\n## Github Pages deploy complete, cleaning up "
  end
  rm_rf "#{deploy_path}"
  puts "\n## Done. "
end
