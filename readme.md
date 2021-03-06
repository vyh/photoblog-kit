# Photoblog Kit

This is a plugin with tools for adding a photoblog to a WordPress site. Features:

- Photos custom post type (id "photos") with custom meta fields for a date-taken timestamp 
and an array of product page urls - Albums (id "albums") and Keywords (id "keywords") custom 
taxonomies, both non-hierarchical
- Auto-populates title, content/description, timestamp, and keywords from Featured Image EXIF 
data, if available, upon saving the post
- Adds a div of available EXIF data (date taken, camera, lens, aperture, shutter speed, focal 
length, ISO) to the post content upon single-post display
- Adds product links, albums, and keywords, if they are available, below post content upon 
single-post display; if no product links are present, displays a "contact me with requests"
message instead
- Display-only field on photo posts will hide product links / request message for that post
if checked
- Support for query var "prints=true" (or false) to query photos with(out) product links
- "Featured" field on photo posts with support for query var "featured=true" (or false)
- Support for ordering photo posts by date taken with "orderby=timestamp"

Further display customization is up to the theme in use. The idea is for this to allow a blog 
to include single-image posts and have most of the content automatically populated from the 
image's EXIF data, as well as to display the EXIF data in a nice format. It's not *quite* 
automatic, in that you have to Save Draft (presumably you aren't going to blindly publish the 
post) after setting the featured image in order to populate the fields in the editor. It will 
not overwrite any existing data in those four fields, so you should be able to customize them 
as needed.

As long as the date taken meta field is in a format accepted by php's `strtotime` function, 
it should display properly in the EXIF block. (Note that it displays day, month, and year, 
even if, e.g., you only enter year and month.)

If you prefer a different style of EXIF display, the EXIF block is added with 
`add_filter( 'the_content', 'pk_display_exif' )` and should be removable with a 
`remove_filter` call with the same arguments. There is a function available, 
`pk_get_exif_array`, which takes the post ID and returns an array of EXIF data.
