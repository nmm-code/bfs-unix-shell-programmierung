#####################################################################################
#	ueb05 : Makefile
#	Unix/Shell Programmierung
#	
#	Diese Makefile erstellt ein Kommentar für jedes Shell Skript im Verzeichnis.
#	Außerden werden die Skripte je nach bedarf in einen anderes 
#	Format umwandelt und zusammengefasst.
#
#	@author Nima, Max
#
#	| Siehe die Hilfe: |
#	V                  V
#####################################################################################

###########################################
# Target: all
# alias für index
###########################################
.PHONY: all
all: index

###########################################
# Target: help
# gibt auf stdout die Hilfe aus
###########################################
.PHONY: help
help:
	@echo 'Makefile to create a code documentation of shell files using markdown.'
	@echo ''
	@echo 'VARIABLES'
	@echo '  PRETEXT - text prepended to every markdown file'
	@echo '            (default="# Code Documentation")'
	@echo ''
	@echo 'TARGETS'
	@echo '  all   - default target, does the same as index target'
	@echo '  index - create all md files, html pages and an index.htm'
	@echo '  html  - create all md files and html pages'
	@echo '  md    - create all md files'
	@echo '  help  - display this help and exit'
	@echo '  clean - remove all generated files'
	
#################################################################################
# Variablen
PRETEXT := "\# Code Documentation"

LIST_SH_FILES := $(wildcard *.sh) # Alle Datein die .sh enden 
LIST_MD_FILES := $(wildcard *.md) # Alle Datein die .md enden 

# Liste die bei md erstellt werden müssen
ALL_MD_FILES := $(subst .sh,.md,$(LIST_SH_FILES))
# Liste die bei html erstellt werden müssen
ALL_HTML_FILES := $(sort $(subst .md,.html,$(LIST_MD_FILES)) $(subst .md,.html,$(ALL_MD_FILES)))

# Alle generierten md Dateien
GENERATED_MD_FILES := $(subst .sh,.md,$(wildcard *.sh))
# Alle generierten html Dateien
GENERATED_HTML_FILES := $(subst .md,.html,$(wildcard *.md))

# Die Index Datei
INDEX := "index.htm"

###########################################
# Target: md
# - wandelt jede SH-Datei zu einer MD-Datei um
###########################################
.PHONY: md
md: $(ALL_MD_FILES)

$(ALL_MD_FILES): 
	@echo $(PRETEXT) > $@
	@chmod +x shelltomd
	@cat $(subst .md,.sh,$@) | ./shelltomd >> $@


###########################################
# Target: html
# - wandelt jede SH-Datei zu einer MD-Datei um
# - wandelt jede MD-Datei zu einer HTML-Datei um
###########################################
.PHONY: html
html: md $(ALL_HTML_FILES)

$(ALL_HTML_FILES): 
	@chmod +x Markdown.pl
	@cat $(subst .html,.md,$@) | ./Markdown.pl > $@

###########################################
# Target: html
# erstellt eine index datei, die alle HTML-Seiten im Verzeichnis zusammenfasst
###########################################

.PHONY: index 
index: html 
	@chmod +x genindex
	@./genindex > $(INDEX) 


###########################################
# Target: clean
# löscht alle generierte Dateien im Verzeichnis
###########################################
.PHONY: clean
clean:
	@rm -f $(GENERATED_HTML_FILES) $(GENERATED_MD_FILES) $(INDEX) 


.SECONDARY:
