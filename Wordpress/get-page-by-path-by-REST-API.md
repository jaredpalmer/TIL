Now you can ping the WP-REST API with arbitrary path and get the correct page (not just the slug)

```php
add_action('rest_api_init', function () {
	$namespace = 'presspack/v1';
	register_rest_route( $namespace, '/path/(?P<url>.*?)', array(
		'methods'  => 'GET',
		'callback' => 'get_post_for_url',
	));
});
/**
* This fixes the wordpress rest-api so we can just lookup pages by their full
* path (not just their name). This allows us to use React Router.
*
* @return WP_Error|WP_REST_Response
*/
function get_post_for_url($data)
{
    $postId    = url_to_postid($data['url']);
    $postType  = get_post_type($postId);
    $controller = new WP_REST_Posts_Controller($postType);
    $request    = new WP_REST_Request('GET', "/wp/v2/{$postType}s/{$postId}");
    $request->set_url_params(array('id' => $postId));
    return $controller->get_item($request);
}
```
