# frozen_string_literal: true

# Build Prince Cooks 4 U site
# Usage: rake build

require 'erb'
require 'json'

# Helper logic for the actual Rake tasks
module Site
  module_function

  def popups
    File.read('popups.json')
        .then { |json| JSON.parse(json, symbolize_names: true) }
        .map { |popup| Popup.new(**popup) }
  end

  def template
    ERB.new(File.read('index.html.erb'), trim_mode: '-')
  end

  def output
    'index.html'
  end

  # noinspection RubyUnusedLocalVariable
  def erb(popups)
    output = Site.template.result(binding)

    File.write(Site.output, output)

    output
  end

  Popup = Data.define(:name, :slug, :slogan, :offerings, :extra)
end

desc 'Build site file'
file 'index.html' => %w[index.html.erb popups.json] do
  popups = Site.popups

  Site.erb(popups)
end

desc 'Build the whole site'
task build: ['index.html']

desc 'Build and push a new version of the site'
task release: :build do
  # TODO
end

task dev: ['index.html'] do
  sh 'open index.html'
end
