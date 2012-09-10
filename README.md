# Render Version [![Build Status](https://secure.travis-ci.org/bwillis/renderversion.png?branch=master)](http://travis-ci.org/bwillis/renderversion)

Render version is a way to easily version views in your Rails app.

## Install - not release yet

```
gem install renderversion # TBD
```

## How to use

### Configure
You need to define the supported versions in your Rails application.rb file as
```view_versions```. Use this config to set the range of supported API
versions:
```ruby
config.view_versions = [1,3,4,5] # or (1...5)
```

### Version your views

When a client makes a request to your controller the latest version of the
view will be rendered. The latest version is determined by naming the template
or partial with a version number that you configured to support.
```
- app/views/posts
    - index.html.erb
    - edit.html.erb
    - show.html.erb
    - show.json.jbuilder
    - show.v1.json.jbuilder
    - show.v2.json.jbuilder
    - new.html.erb
    - _form.html.erb
```
If you start supporting a newer version, v3 for instance, a request for the latest
version of posts/show will gracefully degrade to the latest support available
version, in this case posts/show.v2.json.jbuilder.

### Client requests

When a client makes a request it will automatically receive the latest supported
version of the view. The client can also request for a specific version by one of three
strategies:

 - Api version HTTP header ```API-Version: 1```
 - HTTP Accept header ``Accept: application/xml; version=1`` - http://blog.steveklabnik.com/posts/2011-07-03-nobody-understands-rest-or-http#i_want_my_api_to_be_versioned
 - parameter based ``?_api_version=1``

## Development Work

1. Ensure controller tests are Rails like
2. Expose helpers in the controller to detect the version
 - is_view_v1?
3. Log the version requested in the logs

# License

RenderVersion is released under the MIT license: www.opensource.org/licenses/MIT
