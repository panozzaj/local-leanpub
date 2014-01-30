# https://github.com/guard/guard#readme

ignore /_generated/

contents_filename = 'contents.txt'
chapters = File.read(contents_filename).split("\n")
images = Dir['images/**']
puts chapters
files = [*chapters, 'build', *images, contents_filename]
file_string = files.join("|")
puts file_string

guard 'process', command: './build' do
  watch(%r{#{file_string}})
end
