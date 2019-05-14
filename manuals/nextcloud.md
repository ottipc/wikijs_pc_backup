<!-- TITLE: Nextcloud Manual -->
<!-- SUBTITLE: A quick summary of how to use the Petitcode Nextcloud -->

# Nextcloud Manual
## Documentation 

https://nextcloud.petitcode.com/index.php/settings/help

## Url
Peticode nextcloud is running on : https://nextcloud.petitcode.com


### Firefox

![Nextcloud Firefox](/uploads/nextcloud-firefox.png "Nextcloud Firefox")

### Chrome

![Nextcloud Chrome](/uploads/nextcloud-chrome.png "Nextcloud Chrome")


## Folders

### Petitcode-Documents

The Petitcode-Documents Folder is shared with all Members of Petitcode.

![Nextcloud Manual 1](/uploads/nextcloud-manual-1.png "Nextcloud Manual 1")


### Others
All other Folders are only visible for the User, who created it.

## Problems

### Not able to upload files with large file size

Solution. Set the max_size param in the nginx config fiel : **/etc/nginx/nginx.conf**:

in the httpd Section do : client_max_body_size 1000M;




