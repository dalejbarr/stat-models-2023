SHELL := /bin/bash
include ../.make_config
DEST := ../$(htmldir)

default : 
	emacs --batch -l org \
		-l publish.el \
		index.org \
		--eval='(org-publish-project "org")'

deploy : default
	rsync -av --delete ../html/* hh1-web.psy.gla.ac.uk:/web/web2/talklab/stat-models/
	rsync -av --delete slides/ hh1-web.psy.gla.ac.uk:/web/web2/talklab/stat-models/slides/
	ssh hh1-web.psy.gla.ac.uk "find /web/web2/talklab/stat-models -type d -exec chmod a+rx {} \;"
	ssh hh1-web.psy.gla.ac.uk "find /web/web2/talklab/stat-models -type f -exec chmod a+r {} \;"

clean :
	find $(DEST) -regextype grep \
		-not -regex '^$(DEST)/book.*' \
		-not -regex '^$(DEST)/slides.*' \
		-not -path $(DEST) \
		-delete
