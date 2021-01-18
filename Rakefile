require "rake/testtask"
require "rubocop/rake_task"
require "rdoc/task"

task default: [:test, :rubocop]

task :clean_log do
  File.unlink "log/test.log" if File.exist? "log/test.log"
end

# fix for NoMethodError: undefined method `last_comment'
module LastComment
  def last_comment
    last_description
  end 
end
Rake::Application.send :include, LastComment

Rake::TestTask.new test: :clean_log do |t|
  t.libs << "test"
  t.pattern = "test/**/*_test.rb"
end

RuboCop::RakeTask.new(:rubocop) do |task|
  task.patterns = ["**/*.rb", "Rakefile", "Gemfile", "mongoid_enum.gemspec"]
  task.fail_on_error = false
end

RDoc::Task.new do |rdoc|
  rdoc.main = "README.md"
  rdoc.rdoc_dir = "doc"
  rdoc.rdoc_files.include("README.md", "lib/**/*.rb")
  rdoc.markup = "tomdoc"
end
