require 'fileutils'

task default: :install

task :install do
  scripts = Dir['*'] - %w{script vendor common.rb Gemfile Gemfile.lock LICENSE.txt Rakefile README.md}
  target  = ENV["TARGET"] || ask_for_target_dir
  File.directory?(File.expand_path(target)) or abort("Install directory isn't a directory")

  scripts.each do |filename|
    puts "  Linking #{target}/#{filename}"
    path_to_target = File.join File.expand_path(target), filename
    if File.exist?(path_to_target) && File.symlink?(path_to_target)
      FileUtils.rm(path_to_target)
    end
    FileUtils.symlink File.absolute_path(filename), path_to_target
  end
end

def ask_for_target_dir
  default_target = ENV["TARGET"] || "usr/local/bin"
  puts "Directory to install? (needs to be in your $PATH; #{default_target} is the default, hit enter to use that)"
  answer = STDIN.gets.chomp
  (answer unless answer == "") || default_target
end
