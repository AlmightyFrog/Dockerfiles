FROM ghcr.io/linuxserver/rdesktop:arch-xfce

RUN mkdir /data
WORKDIR /data

RUN \
	curl -L https://download.kde.org/unstable/digikam/8.0.0/digiKam-8.0.0-beta1-x86-64.appimage -o /opt/digikam.appimage && \
	cd /opt/ && \
	chmod +x digikam.appimage && \
	./digikam.appimage --appimage-extract && \
	mv squashfs-root digikam && \
	rm digikam.appimage

RUN \
	pacman -Sy --noconfirm --needed \
		ncdu && \
	rm -rf \
		/tmp/* \
		/var/cache/pacman/pkg/* \
		/var/lib/pacman/sync/*

COPY <<-EOT /config/Desktop/digikamGeneric.desktop
	[Desktop Entry]
	Type=Application
	Categories=Qt;Graphics;Photography;
	Exec=/opt/digikam/AppRun
	Icon=/opt/digikam/digikam.png
	MimeType=x-content/image-dcf;x-content/image-picturecd;
	Name=digiKam generic
	Terminal=false
	StartupWMClass=digikam
EOT

COPY <<-EOT /config/Desktop/digikam.desktop
	[Desktop Entry]
	Type=Application
	Categories=Qt;Graphics;Photography;
	Exec=/opt/digikam/AppRun --config /data --database-directory /data
	Icon=/opt/digikam/digikam.png
	MimeType=x-content/image-dcf;x-content/image-picturecd;
	Name=digiKam
	Terminal=false
	StartupWMClass=digikam
EOT

RUN chmod +x /config/Desktop/*.desktop

VOLUME ["/data"]

