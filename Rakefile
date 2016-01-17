master_dir = "healthhackconf.github.io.master"
work_dir = "healthhackconf.github.io"

desc "All deploy"
task :alldeploy => [:push_src, :clean, :build, :deploy]

desc "Build all posts and pages."
task :build do
  sh "jekyll build -t"
end

desc "Clean _site"
task :clean do
  sh "rm -rf _site/*"
end

# Usage: rake deploy
desc "Begin a push static file to GitHub"
task :deploy do
  puts "! Copy static file from _site to kkd.github.com.master"
  sh "rsync -av --delete _site/* ../#{master_dir}/"
  puts "! Change directory master"
  cd "../#{master_dir}" do
    puts "! Push to master branch of GitHub"
    sh "git add --all *"
    message = "deploy at #{Time.now}"
    begin
      sh "git commit -m \"#{message}\""
      sh "git push origin master:master"
      sh "cd ../#{work_dir}"
    rescue Exception => e
      puts "! Error - git command abort"
      exit -1
    end
  end
end

# Usage: rake push master
desc "Begin a push sources to Github"
task :push_src do
  puts "! Push to master branch of GitHub"
  begin
    sh "git push origin master"
  rescue Exception => e
    puts "! Error - git command abort"
    exit -1
  end
end