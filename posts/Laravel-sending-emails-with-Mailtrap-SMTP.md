# Laravel: Sending Emails with Mailtrap SMTP

If you have a Laravel application/project and you’re wondering how to send emails in it with SMTP, you’ve come to the right place!

I’ve been collaborating with the Mailtrap team for a while, and we’ve prepared the exact guide you need.

[Mailtrap](https://l.rw.rw/benjamin-hp) provides SMTP credentials for both sending and testing. It offers high deliverability rates and, besides being nothing but reliable for me so far, allows me to send emails in Laravel with ease.

So, without further ado, let’s see how to send emails in Laravel with Mailtrap SMTP.


## Setting up a Laravel project

Before I show you [how to send emails in Laravel](https://l.rw.rw/benjamin-laravel), let me show you how to set the project itself up first. 


### Configuration

Your best friend for configuring Laravel email services will be the **config/mail.php** file. It contains a mailers configuration array with a sample configuration entry for each major mail drivers/transports supported by Laravel.

The default configuration your new best friend config file has is exactly what determines which mailer will be used by default when you’re sending an email from your Laravel application.

This gives us plenty of flexibility, because thanks to the mailers configuration in the **config/mail.php** file, we can use different email-sending services for different types of emails.


### Generating and writing mailables

In Laravel, a “mailable” class stored in the **app/Mail** directory represents different types of emails.

Note that you won’t be able to find the **app/Mail** directory in your application as it’s not present there by default. Instead, it’s generated when you create the first mailable class.

To do this, I used the following command of the Artisan CLI (included in Laravel):


```
php artisan make:mail MailableName
```


After creating a mailable class, I was able to see the contents and configure the class itself. For this, I used the methods in the table below:


<table>
  <tr>
   <td><strong>Method</strong>
   </td>
   <td><strong>Explanation</strong>
   </td>
  </tr>
  <tr>
   <td>Envelope
   </td>
   <td>Returns the Illuminate\Mail\Mailables\Envelope object, which defines the subject and the recipients.
   </td>
  </tr>
  <tr>
   <td>Content
   </td>
   <td>Returns the Illuminate\Mail\Mailables\Content object, which defines the Blade template used for generating message content.
   </td>
  </tr>
  <tr>
   <td>Attachments
   </td>
   <td>Returns an array of attachments.
   </td>
  </tr>
</table>



### Sender configuration

Once we have our mailables, we need to specify the sender or the **from** email address and name. For this, we can either:



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



**Pro Tip**: You should use the global **from** address if you plan to use it in all of the emails your application sends. I found this quite convenient as it prevented me from having to call **from** method in each of my mailable classes. On top of that, it served as my default **from** address as I didn’t specify any other.


## How to send email in Laravel using Mailtrap Email Sending SMTP?

And finally, we’ve come to the fun part.

First I’ll show you how to set up Mailtrap as the SMTP in your application/project and then I’ll show you how I created the mailable classes and ran tests.


### Insert Mailtrap SMTP credentials

The first thing I did was insert my SMTP mail server credentials provided by Mailtrap Email Sending into the **.env** of my application.

To do this, all you have to do is create a Mailtrap account, log in, and navigate to Sending Domains under Email Sending. There you need to add and verify your domain, which takes only a few seconds.

If you’re a visual learner, Mailtrap has an [easy-to-follow video](https://www.youtube.com/watch?v=g5o0ixCi4tg) for you.             


Once you’ve verified your domain, Mailtrap will take you to the page from where you can copy the SMTP credentials and easily paste them into your project, app, or email-sending service. 

![img 1](https://github.com/benjamincrozat/content/assets/156003281/54869b60-0bf2-4151-b0d8-0776893c1950)







And here’s what your credentials should look like once you integrate them into your Laravel code:


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



### Verify your SMTP setup

Once I inserted the credentials and sent a test mail from my Laravel project, Mailtrap verified my SMTP setup.

Here’s what you should receive as a response if your test email was sent successfully:



* “250 2.0.0 Ok: queued as …”

Then, simply click on the “Verify Setup,” which will start the verification process.





![img 3](https://github.com/benjamincrozat/content/assets/156003281/852163e9-aa15-4d9d-a622-b1397edfddea)




### Enable Mailtrap tracking settings (Optional)

Now, this step is optional, but I highly recommend it as it allows me to monitor my email performance.

Namely, Mailtrap provides you with in-depth analytics through which you can keep an eye out on your opens, clicks, bounces, and more.





![img 2](https://github.com/benjamincrozat/content/assets/156003281/e046943a-f070-40e4-afbd-1a7f6136e803)



Here’s what I see when I open my stats:



![img 4](https://github.com/benjamincrozat/content/assets/156003281/953b7698-dcaf-46ed-9a5d-09ca75529e30)




And here’s the stats overview:



![img 6](https://github.com/benjamincrozat/content/assets/156003281/8e8f1718-dad9-4909-9941-2cc44620de4a)



### Create mailable classes

Remember those mailable classes I told you about previously? It’s time to create them with the following command:


```
php artisan make:mail MyTestEmail
```


After running this command, you should see the **MyTestEmail** class under “**app/mailMyTestEmail.php**”.



![img 5](https://github.com/benjamincrozat/content/assets/156003281/6deb4707-573b-4315-ae9f-6f2f727d8132)



Here’s the class code for your convenience:


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


See anything interesting? That’s right, the **content()** method returns a view. So, let’s go to resources/views and create a new folder with a [blade.php file](https://laravel.com/docs/9.x/blade) in it.

Ready to finally write some text? You can do so in the blade.php file, likewise:


![img 9](https://github.com/benjamincrozat/content/assets/156003281/f10590da-e921-47a5-993e-1356aa293e6f)




Now, let’s return to the **content()** method and replace the name of the view it returned with the name of our newly created one.

You can also make things a bit more dynamic by making your email **template/blade.php** file include the recipient’s name using the **with** attribute to pass the name. 

Check it out.


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
    public function __construct(private $name)
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
            view: 'mail.test-email',
            with: ['name' => $this->name],
        );
    }
}
```


To make this work, I had to make a small change in the **test-email.blade.php** view file as well. What this does is it allows it to accept the **$name** variable.


```
// resources/views/mail/test-email.blade.php

Hey {{$name}}, 
Can your Laravel app send emails yet? 😉 
Mailtrap
```


And lastly, let’s create a route in the **routes/web.php** file with this code:


```
<?php

use Illuminate\Support\Facades\Route;
use App\Mail\MyTestEmail;
use Illuminate\Support\Facades\Mail;

Route::get('/testroute', function() {
    $name = "Funny Coder";

    // The email sending is done using the to method on the Mail facade
    Mail::to('testreceiver@gmail.com'')->send(new MyTestEmail($name));
});
```


Here’s how the file should look then:



![img 10](https://github.com/benjamincrozat/content/assets/156003281/8da5aa28-4080-4eed-9b74-5d31ccb1cd8c)



And, the moment of truth has come. I tested things out by running **php artisan serve** command and going to my browser, where I pasted the route I created. In my case, it was localhost:8000/testroute.

In case everything works, your email should land in the inbox of the “to” address you specified.


## How to send HTML email in Laravel 

Sending attention-grabbing emails in Laravel is quite simple. All you have to do is add HTML code to your Blade view file. If you remember, we used **test-email.blade.php** in this guide.

And this is how your plain text email should look like in HTML form:


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
    <p>Can your Laravel app send emails yet? 😉 </p>
    <p class="signature">Mailtrap</p>
</div>
</body>
</html>
```



## How to send email with attachments in Laravel

To add attachments to my emails in Laravel, I simply modified the **attachments** method in the example code for sending emails I showed you earlier.

I first made them in the **MyTestEmail** class:


```
<?php

namespace App\Mail;

use Illuminate\Bus\Queueable;
use Illuminate\Mail\Mailable;
use Illuminate\Mail\Mailables\Content;
use Illuminate\Queue\SerializesModels;
use Illuminate\Mail\Mailables\Envelope;
use Illuminate\Mail\Mailables\Attachment;
use Illuminate\Contracts\Queue\ShouldQueue;

class MyTestEmail extends Mailable
{
    use Queueable, SerializesModels;

    /**
     * Create a new message instance.
     *
     * @return void
     */
    public function __construct(private $name, public $attachedFile){ }

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
            view: 'mail.test-email',
            with: ['name' => $this->name],
        );
    }

    /**
     * Get the attachments for the message.
     *
     * @return array
     */
    public function attachments()
    {
        return [
            Attachment::fromPath($this->attachedFile),
        ];

    }
}
```


Then I made some changes in the **testroute** code under **routes/web.php**:


```
<?php

use Illuminate\Support\Facades\Route;
use App\Mail\MyTestEmail;

Route::get('/testroute', function () {

    $filePath = public_path('favicon.ico');

    $name = "Funny Coder";

    Mail::to('testreceiver@gmail.com'')->send(new MyTestEmail($name, $filePath));
});
```


And that’s pretty much it. If you used this code, your email should now come with an ICO attachment named **favicon.ico**, as you can see in the snippet above.


## How to send emails to multiple recipients in Laravel

To send emails to multiple people in Laravel, I used the following code:


```
foreach (['First Coder' => 'first-recipient@gmail.com', 'Second Coder' => 'second-recipient@gmail.com'] as $name => $recipient) {
    Mail::to($recipient)->send(new MyTestEmail($name));
}
```


What this code does is iterate over an array of recipients. It also re-creates the mailable instance each time, which is super useful as it prevents the sending of another email to every previous recipient at every iteration through the loop. Just imagine the headache. 🤕

“But how do I send emails to just one recipient while also cc-ing and bcc-ing a few others?,” you might be wondering. Simply follow this example in the **MyTestEmail** class:


```
return new Envelope(
    subject: 'My Test Email',
    cc: ['testreceiver-cc@gmail.com'],
    bcc: ['testreceiver-bcc@gmail.com']
);
```



## How to test email sending and emails with Mailtrap Email Testing

If you don’t want to have your emails sent from a blacklisted domain, marked as spam, or their HTML template poorly rendered by web browsers, you should test your emails.

Yes, you can do this with your personal inbox, but why affect your domain reputation and floods your inbox with junk, when you can use [Mailtrap Email Testing](https://l.rw.rw/benjamin-sandbox)?

Besides allowing you to send emails, Mailtrap also comes with other benefits that can help you solve numerous testing problems while keeping the email testing process secure.

Namely, Mailtrap Email Testing gives you a sandbox where you can catch testing emails and then preview them, check their spam score, analyze their HTML/CSS, and more before you send them out.



![img 7](https://github.com/benjamincrozat/content/assets/156003281/408e5f24-5351-404c-9519-c425fef7c27b)



Compared to testing emails with your personal inbox, Mailtrap Email Testing keeps things neatly organized by allowing you to create multiple inboxes for different projects and their stages.

This testing solution also provides you with the original values of email headers and the option to forward your testing emails to whitelisted recipients, either manually or automatically.

And what I like the most about Email Testing is that it will only take you a few minutes to set it all up. All you have to do is:



* Log in to your Mailtrap account
* Navigate to Email Testing → Inboxes → SMTP Settings
* Select the desired Laravel version from the list of integrations

    
![img 8](https://github.com/benjamincrozat/content/assets/156003281/781adcba-29cc-43d4-a43a-1b38214156c6)




* Copy the code snippet generated by Mailtrap and paste it into your email-sending script
* Run the script 

As a result, you should get the test email in your Email Testing virtual inbox.

Mailtrap Email Testing will also provide you with SMTP credentials for each of your inboxes, which you can find by clicking on “Show Credentials” on the SMTP Settings page. This way, you can use credentials over code snippets for integrating this testing solution. You can simply copy and paste them into your email-sending script, MTA settings, email client settings, or any system that supports them. 

Alternatively, you can also integrate Email Testing into your Laravel app via Mailtrap email API. For more details, check out the [official API documentation](https://api-docs.mailtrap.io/).


## Wrapping up

And that’s it!

I’ve shown you how I send emails in Laravel with [Mailtrap SMTP](https://l.rw.rw/benjamin-smtp) and how I test them with the Email Testing solution.

Hopefully, you’ll be able to use this article as your go-to resource for sending emails in Laravel.

Good luck!
