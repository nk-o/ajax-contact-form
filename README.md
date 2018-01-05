# AJAX Contact Form
PHP class for send emails using php `mail()` function.

## Configure PHP
Configuration placed in variables on the top of main class in file `ajax-contact-form.php`.

## Configure HTML
```html
<form action="ajax-contact-form.php" class="ajax-contact-form">
    <p>
    	<input type="text" name="name" placeholder="Name" required>
    </p>
    <p>
    	<input type="email" name="email" placeholder="Email" required>
    </p>
    <p>
    	<textarea name="message" rows="8" placeholder="Your Message" aria-required="true" required></textarea>
    </p>
    <p>
    	<input type="submit" value="Send">
    </p>

    <div class="ajax-contact-form-response-success"></div>
    <div class="ajax-contact-form-response-error"></div>
</form>
```

## Configure JS
Example with jQuery, but you can use plain JS.
```javascript
$('.ajax-contact-form').on('submit', function(e) {
    e.preventDefault();

	var $form = $(this);
    var $responseSuccess = $form.find('.ajax-contact-form-response-success');
    var $responseError = $form.find('.ajax-contact-form-response-error');

    $.ajax({
        type: 'POST',
        url: $form.attr('action'),
        data: $form.serialize(),
        success: function(response) {
            response = JSON.parse(response);
            if (response.type && response.type === 'success') {
                $responseError.hide();
                $responseSuccess.html(response.response).show();
                $form[0].reset();
            } else {
                $responseSuccess.hide();
                $responseError.html(response.response).show();
            }
        },
        error: function(response) {
            $responseSuccess.hide();
            $responseError.html(response.responseText).show();
        }
     });
});
```

# Used in our templates https://nkdev.info/

# License
Copyright (c) 2018 nK Licensed under the MIT license.
