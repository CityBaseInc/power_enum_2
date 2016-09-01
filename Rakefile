require "gemfury/tasks"
begin
  require "jeweler"
  Jeweler::Tasks.new do |gem|
    gem.name = "power_enum"
    gem.summary = "Allows you to treat instances of your ActiveRecord models as though they were an enumeration of values"
    gem.description = <<-EOF
Power Enum allows you to treat instances of your ActiveRecord models as though they were an enumeration of values.
It allows you to cleanly solve many of the problems that the traditional Rails alternatives handle poorly if at all.
It is particularly suitable for scenarios where your Rails application is not the only user of the database, such as
when it's used for analytics or reporting.
    EOF
    gem.email = "arthur.shagall@gmail.com"
    gem.homepage = "http://github.com/albertosaurus/power_enum_2"
    gem.authors = ["Trevor Squires", "Pivotal Labs", 'Arthur Shagall', 'Sergey Potapov']
    gem.files = Dir["{lib}/**/*"]
    gem.signing_key = 'gem-private_key.pem' if File.exists?('gem-private_key.pem')
    gem.cert_chain = ['gem-public_cert.pem']
    gem.licenses = ['MIT']
  end
rescue
  puts "Jeweler or one of its dependencies is not installed."
end


begin
  require 'rspec/core/rake_task'
  task :default => :spec

  RSpec::Core::RakeTask.new
rescue
  puts "rspec gem is not installed"
end

namespace :version do

  desc "create a new version, create tag and push to github"

  task :patch_release do
    Rake::Task['version:bump:patch'].invoke
    Rake::Task['git:release'].invoke
  end

  task :minor_release do
    Rake::Task['version:bump:minor'].invoke
    Rake::Task['git:release'].invoke
  end

  task :major_release do
    Rake::Task['version:bump:major'].invoke
    Rake::Task['git:release'].invoke
  end

end

Rake::Task['release'].clear

desc "Tag and release to gemfury under the 'citybase' organization"
task 'release' => 'release:source_control_push'  do
  Rake::Task['fury:release'].invoke('power_enum.gemspec', 'citybase')
end
