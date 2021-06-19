# CakeHouse
Kullanmak için aşağıdakı komutları çalıştırın ...

```php
<?php
// config.php
$GLOBALS['TL_HOOKS']['gc_generateFrontendTemplate'][] = array('MyGalleryCreatorClass', 'doSomething');

// MyGalleryCreatorClass.php
class MyGalleryCreatorClass extends \System
{

       /**
        * Do some custom modifications
        * @param Module $objModule
        * @param null $objAlbum
        * @return mixed
        */
       public function doSomething(\Module $objModule, $objAlbum=null)
       {
              global $objPage;
              $objPage->pageTitle = 'Bildergalerie';
              if($objAlbum !== null)
              {
                     // display the album name in the head section of your page (title tag)
                     $objPage->pageTitle = specialchars($objAlbum->name);
                     // display the album comment in the head section of your page (description tag)
                     $objPage->description = specialchars(strip_tags($objAlbum->comment));
                     // add the album name to the keywords in the head section of your page (keywords tag)
                     $GLOBALS['TL_KEYWORDS'] .= ',' . specialchars($objAlbum->name) . ',' . specialchars($objAlbum->event_location);
              }
              return $objModule->Template;
       }
}
``` 
Btw, Backend is PHP , will change to C# soon..
Installation Instructions
- 1. Create a database on your MYSQL Server
- 2. Run -setup/cc_embeddable_galleries.sql- in your MYSQL client to create tables
- 3. Create at least 1 user in the -- cc_embeddable_galleries_users_admin -- table
- 4. In the -lib/config.inc.php- you need to do 2 things.
	- Set up database connection credentials and filepath constants in -lib/config.inc.php- file and comment out local settings
	- Set up your station site details (ad market, format, FB app id's) in the section titled // ads and facebook share - EDIT
- 5. Place all files and folders on your COMMON server in a folder called "gallery"
- 6. To create galleries, go to http://yourstationwebsite.com/common/gallery/admin.php and log in.
