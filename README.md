CacheModel
==========

A caching layer for Play Framework 1.x using memcached key value coding

Any class that uses this must implement a method with the signature
public boolean initAttributesToCache()

To retrieve from the cache, instead of the default Play! "search" function, use 

<pre><code>
public static <T extends CacheModel> List<T> findFromCache(Class<T> clazz, String query, Object... params)
</code></pre>

Example:
<pre><code>
	public String user_name;
	public Calendar time_created;
	public Calendar time_modified;
	
	/* init CacheModel */
	public boolean initAttributesToCache()
	{
 	  String[] keys_to_cache_list = {"time_created", "time_modified", "user_name"};
          attributes_to_cache = getHashmapForStrings(this, keys_to_cache_list);
          return true;
	}
</code></pre>
	
To search:

<pre><code>
CacheModel.findFromCache(User.class, "user_name = ?", "justin_k");
</code></pre>