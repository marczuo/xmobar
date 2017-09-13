index.src = ../readme.md
index = readme.md
releases = ../news.md
css = xmobar.css
images = xmobar-sawfish.png xmobar-xmonad.png
remote = community.haskell.org:/srv/projects/xmobar/
htmls = index.html releases.html
title = % xmobar - a minimalistic status bar

default: index.html

$(index): $(index.src)
	@sed -E "s/^\\[!\\[Build .+/$(title)/1" $(index.src) > $(index)

index.html: releases.html $(index) $(css)
	pandoc -f markdown -t html -c $(css) --toc -N -s \
               $(index) > index.html

releases.html: $(releases) $(css)
	pandoc -f markdown -t html -c $(css) -s \
               $(releases) > releases.html

upload-images:
	rsync -zav $(images) $(remote)

upload-pages: $(htmls)
	rsync -zav $(htmls) $(css) $(remote)

upload: upload-images upload-pages

clean:
	rm -f $(htmls) $(index)
