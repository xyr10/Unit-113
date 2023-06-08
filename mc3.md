# PasswordResetView
This view allows us to enter an email address and receive an email
with instructions on resetting our password (if the email is valid).
```
template_name = "registration/password_reset_form.html"
subject_template_name = "registration/password_reset_subject.txt"
email_template_name = "registration/password_reset_email.html"
```

# PasswordResetDoneView
This view is simply a (text) confirmation communicating that
we submitted the previous form successfully.
```
template_name = "registration/password_reset_done.html"
```

# PasswordResetConfirmView
This view is where we will pick a new password (and confirm it).
```
template_name = "registration/password_reset_confirm.html"
```

# PasswordCompleteView
This view offers a plain text confirmation that we submitted the previous form correctly.
```
template_name = "registration/password_reset_complete.html"
```

## Steps
1. Override all the templates above so they match the look and feel of our site.
2. Test out the entire flow, ensuring that everything meets your expectations.


{% load i18n %}{% autoescape off %}
{% blocktranslate %}You're receiving this email because you requested a password reset for your user account at {{ site_name }}.{% endblocktranslate %}

{% translate "Please go to the following page and choose a new password:" %}
{% block reset_link %}
{{ protocol }}://{{ domain }}{% url 'password_reset_confirm' uidb64=uid token=token %}
{% endblock %}
{% translate 'Your username, in case you’ve forgotten:' %} {{ user.get_username }}

{% translate "Thanks for using our site!" %}

{% blocktranslate %}The {{ site_name }} team{% endblocktranslate %}

{% endautoescape %}
