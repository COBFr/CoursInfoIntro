#!/bin/make -f
OUT		=0_out/
CONFIG	=$(shell find . -iname "*.t2trc")
CSS		=$(patsubst %.css,${OUT}%.css,$(wildcard *.css))
DATE     =$(shell date +%Y%m%d-%H%M%S)
SOURCE=	$(shell find . -iname "*.t2t"| sed -e 's@^\./@@')
CIBLE		=$(patsubst %.t2t,${OUT}%.html,${SOURCE})
CIBLEDOS	=$(shell echo ${CIBLE}|xargs dirname|sort -u)
DOS		=${OUT} ${CIBLEDOS}
CC       =txt2tags -o $@ $<

.PRECIOUS: ${SOURCE}

.PHONY: all
all: html

.PHONY: html
html : dos css ${CIBLE} ${CONFIG}

${OUT}%.html: %.t2t
	@mkdir -vp $(shell dirname $@)
	@${CC}

#[[ -d $(shell dirname $@) ]] || mkdir $(shell dirname $@)

.PHONY: dos
dos : ${DOS}
${DOS}:
	@echo -n "Création du dossier : "
	mkdir -p $@

.PHONY: css
css : ${CSS} ${DOS}
${OUT}%.css : %.css
	@echo -n "Copie du fichier : $@"
	@cat $< > $@

.PHONY: clean
clean :
	@echo "Néttoyage des fichiers inutiles"

#	rm -rf ${OUT}*.aux ${OUT}*.dvi ${OUT}*.log ${OUT}*.ps ${OUT}*.toc ${OUT}*.tns ${OUT}*.idx
#	rm -rf ${OUT}*.maf ${OUT}*.minAtt ${OUT}*.minDec ${OUT}*.minTsk ${OUT}*.mtc* ${OUT}*.out ${OUT}*.cld ${OUT}*.minCld

.PHONY: mrpropre
mrpropre : clean
	rm -rf ${OUT}

.PHONY: install
install:
	lftp ftp.educanet2.ch -e "mirror -e -R ../0_out . ; quit"

#	lftp ecole.co-belluard.ch -e "mirror -e -R ../0_out /Sites/infintro ; quit"


.PHONY: test
test :
	@echo "    source : ${SOURCE}"
	@echo "    cibles : ${CIBLE}"
	@echo "  dossiers : ${CIBLEDOS}"


