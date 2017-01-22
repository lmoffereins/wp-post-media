# WP Post Media #

WP drop-in to add media attachments to posts

## Description ##

> This WordPress drop-in requires at least [WordPress](https://wordpress.org) 4.7.

Adding attachments to posts through the Media Library is simplified through this drop-in class. Use this in your plugin or theme to add media selection in your post creation/publishing workflow. 

## Usage ##

To include this drop-in in your project, do the following:

1. Put the drop-in class file and `assets` folder in your project
2. Require the `class-wp-post-media.php` class file in your main project file
3. Register a post media item with the `wp_post_media()` function, generally at the 'init' action
4. Use the `wp_post_media_field()` template tag in the Edit Post admin page where you want to have the selector field - usually in a metabox
5. You're done!

```php
// 2. In your main project file
require( $path_to_file . 'class-wp-post-media.php' );

// 3. When hooking in 'init'
wp_post_media(
	__FILE__,   // Location where the assets folder was placed
	'meta-key', // Post meta key
	array(
		'mime_type'  => 'image', // Mime type of selectable attachments. Can be 'image', 'video', 'audio', or any mime type in wp_get_mime_types(). Defaults to 'image'.
		'element'    => '#selector',     // jQuery selector of the field's parent container. Must be unique when using multiple media fields.
		'image_size' => array( 50, 50 ), // For images, the size to add when it does not exist yet. Can be image size name or array with dimensions.
		'labels'     => array(           // Labels for the Media Library
			'setPostMedia'    => __( 'Set Post Attachment',    'your-textdomain' ),
			'postMediaTitle'  => __( 'Post Attachment',        'your-textdomain' ),
			'removePostMedia' => __( 'Remove Post Attachment', 'your-textdomain' ),
		),
	)
);

// 4. In your post metabox
wp_post_media_field( $post_id, 'meta-key' );
```

## Contributing ##

You can contribute to the development of this drop-in by [opening a new issue](https://github.com/lmoffereins/wp-post-media/issues/) to report a bug or request a feature in the drop-in's GitHub repository.

## Related ##

See also the `WP_Term_Media` and `WP_Setting_Media` drop-ins, to select media attachments for terms and settings respectively.
