# Lite for CKeditor in Drupal 8

Lite integrates the LITE track changes plugin for CKEditor with Drupal.
[https://ckeditor.com/cke4/addon/lite](https://ckeditor.com/cke4/addon/lite)

## Installation

### Composer (Recommended)

To download this module fork, Lite library and opentip, using Composer
template for Drupal [https://github.com/drupal-composer/drupal-project](https://github.com/drupal-composer/drupal-project),
add these lines to your repositories section on composer.json file:

```json
"repositories": [
    {
        "type": "composer",
        "url": "https://packages.drupal.org/8"
    },
    {
        "type": "vcs",
        "url": "https://github.com/Mogtofu33/lite"
    },
    {
      "type": "package",
      "package": {
        "name": "library/lite",
        "version": "1.2.28",
        "type": "drupal-library",
        "dist": {
          "url": "https://download.ckeditor.com/lite/releases/lite_1.2.28.zip",
          "type": "zip"
        }
      }
    },
    {
      "type": "package",
      "package": {
        "name": "library/opentip",
        "version": "2.4.6",
        "type": "drupal-library",
        "dist": {
          "url": "https://github.com/enyo/opentip/archive/v2.4.6.tar.gz",
          "type": "tar"
        }
      }
    }
],
```

Then run

```bash
composer require "drupal/lite:2.x-dev" "library/lite:1.2.28" "library/opentip:2.4.6"
```

### Manual (Not recommended, use Composer)

* Download this module in /modules folder.
* Download the version **1.2.28** of the LITE CKEditor plugin from
  [https://download.ckeditor.com/lite/releases/lite_1.2.28.zip](https://download.ckeditor.com/lite/releases/lite_1.2.28.zip) and extract it to /libraries. The extracted
  folder must be named lite. So Lite plugin file can be accessed from
  **/libraries/lite/plugin.js**
* **Optional** By default changes are only visible in the Wysiwyg editor, if you
  want to display changes on the **view mode** with **tooltip** support you must install
  **Opentip** library.
  Create a folder opentip in your /libraries folder.
  From [https://github.com/enyo/opentip/archive/v2.4.6.tar.gz](https://github.com/enyo/opentip/archive/v2.4.6.tar.gz), download
  **opentip-jquery.min.js** and place it in **/libraries/opentip**, so your file can
  be accessed from
  **/libraries/opentip/downloads/opentip-jquery.min.js**
  _Note_: you can remove all files from archive excepting **downloads/opentip-jquery.min.js**
  
### Post installation

* Enable the module
* Visit status report to ensure your Lite plugin is correctly loaded.
* Enable any of the track changes buttons by dragging them into the active
  toolbar configuration for the desired text formats from the Text Formats
  configuration page (For example on /admin/config/content/formats/manage/basic_html).
  * Configure Lite options below **CKEditor plugin settings**
  * Enable the _Lite changes tracking_ under **Enabled filters**
  * If the **Limit allowed HTML tags and correct faulty HTML** filter is enabled, add or replace to the **Allowed HTML tags** under the **Filter settings** :

```text
<del class="ice-del ice-cts-*" data-changedata data-userid data-cid data-last-change-time data-time data-username> <ins class="ice-ins ice-cts-*" data-changedata data-userid data-cid data-last-change-time data-time data-username>
```

* Configure the Lite options under **filter settings**

## Configuration

Lite plugin default state settings are available from the text format
configuration form.

After the installation, you can configure specific options form
**/admin/config/content/lite/settings**

Some global permissions to allow roles to toggle or resolve changes for all text formats can be set from **People > Permissions** (/admin/people/permissions#module-lite)

## Content moderation

If the Drupal Content Moderation module is enabled, Lite text format option by
Workflow and by states will be available.

Prior to text format configuration you must enable a Workflow on your content
type and set the Workflow transitions permissions to your roles accordingly.

## Known issues

Lite **1.2.30** can cause an issue with images or copy/paste, see
[https://www.drupal.org/node/2907869](https://www.drupal.org/node/2907869)

If an image is added without any text it should be not tracked.

If image caption is enable, the image will not be tracked.
