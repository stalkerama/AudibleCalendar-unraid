# AudibleCalendar for Unraid

An Unraid template for [AudibleCalendar](https://github.com/brandochdaha/AudibleCalendar), a self-hosted audiobook release calendar. The application is maintained by its upstream author and is subject to its [noncommercial license](https://github.com/brandochdaha/AudibleCalendar/blob/main/LICENSE).

## Install

The image is `ghcr.io/stalkerama/audiblecalendar:latest`. Create the persistent data directory on local storage and make it writable by the application's UID and GID:

```sh
mkdir -p /mnt/cache/appdata/audiblecalendar
chown 10001:10001 /mnt/cache/appdata/audiblecalendar
```

Save `AudibleCalendar.xml` from this repository as `/boot/config/plugins/dockerMan/templates-user/my-AudibleCalendar.xml`, then select the template in Unraid's Docker interface and apply it. The default web port is 18000; open `http://YOUR-UNRAID-IP:18000`. Change the data path if your cache pool has a different name.

On first login use `admin` / `admin` and set a new password as prompted. Keep the app on a trusted network or place it behind an HTTPS reverse proxy.

## Builds and updates

GitHub Actions builds and tests the image from the upstream revision pinned in `.github/workflows/image.yml`, then publishes it to GitHub Container Registry. To update the app, review upstream changes and update the pinned revision in that workflow. Manual workflow runs rebuild the same pinned version; they do not automatically track upstream.

Before updating the container, stop it and back up the complete data directory. Preserve that directory when recreating the container. See the upstream documentation for backup and restoration details.
