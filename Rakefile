require "rubygems"
require "tmpdir"
require "bundler/setup"

task :default => [:build]

desc "Build the static site"
task :build do
  puts "Building project"
  system "rm -rf build/*"
  try "middleman build"
  puts "Build complete 🛠"
end

GITHUB_REPONAME = "algorithmiaio/api-docs"

desc "Generate and publish blog to gh-pages"
namespace :shippable do
  task :publish do

    Rake::Task["build"].invoke

    Dir.mktmpdir do |tmp|
      cp_r "build/.", tmp

      pwd = Dir.pwd
      Dir.chdir tmp

      system "git init"
      system "git add ."
      message = "Site updated at #{Time.now.utc}"
      system "git commit -m #{message.inspect}"
      system "git remote add origin git@github.com:#{GITHUB_REPONAME}.git"
      system "git push origin master:refs/heads/gh-pages --force"
      system "echo Site updated! 💃"

      Dir.chdir pwd
    end
  end
end

## Helper so we fail as soon as a command fails.
def try(command)
  system command
  if $? != 0 then
    raise "Command: `#{command}` exited with code #{$?.exitstatus}"
  end
end