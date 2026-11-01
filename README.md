# AudibleCalendar for Unraid

An Unraid template for [AudibleCalendar](https://github.com/brandochdaha/AudibleCalendar), a self-hosted audiobook release calendar. This repository contains the Unraid template; the application is maintained by its upstream author and is subject to its [noncommercial license](https://github.com/brandochdaha/AudibleCalendar/blob/main/LICENSE).

## Install

The template uses a locally built Docker image, not a prebuilt registry image. From the Unraid terminal:

```sh
git clone https://github.com/brandochdaha/AudibleCalendar.git /mnt/cache/appdata/audiblecalendar-source
docker build -t audiblecalendar:local /mnt/cache/appdata/audiblecalendar-source
mkdir -p /mnt/cache/appdata/audiblecalendar
chown 10001:10001 /mnt/cache/appdata/audiblecalendar
```

Save `AudibleCalendar.xml` from this repository as `/boot/config/plugins/dockerMan/templates-user/my-AudibleCalendar.xml`, then select the template in Unraid's Docker interface and apply it. The default web port is 18000; open `http://YOUR-UNRAID-IP:18000`. The app runs as UID/GID 10001 and needs write access to the data folder. Change the host path if your cache pool has a different name, and keep SQLite data on local storage.

On first login use `admin` / `admin` and set a new password as prompted. Keep the app on a trusted network or place it behind an HTTPS reverse proxy.

## Updating

Back up the complete data directory with the container stopped. Update the upstream source checkout and rebuild `audiblecalendar:local`, then recreate the container from the Unraid template. The local image is not updated automatically by Unraid's usual registry update checks. Review upstream changes before updating.

```sh
cd /mnt/cache/appdata/audiblecalendar-source
git pull --ff-only
docker build -t audiblecalendar:local .
```

The template and source checkout are separate from the application data. Preserve `/mnt/cache/appdata/audiblecalendar` when recreating the container. See upstream documentation for backup and restoration details.
