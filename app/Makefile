# Copyright 2020 Alex Woroschilow (alex.woroschilow@gmail.com)
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
PWD:=$(shell pwd)

.PHONY: all

all: clean init
	mkdir --parents $(PWD)/build/Boilerplate.AppDir/msedge
	$(PWD)/bin/Apprepo.AppImage --destination=$(PWD)/build appdir boilerplate libatk1.0-0 libatk-bridge2.0-0 libgtk-3-0 libreadline8 at-spi2-core

	wget --output-document=$(PWD)/build/build.rpm https://packages.microsoft.com/yumrepos/edge/microsoft-edge-stable-99.0.1150.46-1.x86_64.rpm
	cd $(PWD)/build && rpm2cpio $(PWD)/build/build.rpm | cpio -idmv && cd ..

	cp --force --recursive $(PWD)/build/usr/share/*			            $(PWD)/build/Boilerplate.AppDir/share
	cp --force --recursive $(PWD)/build/opt/microsoft/msedge*/* 	    $(PWD)/build/Boilerplate.AppDir/msedge

	chmod 4755 $(PWD)/build/Boilerplate.AppDir/msedge/msedge-sandbox
	chmod 4755 $(PWD)/build/Boilerplate.AppDir/msedge/msedge

	echo "LD_LIBRARY_PATH=\$${LD_LIBRARY_PATH}:\$${APPDIR}/msedge" 	>> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo "export LD_LIBRARY_PATH=\$${LD_LIBRARY_PATH}" 				>> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo "" 		                                                >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo "" 		                                                >> $(PWD)/build/Boilerplate.AppDir/AppRun
	echo "exec \$${APPDIR}/msedge/msedge \$${@}" 		            >> $(PWD)/build/Boilerplate.AppDir/AppRun

	rm -f $(PWD)/build/Boilerplate.AppDir/*.desktop 		|| true
	rm -f $(PWD)/build/Boilerplate.AppDir/*.png 		  	|| true
	rm -f $(PWD)/build/Boilerplate.AppDir/*.svg 		  	|| true

	cp --force $(PWD)/AppDir/*.desktop 			$(PWD)/build/Boilerplate.AppDir/ || true
	cp --force $(PWD)/AppDir/*.png 				$(PWD)/build/Boilerplate.AppDir/ || true
	cp --force $(PWD)/AppDir/*.svg 				$(PWD)/build/Boilerplate.AppDir/ || true

	 export ARCH=x86_64 && $(PWD)/bin/appimagetool.AppImage $(PWD)/build/Boilerplate.AppDir $(PWD)/Edge.AppImage
	 chmod +x $(PWD)/Edge.AppImage

init:
	mkdir --parents $(PWD)/bin

	wget https://apprepo.de/appimage/download/apprepo \
		--output-document=$(PWD)/bin/Apprepo.AppImage
	chmod +x $(PWD)/bin/Apprepo.AppImage

	wget https://github.com/AppImage/AppImageKit/releases/download/13/appimagetool-x86_64.AppImage \
		--output-document=$(PWD)/bin/appimagetool.AppImage
	chmod +x $(PWD)/bin/appimagetool.AppImage

clean:
	rm -rf $(PWD)/*.AppImage
	rm -rf $(PWD)/bin/*
	rm -rf $(PWD)/build
