wp-bootstrap-navwalker
======================

**A custom WordPress nav walker class to fully implement the Bootstrap 3.0+ navigation style in a custom theme using the WordPress built in menu manager.**

This version adds the support for multi level dropdowns with titles and descriptions.

NOTE
----
This is a utility class that is intended to format your WordPress theme menu with the correct syntax and classes to utilize the Bootstrap dropdown navigation, and does not include the required Bootstrap JS files. You will have to include them manually. 

Installation
------------
Place **wp_bootstrap_navwalker.php** in your WordPress theme folder `/wp-content/your-theme/`

Open your WordPress themes **functions.php** file  `/wp-content/your-theme/functions.php` and add the following code:

```php
// Register Custom Navigation Walker
require_once('wp_bootstrap_navwalker.php');
```

Usage
------------
Update your `wp_nav_menu()` function in `header.php` to use the new walker by adding a "walker" item to the wp_nav_menu array.

```php
 <?php
          $args = array(
		  'theme_location' => 'primary',
		  'depth' => 0,
		  'container' => '',
		  'menu_class'  => 'nav navbar-nav',
		  'walker'  => new BootstrapNavMenuWalker()
          );
    wp_nav_menu($args);
        ?>
```

Your menu will now be formatted with the correct syntax and classes to implement Bootstrap dropdown navigation. 

You will also want to declare your new menu in your `functions.php` file.

```php
register_nav_menus( array(
	'primary' => __( 'Primary Menu', 'THEMENAME' ),
) );
```

Typically the menu is wrapped with additional markup, here is an example of a ` navbar-fixed-top` menu that collapse for responsive navigation.

```php
<nav class="navbar navbar-inverse navbar-fixed-top">
  <div class="container">
        <div class="navbar-header">
               <button type="button" class="navbar-toggle collapsed" data-toggle="collapse" data-target="#bootstrap-nav-collapse">
                        <span class="sr-only">Toggle navigation</span>
                        <span class="icon-bar"></span>
                        <span class="icon-bar"></span>
                        <span class="icon-bar"></span>
                </button>

 <a class="navbar-brand" id="logo" href="<?php echo site_url(); ?>"><img src="<?php header_image(); ?>" height="<?php echo get_custom_header()->height; ?>" width="<?php echo get_custom_header()->width; ?>" alt="" class="img-responsive logo"/></a>

        </div><!-- /. navbar-header -->
            <!-- Collect the nav links from WordPress -->
  <div class="collapse navbar-collapse" id="bootstrap-nav-collapse">         
  <?php $args = array(
          'theme_location' => 'primary',
          'depth' => 0,
          'container' => '',
          'menu_class'  => 'nav navbar-nav',
          'walker'  => new BootstrapNavMenuWalker()
          );
    wp_nav_menu($args);
  ?>
  </div><!-- ./collapse -->
          </div><!-- /.container -->
        </nav>
```

To change your menu style add Bootstrap nav class names to the `menu_class` declaration.

Review options in the Bootstrap docs for more information on nav classes
http://getbootstrap.com/components/#nav

Displaying the Menu 
-------------------
To display the menu you must associate your menu with your theme location. You can do this by selecting your theme location in the *Theme Locations* list wile editing a menu in the WordPress menu manager.

Displaying the Titles and Descriptions 
-------------------
To display the menu item descriptions you need to click the tab **Screen Options** at the top of the screen and check "Title Attribute" and "Descriptions". The title attribute is part of the menu ite's link. the description text is not inside the menu item's link so you can add text here.



Original work by johnmegahan https://gist.github.com/1597994, Emanuele 'Tex' Tessore https://gist.github.com/3765640

