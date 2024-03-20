# Laravel: Managing Email Attachments 

Are you working on a Laravel project or application but don’t know how to send emails with attachments? Don’t worry—I’ve got you covered!

In this step-by-step tutorial, I’ll show you how to send emails with attachments in Laravel and test them to make sure they reach your recipients’ inboxes.

Let’s get straight into it!


## Setting up the Laravel project

First things first, we have to set up the project itself before [sending emails in Laravel](https://mailtrap.io/blog/send-email-in-laravel/).


### Configuration

To configure Laravel email services, I used the **config/mail.php** file. Within it, there’s a mailers configuration array with a sample configuration entry for each of the mail drivers/transports that Laravel supports.

The important thing to note here is that the default configuration value in this file will determine which mailer you will use by default when sending an email from your Laravel application.

This gave me plenty of options because, thanks to all of the mailers configured in the **config/mail.php** file, I was able to use different email-sending services for different email types.


### Generating and writing mailables

In Laravel, the “mailable” classes stored in the app/Mail directory represents different types of emails.

Note that the **app/Mail** directory isn’t present in your application by default, so you won’t be able to find it there. Instead, it’s generated once you create the first mailable class.

To create a mailable class, simply use the following command of the Artisan CLI, which is included in Laravel:


```
php artisan make:mail MailableName
```


Once I ran this command and created the mailable class, I was able to see its contents.

To configure the class itself, you can use some of the following methods:



* **Envelope** – This method returns the Illuminate\Mail\Mailables\Envelope object, which defines the subject and the recipients.
* **Content** – This method returns the Illuminate\Mail\Mailables\Content object, which defines the Blade template used to generate message content.
* **Attachments** – This method returns an array of attachments.


### Sender configuration

Now, we need to specify the sender or the “from” email address and name.

To do this, you can either specify the sender in the Envelope object, like so:


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


Or, specify the sender in **config/mail.php** using a global “from” address:


```
'from' => ['address' => 'example@example.com', 'name' => 'App Name']
```


Keep in mind that you should use the global “from” address if you plan on using the same “from” address in all of the emails your application sends. This prevents you from having to call the “from” method in each of your mailable classes, which can be quite convenient. Moreover, it serves as the default “from” address if you don’t specify any other.


## How to send emails with attachments in Laravel?

Now that we have set up everything, we can finally start sending.

But first, we need to configure our SMTP credentials provided by [Mailtrap Email Delivery Platform](https://mailtrap.io/), which offers high deliverability rates and has been super reliable for me so far.

Simply create a Mailtrap account, log in, and navigate to Sending Domains located under Email Sending. Once there, you’ll need to add and verify your domain, which takes a few seconds only.

Check out how to do it step by step in this [handy video](https://www.youtube.com/watch?v=g5o0ixCi4tg).



After verifying your domain, you will be taken to the page from where you can copy the Mailtrap SMTP credentials into the **.env** of your email-sending service, project, or app.



![1](https://github.com/benjamincrozat/content/assets/156003281/a3d5a752-6dcc-4cde-95c7-3266abfc6326)



Here’s what the credentials should look like once integrated into the Laravel code:


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


After I entered the credentials and sent a test email from my Laravel project, Mailtrap verified my SMTP setup.

If your test email is sent successfully, you should receive a response similar to “250 2.0.0 Ok: queued as …”

To finish verifying, simply click on **Verify Setup**.



![2](https://github.com/benjamincrozat/content/assets/156003281/0040a088-72ec-4f80-ae30-e4a90141c04a)





Besides offering an SMTP service, Mailtrap also allows me to keep a close eye on the performance of my email infrastructure.

But how does it accomplish this?

Put simply, Mailtrap provides me with in-depth analytics, through which I can monitor my opens, clicks, bounces, etc.



![3](https://github.com/benjamincrozat/content/assets/156003281/8f8f9916-1352-4141-9b2b-5236fecd4ab7)





When I open my stats, I can see which emails were delivered successfully, which weren’t, and more.



![4](https://github.com/benjamincrozat/content/assets/156003281/cecfda5d-916d-41fe-a915-9a0b46e3d630)




The best part about it is that I get to see an overview of all the important stats and metrics:



![5](https://github.com/benjamincrozat/content/assets/156003281/5f367bb0-2d05-407f-8355-dd023ebd52f9)




So, I highly recommend you enable Mailtrap tracking settings, as they can be a lifesaver.

But let’s get back to creating those mailable classes I talked about previously in the article. For this, we can use the following command:


```
php artisan make:mail MyTestEmail
```


Once you run this command, check under **app/mailMyTestEmail.php**, where you should see the **MyTestEmail** class.



![6](https://github.com/benjamincrozat/content/assets/156003281/0132a906-a39d-4f54-a6c7-49c02a2bedcf)




And here’s the class code for you:


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


If you’ve followed along, the **content()** method should return a view. Then, we need to go to resources/views and create a new folder with a [blade.php file](https://laravel.com/docs/9.x/blade) in it, where you can write some text.



![7](https://github.com/benjamincrozat/content/assets/156003281/4c9e2f29-3fb4-4750-be3f-897bae5a72de)




Now, let's revisit the **content()** method and update it to return the newly created view by changing its name accordingly.

If you want to make things a bit more dynamic, you can make your email **template.blade.php** file include your recipient’s name using the **with** attribute to pass the name.

Here’s how:


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


I did this by making a small change in the **test-email.blade.php** view file as it allows it to accept the **$name** variable.


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


Here’s what you should see:



![8](https://github.com/benjamincrozat/content/assets/156003281/ec22c929-3c91-4531-96b2-06153744d7c3)




To test things out, I ran the **php artisan serve** command and went to my browser, where I pasted the route I created. It was **localhost:8000/testroute** in my case.

If everything works as expected, the email you test should go to the inbox of the “to” address you specified.

And now, finally, what you’ve come here for. 

To add attachments to my emails in Laravel, all I did was modify the **attachments** method.

First, I made them in the **MyTestEmail** class, like so:


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


Then, I made some changes in the **testroute** code under **routes/web.php**:


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


## How to test emails in Laravel?

When implementing this much code, testing your email-sending setup is crucial as plenty of things can go wrong. Your emails might be sent from a blacklisted domain, they might be marked as spam, or their HTML template code can be poorly rendered by some browsers.

All of this can happen without you even knowing it.

Although you can test your emails with your personal inbox, I always recommend email testing solutions as they’re faster, don’t affect your domain rating, don’t fill up your inbox with junk, and usually come with various beneficial features.

I typically use [Mailtrap Email Testing](https://mailtrap.io/email-sandbox/), a part of the Mailtrap Email Delivery Platform, which allows me to solve numerous email testing issues while maintaining the email process secure.

Mailtrap Email Testing allows me to catch testing emails from staging and dev environments and preview them. It also checks their content spam score and analyzes their HTML/CSS so I can replace or remove any faulty lines of code before I send emails to my recipients.




![9](https://github.com/benjamincrozat/content/assets/156003281/33ecce09-671d-49e7-aefa-48fac456700f)



If you’re a developer or a QA and you want to keep things more organized, Mailtrap Email Testing allows you to do just this by creating multiple inboxes for different projects and stages of projects.

Additionally, Mailtrap Email Testing provides you with insight into SMTP transaction info, along with the original values of email headers and the option to forward your testing emails to whitelisted recipients, either automatically or manually.

Most importantly, testing emails in Laravel with Mailtrap Email Testing is super easy as it takes only a few minutes and consists of several easy steps.

All you have to do is:




* Register for a Mailtrap account and log in
* In your account, go to Email Testing → Inboxes → SMTP settings
* Select Laravel from the list of integrations





![10](https://github.com/benjamincrozat/content/assets/156003281/d4ca178a-2c89-477d-82be-5e0ed0fb3e12)




* Copy the generated code snippet and paste it into your email-sending script

Once you run the script, you will get the test email in your Email Testing virtual inbox.

Lastly, Mailtrap Email Testing offers you an alternative way to start using the testing solution.

It provides SMTP credentials for each of your virtual inboxes, which you can find by clicking “Show Credentials” on the SMTP Settings page. So, if you prefer using credentials over code snippets, simply copy and paste the Mailtrap SMTP server credentials into your email-sending script, MTA settings, or any other system that supports them.


## Wrapping up

And this wraps our guide on sending email attachments in Laravel with Mailtrap SMTP!

I’ve shown you how the process works step-by-step, so now you can use it as a resource whenever you want to send email attachments in Laravel.

Thanks for reading!
