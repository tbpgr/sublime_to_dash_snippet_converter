require 'toml'
require 'logger'
require 'fileutils'
require 'dotenv'
require 'xmlsimple'
Dotenv.load

namespace :dash do
  DASH_PATH = './dash'
  SUBLIME_PATH = './sublime'
  SYNTAX = 'None'
  TAG = 'Emoji'

  module XmlKeys
    CONTENT = "content"
    TAB_TRIGGER = "tabTrigger"
  end

  module Fields
    TITLE = 'title'
    BODY = 'body'
    SYNTAX = 'syntax'
    TAG = 'tag'
  end

  def sublime_convert
    initialize_log
    @logger.debug('start convert snippets')
    snippets = load_sublime_snippets
    snippets.each do |snippet|
      outer = {}
      inner = {}
      title = snippet[XmlKeys::TAB_TRIGGER].first
      inner[:title] = "#{title};;"
      inner[:body] = snippet[XmlKeys::CONTENT].gsub(/\n/, '')
      inner[:syntax] = SYNTAX
      inner[:tag] = TAG
      outer[:snippet] = inner
      filename = title
      File.open("#{DASH_PATH}/#{filename}.toml", "w") {|e|e.puts TOML.dump(outer) }
      @logger.debug("\t complete output #{DASH_PATH}/#{filename}.toml ")
    end
    @logger.debug('finish convert snippets')
  end

  private

  def initialize_log
    @logger = Logger.new(STDOUT)
    level = ENV['LOG_LEVEL']
    @logger.level = Object.const_get("Logger::#{level}")
    @logger.formatter =-> (severity, datetime, progname, message) {
      "#{datetime.strftime('%Y/%m/%d %H:%M:%S')} - #{level} - #{message}\n"
    }
  end

  def load_sublime_snippets
    Dir.glob("#{SUBLIME_PATH}/*.sublime-snippet").each_with_object([]) do |f, memo|
      memo << XmlSimple.xml_in(File.read(f))
    end
  end

  desc 'convert sublime snippets to dash snippets'
  task :sublime_convert do
    sublime_convert
  end
end
