# frozen_string_literal: true

task all: %i[build lint]

desc 'Build'
task :build do
  sh 'scedilla _.sh >_.html'
end

desc 'Clean'
task :clean do
  rm_rf %w[.sass-cache _site]
end

desc 'Lint'
task :lint do
  if ENV['lang'].nil? || ENV['lang'] == 'sh'
    sh %(shellcheck $(find -type f -and -not -path './.git/*' | xargs file --mime-type | grep text/x-shellscript$ | cut -f1 -d:)) # rubocop:disable Metrics/LineLength
  end
  sh 'rubocop'           if ENV['lang'].nil? || ENV['lang'] == 'rb'
  sh 'markdownlint *.md' if ENV['lang'].nil? || ENV['lang'] == 'md'
end

desc 'Serve'
task :serve do
  sh 'jekyll serve'
end

task default: :build
