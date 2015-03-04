require 'rake/packagetask'

desc "Completely empty /build and /pkg"
task :clobber do
  puts "## Completely empty /build and /pkg"
  sh "rm -rf build pkg"
end

desc "Build the website from source"
task :build do
  puts "## Building website"
  status = system("middleman build --clean")
  puts status ? "OK" : "FAILED"
end

task :build_package do
  # see http://rake.rubyforge.org/classes/Rake/PackageTask.html
  desc 'precompiles the assets and builds a tarball of the middleman application'
  revision = `git rev-parse HEAD`.delete!("\n")[0..8]
  Rake::PackageTask.new("tingba-package", revision) do |p|
    p.need_zip = true
    p.package_files.include("build/**/*")
  end
  Rake::Task['package'].invoke
end

task default: [:clobber, :build, :build_package]
