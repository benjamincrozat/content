# Crafting HTML Emails in Laravel

Looking to send HTML emails in Laravel? Well, look no further!

In this article, I’ll show you how to make some beautifully designed HTML emails and send them in Laravel by leveraging the SMTP service provided by the [Mailtrap Email Delivery Platform](https://mailtrap.io/?utm_source=codingblogs&utm_medium=article&utm_campaign=BenjaminCrozat).

Let’s dive right in!


# Setting up Laravel project

Before we dive in, we first need to set the project up and generate mailables.


### Configuration

The **config.mail.php** file is the main tool we’ll use for [setting up email services in Laravel](https://l.rw.rw/benjamin-laravel). It has a **mailers** section with a sample configuration for each mail drivers/transports Laravel supports.

The default configuration value in this file determines which mailers you will use by default when sending emails from your Laravel app.

This gives you a lot of flexibility because thanks to all of the mailers configured in the **config/mail.php** file, you can use different email-sending services for different email types.


### Generating and writing mailables

The “mailable” classes stored in the app/Mail directory represent different types of emails.

Keep in mind that you won’t be able to find the **app/Mail** directory in your application as it isn’t present there by default. Instead, it will be generated after you create the first mailable class. For this, you can use the following command:


```
php artisan make:mail MailableName
```


Once you create the mailable class, you will be able to see its contents.

To configure the class itself, use the following commands:



* **Envelope** **method** – Returns the Illuminate\Mail\Mailables\Envelope object, which defines the subject and the recipients.
* **Content** **method** – Returns the Illuminate\Mail\Mailables\Content object, which defines the Blade template used to generate message content.
* **Attachments method** – Returns an array of attachments.


### Sender configuration

There are two options you can use to specify the sender or the “from” email address and name, namely:



* **Envelope object**

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


* **config/mail.php**

```
'from' => ['address' => 'example@example.com', 'name' => 'App Name']
```



Note that you should use the global “from” address if you plan on using the same “from” address in all of the emails your application sends. What this does is it conveniently prevents you from having to call the “from” method in each of your mailable classes. On top of that, it serves as the default “from” address if you don’t specify any other.


### Customize the Mailable layout

For emails rendered with Markdown, you can create your own themes for mailables by publishing the **laravel-mail** assets and adding your own CSS files to the **resources/views/vendor/mail/html/themes** folder. 

Here’s the command you can use for publishing the assets:


```
php artisan vendor:publish --tag=laravel-mail
```


This Artisan command copies the default email HTML templates from Laravel’s framework to your application’s **resources/views/vendor/mail** directory, which allows you to modify them as needed.

Once you have your theme ready, you can specify it in the Mailable with public **$theme = ‘customStyle’;**

Keep in mind that this customization is for emails you render with Markdown, which Laravel then converts to HTML, applying the specified CSS theme. 


### Configure and customize Blade templates

To create dynamic HTML content for our emails, we’ll use [Blade](https://laravel.com/docs/11.x/blade), a templating engine. 

First, we need a Blade view for your email, which will contain the HTML structure of your email.

So, for example, let’s create a file named **myHtmlEmail.blade.php** in the **resources/views/emails** directory:


```
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">

    <style>
        p {
            font-size: 12px;
        }

        .signature {
            font-style: italic;
        }
    </style>
</head>
<body>
<div>
    <p>Hey {{ $name }},</p>
    <p>Can your Laravel app send HTML emails yet? 😉 </p>
    <p class="signature">Mailtrap</p>
</div>
</body>
</html>
```


Blade templates allow you to write your HTML emails and customize them with tables, styles, and other HTML elements. 

For instance, you can make the file include the recipient’s name using the **with** attribute to pass it. Here’s how:


```
<?php

namespace App\Mail;

use Illuminate\Bus\Queueable;
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Mail\Mailable;
use Illuminate\Queue\SerializesModels;

class MyTestEmail extends Mailable
{
    use Queueable, SerializesModels;

    private $name;

    /**
     * Create a new message instance.
     *
     * @param string $name
     */
    public function __construct(string $name)
    {
        $this->name = $name;
    }

    /**
     * Build the message.
     *
     * @return $this
     */
    public function build()
    {
        return $this->subject('My Test Email')
                    ->view('emails.myHtmlEmail')
                    ->with([
                        'name' => $this->name,
                    ]);
    }
}
```


This code ensures that the **myHtmlEmail.blade.php** view is correctly referenced in the Mailable class.

Customization tips:



* For CSS styling, you can include **&lt;style>** tags within the **&lt;head>** section of your HTML Blade template. 
* You can modify the Blade and CSS files directly if you publish the vendor templates with the following command:
    * **php artisan vendor:publish --tag=laravel-mail**
* Although you can link to external CSS files, keep in mind that many clients do not support external stylesheets.
* When you use dynamic data within emails, make sure that any user-generated content is escaped to prevent cross-site scripting (XSS) attacks. Laravel’s Blade syntax achieves this by automatically escaping output with **{{ }}**, but be cautious in any case.


## How to send HTML email in Laravel?

And finally, it’s time for the fun part. 

Let’s set up Mailtrap Email Sending as our [SMTP service](https://l.rw.rw/benjamin-smtp) provider, create mailable classes, and check if everything works as intended.

**Step 1. Integrate Mailtrap SMTP server with your app**

First, create a Mailtrap account, log in, and then navigate to Sending Domains, where you’ll add and verify your domain.



Once you verify your domain, you’ll be taken to the SMTP/API Settings page, where you can get your SMTP credentials. You’ll see Transactional and Bulk streams, so choose one according to the types of email messages you want to send.


![SMTP API Settings](https://github.com/benjamincrozat/content/assets/156003281/efcb7ca0-7518-4bd6-ab04-278527a39bfb)





Here’s what your SMTP mail credentials should look like when pasted into the **.env** file:


```
// .env file

MAIL_MAILER=smtp
MAIL_HOST=live.smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=//your username
MAIL_PASSWORD=// your password
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS=from@example.com
MAIL_FROM_NAME=//your app name
```


**Step 2. Verify your SMTP setup**

Next, you need to verify your SMTP setup by clicking on **Verify Setup**.



![verify your setup](https://github.com/benjamincrozat/content/assets/156003281/8091f0e2-8f1a-4896-9cf0-783334749613)





If your email is sent successfully, you should get the following response:



* “250 2.0.0 Ok: queued as …”

**Step 3. Create mailable classes**

Remember those mailable classes we talked about previously? Let’s create some now by using the following command:


```
php artisan make:mail MyTestEmail
```


Once you run this command, you should see the **MyTestEmail** class under “**app/mailMyTestEmail.php**”. Of course, you can name it as you wish, as **MyTestEmail** is just an example.


![6](https://github.com/benjamincrozat/content/assets/156003281/69284ab8-e892-4ce2-a26c-38dd99427d0a)



And here’s the class code:


```
<?php

namespace App\Mail;

use Illuminate\Bus\Queueable;
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Mail\Mailable;
use Illuminate\Mail\Mailables\Content;
use Illuminate\Mail\Mailables\Envelope;
use Illuminate\Queue\SerializesModels;

class MyTestEmail extends Mailable
{
    use Queueable, SerializesModels;

    /**
     * Create a new message instance.
     *
     * @return void
     */
    public function __construct()
    {
        //
    }

    /**
     * Get the message envelope.
     *
     * @return \Illuminate\Mail\Mailables\Envelope
     */

    public function envelope()
    {
        return new Envelope(
            subject: 'My Test Email',
        );
    }
 /**
     * Get the message content definition.
     *
     * @return \Illuminate\Mail\Mailables\Content
     */

    public function content()
    {
        return new Content(
            view: 'view.name',
        );
    }

    /**
     * Get the attachments for the message.
     *
     * @return array
     */
    public function attachments()
    {
        return [];
    }
}
```


And finally, let’s create a route in the **routes/web.php** file with the following code:


```
<?php

use Illuminate\Support\Facades\Route;
use App\Mail\MyTestEmail;
use Illuminate\Support\Facades\Mail;

Route::get('/testroute', function() {
    $name = "Funny Coder";

    // The email sending is done using the to method on the Mail facade
    Mail::to('testreceiver@gmail.com')->send(new MyTestEmail($name));
});
```


Here’s how the file should ultimately look like:



![8](https://github.com/benjamincrozat/content/assets/156003281/0e419533-99cc-4654-835a-c56ba2218d1e)





To test things out, you can run the **php artisan serve** command and go to your browser where you pasted the created route. For example, in my case, it was **localhost:8000/testroute**.

If everything is working as it should, your email should end up in the inbox of the “to” address you specified previously.


## How to test emails in Laravel?

Writing this much code without testing your emails before you send them would be like going to the airport without checking whether you packed everything. Imagine arriving at the check-in and realizing you forgot your passport. 🛂

This is exactly what can happen to your emails if you don’t test them.

Their HTML template might be poorly rendered by some web browsers, they can get sent from a blacklisted domain, or even get marked as spam—all without you knowing it.

Now, although you can use your personal inbox or log driver to test your emails, why risk affecting your domain reputation and flooding your inbox with junk when you can use [Mailtrap Email Testing](https://l.rw.rw/benjamin-sandbox)?

This Email-Sending platform is [supported by Laravel](https://laravel.com/docs/10.x/mail#mailtrap) in the official documentation and has a plethora of features that can help you boost your email deliverability and solve various testing issues. All of this while keeping the email process secure.

Mailtrap Email Testing lets you catch testing emails and preview them in a safe sandbox environment. You can check their spam score, analyze their HTML/CSS to fix or remove faulty lines of code, and more, before sending out your emails.




![html](https://github.com/benjamincrozat/content/assets/156003281/ddbe577a-ee16-4056-a473-c411c7fa2e66)


Essentially, Mailtrap Email Testing ensures your emails land where and when they’re supposed to, instead of ending up in spam folders.

And most importantly, testing emails in Laravel with Mailtrap Email Testing is quite easy, as all you have to do is:



* Register for a Mailtrap account and log in.
* In your account, go to **Email Testing** → **Inboxes** → **SMTP settings**.
* Select Laravel from the list of integrations.




![curl](https://github.com/benjamincrozat/content/assets/156003281/ed1c6843-3908-4953-b605-481f2ba0622e)






* Copy the generated code snippet and paste it into your email-sending script.

After you run the script, you will receive the test email in your Email Testing virtual inbox.

It provides SMTP credentials for each of your virtual inboxes, which you can find by clicking “Show Credentials” on the SMTP Settings page. So, if you prefer using credentials over code snippets, simply copy and paste the Mailtrap SMTP server credentials into your email-sending script, MTA settings, or any other system that supports them.


## Wrapping up

And with that, we’ve come to the end of the article!

I went over crafting HTML emails, sending them with Mailtrap SMTP, and testing them to make sure everything works as intended before you send your messages out.

Feel free to use this article as your go-to guide for sending emails in Laravel, and happy sending!
