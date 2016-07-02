require 'open3'
require 'yaml'
#require 'io'
require  'rake/clean'


def valida_yaml
  metadados = IO.read("metadados.yaml")
  puts YAML.load(metadados)
end

task :compile do
  system "latexmk --xelatex trabalho-academico.tex"
end


task :custom do
  puts "Gerando preambulo-customizado.tex"
  system "pandoc -f markdown --data-dir=. --template=abntex2-preambulo metadados.yaml -o preambulo-customizado.tex"
  puts "Gerando pretextual-customizado.tex"
  system "pandoc -f markdown --data-dir=. --template=abntex2-pretextual metadados.yaml -o pretextual-customizado.tex"
  puts "Gerando postextual-customizado.tex"
  system "pandoc -f markdown --data-dir=. --template=abntex2-postextual metadados.yaml -o postextual-customizado.tex"

end

task :tex => [:custom] do
  valida_yaml
  #system "pandoc --smart --standalone --wrap=none --data-dir=. -f markdown -t latex trabalho-academico.md metadados/matedados.yaml -o trabalho-academico.tex"
# --template=templates/default.latex 
# --filter=pandoc-citeproc 
# --template=abntex2-trabalho-academico
  system "pandoc -f markdown -s --normalize --chapter  --include-in-header=preambulo-customizado.tex  --include-before-body=pretextual-customizado.tex --include-after-body=postextual-customizado.tex metadados.yaml trabalho-academico.md  -o trabalho-academico.tex"
end

CLEAN.include(["trabalho-academico.aux","trabalho-academico.idx","trabalho-academico.lof", "trabalho-academico.pdf","trabalho-academico.fdb_latexmk","trabalho-academico.ilg","trabalho-academico.log","*.*~","trabalho-academico.tex","trabalho-academico.fls","trabalho-academico.ind","trabalho-academico.lot","trabalho-academico.out","trabalho-academico.toc","preambulo-customizado.tex","pretextual-customizado.tex"])


task :default => [:tex, :compile]
