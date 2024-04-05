# Guide to Email Testing in Laravel

In this article, I’ll go over Laravel and show you how to test your emails in this ever-so-popular Framework.

For email testing purposes, I’ll use [Mailtrap](https://l.rw.rw/benjamin-hp), an Email Delivery Platform [supported by Laravel](https://laravel.com/docs/10.x/mail#mailtrap) in the official documentation, which offers both [Email Sending](https://mailtrap.io/email-sending/) and [Email Testing](https://l.rw.rw/benjamin-sandbox) solutions.


## What is Laravel, and how does it work?

Simply put, Laravel is a framework with an expressive and elegant syntax.

Its creators call it incredibly scalable and claim that it is capable of handling enterprise workloads. They also say it’s a progressive framework as it grows with the developer, whether it’s a junior or senior one.

Laravel offers various features, such as:



* Thorough dependency injection
* An expressive database abstraction layer
* Queues and scheduled jobs, 
* Unit and integration testing
* And more.


### Laravel versions

Major releases of the Laravel framework happen yearly around February, while minor and patch releases, which do not contain breaking changes, happen frequently, sometimes even on a weekly basis.

Each major release receives bug fixes for 18 months and security fixes for 2 years.


<table>
  <tr>
   <td><strong>Version</strong>
   </td>
   <td><strong>Release</strong>
   </td>
   <td><strong>Bug Fixes Until</strong>
   </td>
   <td><strong>Security Fixes Until</strong>
   </td>
  </tr>
  <tr>
   <td>7
   </td>
   <td>March 3rd, 2020
   </td>
   <td>October 6th, 2020
   </td>
   <td>March 3rd, 2021
   </td>
  </tr>
  <tr>
   <td>8
   </td>
   <td>September 8th, 2020
   </td>
   <td>July 26th, 2022
   </td>
   <td>January 24th, 2023
   </td>
  </tr>
  <tr>
   <td>9
   </td>
   <td>February 8th, 2022
   </td>
   <td>August 8th, 2023
   </td>
   <td>February 8th, 2024
   </td>
  </tr>
  <tr>
   <td>10
   </td>
   <td>February 7th, 2023
   </td>
   <td>August 7th, 2024
   </td>
   <td>February 7th, 2025
   </td>
  </tr>
</table>


Laravel 9 builds on the improvements made in Laravel 8.x and introduces bug fixes, usability enhancements, support for Symfony 6.0 components, Symfony Mailer, Flysystem 3.0, improved route:list output, a Laravel Scout database driver, new Eloquent accessor/mutator syntax, and implicit route bindings via Enums.

Laravel 10 includes a minimum PHP v8.1 version, a new Laravel Pennant package, invokable validation rules, native type declarations, and more.

I recommend a newer version of the framework for better performance that aligns with industry standards if your project server supports its setup.


### Laravel email services

Laravel has its own email services, which enable sending emails through local or cloud-based services.

The sending is done with a simple email API powered by the Symfony Mailer component.

The Laravel and Symfony Mailer combination gives users a range of drivers they can use to send email via [SMTP](https://l.rw.rw/benjamin-smtp), third-party email-sending services, and the Sendmail MTA.

Laravel’s email services enjoy quite a lot of popularity, and that is largely due to the features they provide, which include:



* Queueing emails. 
* Creating regular plain text and HTML email messages.
* Attaching files in different formats and MIME types, as well as raw data. 
* Including inline attachments and embedding raw data into email templates. 
* Previewing messages in-browser.
* Markdown support (in quite a few frameworks) - create beautiful templates and easily include buttons, tables, or panels. 
* Templating system - use various templates and configure views. 
* Localization methods - set the desired language for a specific user.
* Local development mailing - prevent sending test emails to real inboxes. 


## Why is it important to test emails?

Imagine writing a bunch of code to set up [email sending in Laravel](https://l.rw.rw/benjamin-laravel) only to realize later on that your HTML templates are being poorly rendered by some browsers.

Moreover, your emails might be getting sent from a blacklisted domain or being marked as spam.

The worst thing? All of this could happen without you even knowing it. 

Generally, testing emails is a standard industry practice, without which no experienced developer or product marketer would even imagine sending emails. 

Consider it a standard practice like checking your oil or air pressure in your tyres before going on a road trip — no one wants to be in a situation where they’ll have to fix a car by the road or fix emails after they’ve arrived in their recipients’ inboxes. 🚨


## How to test emails with Mailtrap Email Testing

Testing emails in Laravel is easy with Mailtrap Email Testing.

The platform allows you to catch testing emails and preview them in a safe sandbox environment, check the spam score of your emails, analyze their HTML/CSS, and more. The best part about it? You can do this all before sending your emails out to your recipients.



![html](https://github.com/benjamincrozat/content/assets/156003281/899f02cf-fb96-485f-aa3f-1cab6c7b5424)





With Mailtrap Email Testing, you can preview how the HTML of your emails look before you send them out, see them in their source HTML, text, raw, and more.



<img width="1004" alt="you are awesome" src="https://github.com/benjamincrozat/content/assets/156003281/52fe694d-5e82-43bd-818f-898ed8307b5f">






Additionally, you can easily share the testing process with your team members, create new projects, and add multiple objects within.




![my projects](https://github.com/benjamincrozat/content/assets/156003281/363ae73b-f135-4104-9b7b-b2a817907cef)





You can also forward the emails to the real addresses manually or automatically once you’re happy with the results you’re getting.




![staging 1](https://github.com/benjamincrozat/content/assets/156003281/0bef0584-6a97-4448-891b-8e582642c0ce)





Last but not least, testing emails with Mailtrap is quite easy, [check it out](https://youtu.be/pJT0o76RgdQ)!


### SMTP

To start testing your emails with Mailtrap, you first have to create a [free Mailtrap account](https://mailtrap.io/register/signup), which will give you access to the entire Mailtrap Email Delivery Platform. This means you’ll be able to use both Email Testing and Email Sending.

Once you create your account and log in, simply follow these steps:



* Navigate to Email Testing → Inboxes → SMTP Settings
* Select the desired Laravel version from the list of integrations (I recommend version 9+)





<img width="705" alt="laravel smtp" src="https://github.com/benjamincrozat/content/assets/156003281/72571463-d847-4f18-8dfc-03334b1e0236">







* Copy the generated code snippet in the .env file located in the root directory of your project. It should look something like this:

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


**Pro Tip**: Make sure you are using Laravel 5.8 or a newer version and that you have specified the route in the routes/web.php file.

To send the test email, start the application and access/send-mail path in your browser. You’ll soon be able to see the email in **Email Testing** →**Inboxes**.


### API

You can also integrate Email Testing into your app and use Testing API for testing, automation, and testing automated sequences.

Simply run one of the following commands, based on which HTTP client you use:


```
# With symfony http client (recommend)
composer require railsware/mailtrap-php symfony/http-client nyholm/psr7

# Or with guzzle http client
composer require railsware/mailtrap-php guzzlehttp/guzzle php-http/guzzle7-adapter
```


Then, add Mailtrap transport into your config.mail.php file:


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


**Notes**: 



* You can find your API key/token by going to your Mailtrap account and navigating to **Sending Domains** → **SMTP/API Settings**





![smtp api laravel](https://github.com/benjamincrozat/content/assets/156003281/5a1044dc-a9d6-4c2e-9fa0-8f5d05a23b04)






* Make sure to run the clear configuration cache command to set up new variables with:

```
php artisan config:clear
```



Test your first email, you need to [generate a Mailable class](https://laravel.com/docs/10.x/mail#generating-mailables), as with sending:


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


Lastly, to send your email, just call this CLI command:


```
php artisan send-welcome-mail
```


For additional information, have a look at the [official documentation](https://github.com/railsware/mailtrap-php/tree/main/src/Bridge/Laravel) for Mailtrap API.


## Wrapping up 

At the end of the day, no matter how flawless you think your code is, I always recommend testing your emails in Laravel to make sure your messages reach your recipients pitch-perfect.

I’ve shown you how to do it, so go ahead and leverage Mailtrap’s robust Email Testing capabilities to polish up your application’s email-sending functionality to its utmost extent. 🌟

Happy testing!
