require 'rubygems'
require 'bundler/setup'

require 'rake/clean'

require 'cucumber/rake/task'
Cucumber::Rake::Task.new :features
task :default => :features

require 'rspec/core/rake_task'
RSpec::Core::RakeTask.new :spec
task :default => :spec

version = File.exists?('VERSION') ? File.read('VERSION').strip : ''

require 'rdoc/task'
RDoc::Task.new :doc do |rdoc|
  rdoc.rdoc_dir = 'doc'
  rdoc.title = "Rack::Csrf #{version}"
  rdoc.main = 'README.rdoc'
  rdoc.rdoc_files.include('README.rdoc', 'LICENSE.rdoc')
  rdoc.rdoc_files.include('lib/**/*.rb')
end

require 'jeweler'
Jeweler::Tasks.new do |gem|
  gem.name = 'rack_csrf'
  gem.summary = 'Anti-CSRF Rack middleware'
  gem.description = 'Anti-CSRF Rack middleware'
  gem.license = 'MIT'
  gem.authors = 'Emanuele Vicentini, Matt King'
  gem.email = 'emanuele.vicentini@gmail.com, mking@mking.me'
  gem.homepage = 'https://github.com/mattking17/rack_csrf'
  gem.rubyforge_project = 'rackcsrf'
  gem.required_ruby_version = '>= 1.8.7'
  # dependencies defined in Gemfile
  gem.rdoc_options << '--line-numbers' << '--inline-source' << '--title' <<
    "Rack::Csrf #{version}" << '--main' << 'README.rdoc'
  gem.test_files.clear
end

Jeweler::GemcutterTasks.new

desc <<-EOD
Shows the changelog in Git between the given points.

start -- defaults to the current version tag
end   -- defaults to HEAD
EOD
task :changes, [:start, :end] do |t, args|
  args.with_defaults :start => "v#{Rake.application.jeweler.version}",
    :end => 'HEAD'
  repo = Git.open Rake.application.jeweler.git_base_dir
  repo.log(nil).between(args.start, args.end).each do |c|
    puts c.message.split($/).first
  end
end
