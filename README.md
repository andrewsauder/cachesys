# cacheSys

Simple PHP caching system for raw data or rendered output.

----------

## Installing
Composer installer coming soon! For now, simply include cachesys.php in your project.

## Useage
All of the samples below will assume that you add a *use* statement inside of your namespace referencing cacheSys.

    <?php
    namespace MyVendorNamespace;
    use andrewsauder;

If you opt not to add a *use* statement, you must reference the cacheSys methods by it's fully qualified class name. Ie:

    \andrewsauder\cacheSys::get( 'cacheName', 'cacheKey' );


### Retrieving and Create Cache
This is the core useage of cacheSys. I like to think of it as a wrapper for any complex logic that slows requests down.

    $employee = cacheSys::get( 'employees', 712 );

    if( $employee===false ) {
	    //do heavy lifting to create $employee
	    $employee = 'Andrew';
	    cacheSys::put( 'employees', 712, $employee );
    }

	var_dump( $employee );

Of course, you always need to make sure that your cached data remains relevant. To do this you can make use of the *max age* parameter of the *get* method

    /* get the cached copy of employee 712
     * but return false if the cache was created
	 * more than 86,400 seconds (24 hours) ago
	 */
    $employee = cacheSys::get( 'employees', 712, 86400 );

### Delete Cached Item
You can also delete a specific cached item on demand.

    cacheSys::deleteCachedItem( 'employees', 712 );

### Delete Cache Category
Or delete an entire cache category. For example, if you wanted to delete all employees instead of just one, you can delete the entire category instead

    cacheSys::deleteCachedCategory( 'employees');
