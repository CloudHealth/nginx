<<<<<<< HEAD
#!/usr/bin/env rake

require 'foodcritic'
require 'kitchen'
require 'rake/clean'
require 'rspec/core/rake_task'
require 'rubocop/rake_task'

CLEAN.include %w(.kitchen/ coverage/ doc/)
CLOBBER.include %w(Berksfile.lock Gemfile.lock .yardoc/)

# Default tasks to run when executing `rake`
task default: %w(style spec)
=======
require 'rspec/core/rake_task'
require 'rubocop/rake_task'
require 'foodcritic'
require 'kitchen'
>>>>>>> 421e2fee2750c39da254bf1dfaed60f5420f08f6

# Style tests. Rubocop and Foodcritic
namespace :style do
  desc 'Run Ruby style checks'
<<<<<<< HEAD
  RuboCop::RakeTask.new(:ruby)

  desc 'Run Chef style checks'
  FoodCritic::Rake::LintTask.new(:chef) do |t|
    t.options = { fail_tags: ['any'] }
=======
  Rubocop::RakeTask.new(:ruby)

  desc 'Run Chef style checks'
  FoodCritic::Rake::LintTask.new(:chef) do |t|
    t.options = {
      fail_tags: ['any'],
      tags: [
        '~FC005',
        '~FC015',
        '~FC023',
      ]
    }
>>>>>>> 421e2fee2750c39da254bf1dfaed60f5420f08f6
  end
end

desc 'Run all style checks'
task style: ['style:chef', 'style:ruby']

# Rspec and ChefSpec
<<<<<<< HEAD
desc 'Run ChefSpec examples'
RSpec::Core::RakeTask.new(:spec) do |t|
  t.verbose = false
end

desc 'Find notes in code'
task :notes do
  puts `egrep --exclude=Rakefile --exclude=*.log -n -r -i '(TODO|FIXME|OPTIMIZE)' .`
end
=======
desc "Run ChefSpec examples"
RSpec::Core::RakeTask.new(:spec)

# Integration tests. Kitchen.ci
namespace :integration do
  desc 'Run Test Kitchen with Vagrant'
  task :vagrant do
    Kitchen.logger = Kitchen.default_file_logger
    Kitchen::Config.new.instances.each do |instance|
      instance.test(:always)
    end
  end
  
  desc 'Run Test Kitchen with cloud plugins'
  task :cloud do
    run_kitchen = true
    if ENV['TRAVIS'] == 'true' && ENV['TRAVIS_PULL_REQUEST'] != 'false'
      run_kitchen = false
    end
    
    if run_kitchen
      Kitchen.logger = Kitchen.default_file_logger
      @loader = Kitchen::Loader::YAML.new(project_config: './.kitchen.cloud.yml')
      config = Kitchen::Config.new( loader: @loader)
      config.instances.each do |instance|
        instance.test(:always)      
      end      
    end
  end
end

desc 'Run all tests on Travis'
task travis: ['style', 'spec', 'integration:cloud']

# Default
task default: ['style', 'spec', 'integration:vagrant']
>>>>>>> 421e2fee2750c39da254bf1dfaed60f5420f08f6
