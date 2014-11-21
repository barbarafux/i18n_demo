# i18n_demo

This is just a demo Ruby on Rails app to show how internationalization with i18n can look like.

## Steps
Setting locale via before_action in the application controller

````
# app/controllers/application_controller.rb
  before_action :set_locale

  def set_locale
    I18n.locale = params[:locale] || I18n.default_locale
  end

````

Adding a helper method to avoid passing the locale as a URL query 
parameter.

````
# app/controllers/application_controller.rb
  
  def default_url_options(options={})
      { :locale => I18n.locale }
  end
````

Set Route and add language to url

````
# config/routes.rb
scope "(:locale)", :locale => /en|de|fr|it|es/ do
    root :to => 'landing#index'
    get "landing/index"
 end
````

Add YML-file for each language you wanna include

````
# config/locales/en.yml
en:
  hello: "Hello world"
````

````
# config/locales/de.yml
en:
  hello: "Hallo Welt"
````

Add Links to switch  between languages

````
# app/views/layouts/application.html.erb
	<div id="container">
		<div id="nav">
			<%= t('language') %>:
			<%= link_to_unless_current "English", locale: "en" %> | 
			<%= link_to_unless_current "German" , locale: "de" %> | 
			<%= link_to_unless_current "French" , locale: "fr" %> | 
			<%= link_to_unless_current "Italien" , locale: "it" %> | 
			<%= link_to_unless_current "Spanish" , locale: "es" %>
		</div>
	</div>
````

Add variable which should be translated to View 
````
# app/views/landing/index.html.erb
<%= t('hello') %>
````

## Resources
[i18n](https://github.com/svenfuchs/i18n)

[Lingohub-Blog](http://blog.lingohub.com/developers/2013/08/internationalization-for-ruby-i18n-gem/#i18n-ruby-on-rails)
 
[Railscasts](http://www.railscast.com)
 
## License
The MIT License (MIT)


Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.