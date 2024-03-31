# Sending Emails to Multiple Recipients in Laravel

Trying to send emails to multiple recipients in Laravel but you’re stuck? If so, don’t worry—you’ve come to the right place!

Sending emails to multiple recipients in Laravel isn’t rocket science, and in this article, I’ll show you how I generally do it with the help of [Mailtrap](https://l.rw.rw/benjamin-hp), which provides me with a reliable [SMTP](https://l.rw.rw/benjamin-smtp) service with high-deliverability rates by design.

What are we waiting for? Let’s get to it!


## Setting up Laravel project

First things first, before we start [sending emails in Laravel](https://l.rw.rw/benjamin-laravel), we need to set up the project itself.


### Generating and writing mailables

Your go-to resource for setting up email services in Laravel is the **config/mail.php** file. It has a **mailers** configuration array, which includes an array with a sample configuration entry for each major mail drivers/transports that Laravel supports.

The default configuration the config file has determines which mailer will be used by default when you’re sending an email from your Laravel application.

Because of the mailers configuration, we can use different email-sending services for sending specific email types.

To create a mailable class in Laravel, you can use the following command:


```
php artisan make:mail MailableName
```


Once you create a mailable class, you'll be able to find it in the **app/Mail** directory.


### Sender configuration

Next, we need to specify the sender or the **from** email address and name. 

To do this, you can either specify the sender in the message Envelope object, like so:


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


Or, if you plan to use the global **from** address in all of the emails your application sends, you can do it like this:


```
'from' => ['address' => 'example@example.com', 'name' => 'App Name']
```



## How to send emails to multiple recipients in Laravel?

Okay, now that we have our Laravel configuration in place, let's set up Mailtrap Email Sending as our SMTP service provider and send emails to multiple recipients.

**Step 1. Use Mailtrap SMTP credentials for integration with your app**

First, create a Mailtrap account, log in, and navigate to Sending Domains. Once there, you’ll need to add and verify your domain, which is a seamless process.



Then, you can copy and paste the Mailtrap SMTP credentials and paste them into your project or app configuration.



![SMTP API Settings](https://github.com/benjamincrozat/content/assets/156003281/83c2077f-2a69-4258-938d-f38e62c95f3b)




Here’s what your **.env** file should look like with the credentials inserted:


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

Next, you need to verify your SMTP setup by clicking on ‘Verify Setup,’ which will start the verification process.

If your test email is sent successfully, you should receive this response: “250 2.0.0 Ok: queued as …”



![verify your setup](https://github.com/benjamincrozat/content/assets/156003281/e7787306-b96b-442f-8078-ab364f3b5de2)




**Step 3. Create mailable classes**

Now, it’s finally time to create mailable classes I told you about previously:


```
php artisan make:mail MyTestEmail
```


Once you run this command, look for the **MyTestEmail** class under **“app/mailMyTestEmail.php”**.

Here’s the class code:


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


Next, let’s go to resources/views and create a new folder with a [blade.php file](https://laravel.com/docs/9.x/blade), in which we can write some text finally.




![6](https://github.com/benjamincrozat/content/assets/156003281/9b4317cb-9f3e-43e0-8c27-547d122ff691)





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




![8](https://github.com/benjamincrozat/content/assets/156003281/2b4760ff-1ad5-4048-b3b2-00de69e2ea03)





And, the moment of truth has come. I tested things out by running **php artisan serve** command and going to my browser, where I pasted the route I created. In my case, it was **localhost:8000/testroute**.

In case everything works, your email should land in the inbox of the “to” address you specified.


## Emailing multiple recipients

To email multiple recipients in Laravel, I use the following code:


```
foreach (['First Coder' => 'first-recipient@gmail.com', 'Second Coder' => 'second-recipient@gmail.com'] as $name => $recipient) {
    Mail::to($recipient)->send(new MyTestEmail($name));
}
```


This code essentially creates the mailable instance each time, which can come in handy as it prevents the sending of another email to every previous recipient at every iteration through the loop.

On another hand, if you want to send emails to just one recipient while also cc-ing and bcc-ing others, you can use this code snippet:


```
return new Envelope(
    subject: 'My Test Email',
    cc: ['testreceiver-cc@gmail.com'],
    bcc: ['testreceiver-bcc@gmail.com']
);
```



## Wrapping up

And this wraps our guide!

See? Didn’t I tell you that sending emails to multiple recipients in Laravel isn’t rocket science? 

Simply follow the instructions for setting up Mailtrap’s SMTP and use the code I provided you with, and you’re all set.

Happy sending!
