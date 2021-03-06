``madrona.google-analytics`` - Web traffic analytics
====================================================

I manage a lot of Django projects that present slightly-different forms to 
users depending on the site/domain they're visiting.  There's also a bunch of 
custom submission code that differs from form to form, but that's neither here
nor there.

I need different Google Analytics codes depending on the sites and after 
sticking these tags into every single template, I thought it would be cool to 
be able to manage these Google analytics accounts from the Django admin page. 
I also added a mode of operation that excludes the admin interface altogether 
(you can just use the template tag)

==Two modes of operation==

Administering and associating codes with Django sites
---------------------------------------------------------
1. Add the `google_analytics` application to your `INSTALLED_APPS` 
		section of your `settings.py`.  This mode requires that you be using 
		the Django sites framework too, so make sure you have that set up as 
		well.

2. Add `GOOGLE_ANALYTICS_MODEL = True` to your `settings.py` 

3. Run a `./manage.py syncdb` to add the database tables

4. Go to your project's admin page (usually `/admin/`) and click into a site 
		objects

5. You'll now see a new field under the normal site information called 
		"Analytics Code". In this box you put your unique analytics code for 
		your project's domain.  It looks like `UA-xxxxxx-x` and save the site.

6. In your base template (usually a `base.html`) insert this tag at the very 
		top: `{% load analytics %}`

7. In the same template, insert the following code right before the closing 
		body tag: `{% analytics %}`



===Just using the template tag===

1. Add the `google_analytics` application to your `INSTALLED_APPS` section of
 		your `settings.py`.

2. In your base template, usually a `base.html`, insert this tag at the very 
		top: `{% load analytics %}`

3. In the same template, insert the following code right before the closing 
		body tag: `{% analytics "UA-xxxxxx-x" %}` the `UA-xxxxxx-x` is a 
		unique Google Analytics code for you domain when you sign up for a new
		account.
