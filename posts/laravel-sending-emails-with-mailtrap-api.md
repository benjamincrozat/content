# Laravel: Sending Emails with Mailtrap API

Looking to automate your email-sending process? If so, you’ve come to the right place!

In this step-by-step guide, I’ll show you how to leverage [Mailtrap Email Delivery Platform](https://l.rw.rw/benjamin-hp), which offers a reliable email API that has high email deliverability rates by design.

Without further ado, let’s jump straight into it!


## Setting up Laravel project

Before we start [sending emails in Laravel](https://l.rw.rw/benjamin-laravel), we first need to set up the project itself.


### Generating and writing mailables

When configuring Laravel email services In Laravel, the **config/mail.php** file will be your best friend. This file includes a **mailers** configuration array that offers sample configurations for various email drivers/transports supported by Laravel.

Based on how we set up **config/mail.php** file, Laravel will pick which service to use, allowing us to choose between different email services for different [email types](https://mailtrap.io/blog/types-of-emails/).

There’s also the “mailable” class, which is stored in the **app/Mail** directory, representing the different types of emails.

As the **app/Mail** directory isn’t present in your app by default, you can generate it with the following command:


```
php artisan make:mail MailableName
```


Once you create a mailable class, you can use the following methods to see the contents and configure the class itself:



* **Envelope** – Returns the Illuminate\Mail\Mailables\Envelope object, which defines the subject and the recipients.
* **Content** – Returns the Illuminate\Mail\Mailables\Content object, which defines the Blade template used for generating message content.
* **Attachments** – Returns an array of attachments.


### Sender configuration

With our mailables ready, let’s specify the sender or the **from** email address and name.

You can either:



* Specify the sender in the message Envelope object:

```
use Illuminate\Mail\Mailables\Address;
use Illuminate\Mail\Mailables\Envelope;
 
/**
* Get the message envelope.
*
* @return \Illuminate\Mail\Mailables\Envelope
*/
public function envelope()
{
   return new Envelope(
       from: new Address('example@example.com', 'Test Sender'),
       subject: 'Test Email',
   );
}
```


* Specify the sender in **config/mail.php** with a global **from** address:

```
'from' => ['address' => 'example@example.com', 'name' => 'App Name']
```



**Pro Tip**: I recommend you use the global **from** address if you plan to use it in all of the messages your application sends. It prevents you from having to call **from** method in each of the mailable classes and serves as the default **from** address.


## How to send email using Mailtrap Email Sending API

To automate your email-sending process, I suggest using [Mailtrap Email Sending API](https://mailtrap.io/email-api/), which offers high deliverability rates by design and in-depth analytics so you can easily monitor the performance of your email infrastructure.

Thanks to the [official PHP SDK](https://github.com/railsware/mailtrap-php) and documentation for [Laravel framework bridge](https://github.com/railsware/mailtrap-php/tree/main/src/Bridge/Laravel), you can seamlessly integrate Mailtrap Email Sending API as you won’t have to manually write the integration code for your project. 

Moreover, the Mailtrap library is fully compatible with Laravel 9.x. And above.

To get started, all you have to do is:



* Sign up for a [free Mailtrap account](https://mailtrap.io/register/signup) and log in.
* Add and verify your domain.
* Install the Mailtrap PHP client and dependencies with Composer.

```
composer require railsware/mailtrap-php symfony/http-client nyholm/psr7
```


* Add Mailtrap transport into your **config.mail.php** file.

```
<?php

return [
    /*
    |--------------------------------------------------------------------------
    | Mailer Configurations
    |--------------------------------------------------------------------------
    */
    'mailers' => [
    
            // start mailtrap transport
            'mailtrap' => [
                'transport' => 'mailtrap'
            ],
            // end mailtrap transport
    
    ]
];

```


* Add your Mailtrap credentials to your Laravel .env file (make sure to select the Transactional Stream; we will use Bulk Stream later).

```
MAIL_MAILER="mailtrap"
MAILTRAP_HOST="send.api.mailtrap.io"
MAILTRAP_API_KEY="YOUR_API_KEY_HERE"
MAIL_FROM_ADDRESS="name@registered_domain.com"
```


* Create a mailable class to send email.

```
php artisan make:mail WelcomeMail
```


* Configure the app/Mail/WelcomeMail.php class following this example.

```
<?php

namespace App\Mail;

use Illuminate\Bus\Queueable;
use Illuminate\Mail\Attachment;
use Illuminate\Mail\Mailable;
use Illuminate\Mail\Mailables\Address;
use Illuminate\Mail\Mailables\Content;
use Illuminate\Mail\Mailables\Envelope;
use Illuminate\Mail\Mailables\Headers;
use Illuminate\Queue\SerializesModels;
use Mailtrap\EmailHeader\CategoryHeader;
use Mailtrap\EmailHeader\CustomVariableHeader;
use Symfony\Component\Mime\Email;
use Symfony\Component\Mime\Header\UnstructuredHeader;

class WelcomeMail extends Mailable
{
    use Queueable, SerializesModels;

    private string $name;

    /**
     * Create a new message instance.
     */
    public function __construct(string $name)
    {
        $this->name = $name;
    }

    /**
     * Get the message envelope.
     */
    public function envelope(): Envelope
    {
        return new Envelope(
            from: new Address('jeffrey@example.com', 'Jeffrey Way'),
            replyTo: [
                      new Address('taylor@example.com', 'Taylor Otwell'),
                  ],
            subject: 'Welcome Mail',
            using: [
                      function (Email $email) {
                          // Headers
                          $email->getHeaders()
                              ->addTextHeader('X-Message-Source', 'example.com')
                              ->add(new UnstructuredHeader('X-Mailer', 'Mailtrap PHP Client'))
                          ;

                          // Custom Variables
                          $email->getHeaders()
                              ->add(new CustomVariableHeader('user_id', '45982'))
                              ->add(new CustomVariableHeader('batch_id', 'PSJ-12'))
                          ;

                          // Category (should be only one)
                          $email->getHeaders()
                              ->add(new CategoryHeader('Integration Test'))
                          ;
                      },
                  ]
        );
    }

    /**
     * Get the message content definition.
     */
    public function content(): Content
    {
        return new Content(
            view: 'mail.welcome-email',
            with: ['name' => $this->name],
        );
    }

    /**
     * Get the attachments for the message.
     *
     * @return array<int, \Illuminate\Mail\Mailables\Attachment>
     */
    public function attachments(): array
    {
        return [
           Attachment::fromPath('https://mailtrap.io/wp-content/uploads/2021/04/mailtrap-new-logo.svg')
                ->as('logo.svg')
                ->withMime('image/svg+xml'),
        ];
    }

    /**
     * Get the message headers.
     */
    public function headers(): Headers
    {
        return new Headers(
            'custom-message-id@example.com',
            ['previous-message@example.com'],
            [
                'X-Custom-Header' => 'Custom Value',
            ],
        );
    }
}

```


* Create an email template under resources/views/mail/welcome-email.blade.php.

```
Hey, {{$name}} and welcome here 😉

<br>
Funny Coder
```


* Add the CLI router to the app/routes/console.php file.

```
<?php

use App\Mail\WelcomeMail;
use Illuminate\Support\Facades\Artisan;
use Illuminate\Support\Facades\Mail;

/*
|--------------------------------------------------------------------------
| Console Routes
|--------------------------------------------------------------------------
|
*/

Artisan::command('send-welcome-mail', function () {
    Mail::to('testreceiver@gmail.com')->send(new WelcomeMail("Jon"));
    // Also, you can use specific mailer if your default mailer is not "mailtrap" but you want to use it for welcome mails
    // Mail::mailer('mailtrap')->to('testreceiver@gmail.com')->send(new WelcomeMail("Jon"));
})->purpose('Send welcome mail');
```


* Call the CLI command to send your email.

```
php artisan send-welcome-mail
```



And voila, you can send transactional emails without getting any errors!


## How to test email sending and emails with Mailtrap Email Testing

Once you add email-sending functionality to your app, how do you make sure your emails aren’t being sent from a blacklisted domain or marked as spam? How do you know their HTML template is properly rendered by web browsers? \
 \
My recommendation is to use [Mailtrap Email Testing](https://l.rw.rw/benjamin-sandbox).

With Mailtrap Email Testing, you can catch testing emails and preview them in a safe sandbox environment, check their spam score, analyze their HTML/CSS — all before sending them out.




![html](https://github.com/benjamincrozat/content/assets/156003281/d4feaae5-d4f4-4259-9afc-d876e839c9c0)





There’s also the Spam Report feature, which will provide you with the spam score of your emails. If you keep this score below 5, you significantly prevent a significant amount of potential [email deliverability](https://mailtrap.io/blog/email-deliverability/) issues.




![Spam score](https://github.com/benjamincrozat/content/assets/156003281/0cda2861-a51e-40de-93ce-901f5838ebab)





On top of these, and other advanced features, Mailtrap Email Testing is super easy to set up!


### SMTP

To start testing your emails with [Mailtrap’s SMTP](https://l.rw.rw/benjamin-smtp), simply follow these steps:



* Navigate to Email Testing → Inboxes → SMTP Settings
* Select the desired Laravel version from the list of integrations (I recommend version 9+)

    


<img width="705" alt="laravel smtp" src="https://github.com/benjamincrozat/content/assets/156003281/d45bed58-45ae-41bc-bf74-6b00edc606e2">





* Copy the generated code snippet in the **.env** file located in the root directory of your project. It should look something like this:

```
MAIL_MAILER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=07f4dbf61b8122
MAIL_PASSWORD=d7fc5d57bc6eac
MAIL_ENCRYPTION=tls
```



Once you’re done, you’ll be able to send the first test email with the following code:


```
<?php
use App\Mail\JustTesting;
use Illuminate\Support\Facades\Mail;
Route::get('/send-mail', function () {
    Mail::to('newuser@example.com')->send(new JustTesting());
    return 'A message has been sent to Mailtrap!';
});
```


To send the test email, start the application and access/send-mail path in your browser. You’ll soon be able to see the email in Email Testing → Inboxes.


### API

Alternatively, you can integrate Email Testing into your app and use Testing API for testing, 	 automation, and testing automated sequences.

Depending on which HTTP client you use, run one of the following commands:


```
# With symfony http client (recommend)
composer require railsware/mailtrap-php symfony/http-client nyholm/psr7

# Or with guzzle http client
composer require railsware/mailtrap-php guzzlehttp/guzzle php-http/guzzle7-adapter
```


Add Mailtrap transport into your **config.mail.php** file:


```
<?php

return [
    /*
    |--------------------------------------------------------------------------
    | Mailer Configurations
    |--------------------------------------------------------------------------
    */
    'mailers' => [
    
            // start mailtrap transport
            'mailtrap' => [
                'transport' => 'mailtrap'
            ],
            // end mailtrap transport
    
    ]
]
```


Then, you need to set the API key to the **MAILTRAP_API_KEY** variable and set your inbox ID to the **MAILTRAP_INBOX_ID**, like so:


```
MAIL_MAILER="mailtrap"

MAILTRAP_HOST="sandbox.api.mailtrap.io"
MAILTRAP_API_KEY="YOUR_API_KEY_HERE"
MAILTRAP_INBOX_ID=1000001
```


Notes: 



* You can find your API key/token by going to your Mailtrap account and navigating to Sending Domains → SMTP/API Settings




![smtp api laravel](https://github.com/benjamincrozat/content/assets/156003281/b023f52a-0de4-4906-8fb5-1084efa3575b)







* Make sure to run the clear configuration cache command to set up new variables with:

```
php artisan config:clear
```



And to test your first email, you need to [generate a Mailable class](https://laravel.com/docs/10.x/mail#generating-mailables), as with sending:


```
php artisan make:mail WelcomeMail
```


Once you create your Mailable class, you can configure your email. Here’s an example:


```
# app/Mail/WelcomeMail.php
<?php

namespace App\Mail;

use Illuminate\Bus\Queueable;
use Illuminate\Mail\Attachment;
use Illuminate\Mail\Mailable;
use Illuminate\Mail\Mailables\Address;
use Illuminate\Mail\Mailables\Content;
use Illuminate\Mail\Mailables\Envelope;
use Illuminate\Mail\Mailables\Headers;
use Illuminate\Queue\SerializesModels;
use Mailtrap\EmailHeader\CategoryHeader;
use Mailtrap\EmailHeader\CustomVariableHeader;
use Symfony\Component\Mime\Email;
use Symfony\Component\Mime\Header\UnstructuredHeader;

class WelcomeMail extends Mailable
{
    use Queueable, SerializesModels;

    private string $name;

    /**
     * Create a new message instance.
     */
    public function __construct(string $name)
    {
        $this->name = $name;
    }

    /**
     * Get the message envelope.
     */
    public function envelope(): Envelope
    {
        return new Envelope(
            from: new Address('jeffrey@example.com', 'Jeffrey Way'),
            replyTo: [
                      new Address('taylor@example.com', 'Taylor Otwell'),
                  ],
            subject: 'Welcome Mail',
            using: [
                      function (Email $email) {
                          // Headers
                          $email->getHeaders()
                              ->addTextHeader('X-Message-Source', 'example.com')
                              ->add(new UnstructuredHeader('X-Mailer', 'Mailtrap PHP Client'))
                          ;

                          // Custom Variables
                          $email->getHeaders()
                              ->add(new CustomVariableHeader('user_id', '45982'))
                              ->add(new CustomVariableHeader('batch_id', 'PSJ-12'))
                          ;

                          // Category (should be only one)
                          $email->getHeaders()
                              ->add(new CategoryHeader('Integration Test'))
                          ;
                      },
                  ]
        );
    }

    /**
     * Get the message content definition.
     */
    public function content(): Content
    {
        return new Content(
            view: 'mail.welcome-email',
            with: ['name' => $this->name],
        );
    }

    /**
     * Get the attachments for the message.
     *
     * @return array<int, \Illuminate\Mail\Mailables\Attachment>
     */
    public function attachments(): array
    {
        return [
            Attachment::fromPath('https://mailtrap.io/wp-content/uploads/2021/04/mailtrap-new-logo.svg')
                ->as('logo.svg')
                ->withMime('image/svg+xml'),
        ];
    }

    /**
     * Get the message headers.
     */
    public function headers(): Headers
    {
        return new Headers(
            'custom-message-id@example.com',
            ['previous-message@example.com'],
            [
                'X-Custom-Header' => 'Custom Value',
            ],
        );
    }
}
```


Additionally, you can use an email template:


```
# resources/views/mail/welcome-email.blade.php

Hey, {{$name}} and welcome here 😉

<br>
Funny Coder
```


And add CLI router:


```
# app/routes/console.php
<?php

use App\Mail\WelcomeMail;
use Illuminate\Support\Facades\Artisan;
use Illuminate\Support\Facades\Mail;

/*
|--------------------------------------------------------------------------
| Console Routes
|--------------------------------------------------------------------------
|
*/

Artisan::command('send-welcome-mail', function () {
    Mail::to('testreceiver@gmail.com')->send(new WelcomeMail("Jon"));
    // Also, you can use specific mailer if your default mailer is not "mailtrap" but you want to use it for welcome mails
    // Mail::mailer('mailtrap')->to('testreceiver@gmail.com')->send(new WelcomeMail("Jon"));
})->purpose('Send welcome mail');
```


Finally, to send your email, just call this CLI command:


```
php artisan send-welcome-mail
```


For additional information, check out the [official documentation](https://github.com/railsware/mailtrap-php/tree/main/src/Bridge/Laravel) for Mailtrap API.


## Wrapping up

And that’s it! Simple, isn’t it?

I’ve shown you how to send emails with Mailtrap API and ensure your messages reach your recipients’ inboxes just in time. Feel free to use this article as your go-to guide for the process.

Happy sending! 📧
