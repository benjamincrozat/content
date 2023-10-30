---
Author: Benjamin Crozat
Title: Use OpenAI's API to leverage GPT with PHP
Description: Improve your projects by leveraging the power of GPT, the famous language model, using PHP and OpenAI's REST API.
Published at: 2022-10-27
Modified at: 
Categories: php, gpt
---

## Introduction

To use OpenAI's REST API, you can either:
1. Use the API directly;
2. Or use a client written in PHP that will significantly simplify your journey.

Option #2 is precisely what we're aiming for, thanks to the [OpenAI PHP client](https://github.com/openai-php/client) written by Mantas Smilinskas, Nuno Maduro, and Sandro Gehri. It's like their unofficial SDK.

**This package is usable in any kind of PHP project.** No matter what your favorite framework or CMS is (Symfony, CodeIgniter, CakePHP, WordPress, Magento, etc.), there's something here for you.

And a [**Laravel adapter (openai-php/laravel) is available**](https://github.com/openai-php/laravel), which adds a handy facade and mocking abilities for everyone's convenience.

## What is AI (Artificial Intelligence)?

**Artificial intelligence (or AI for short) involves using computers to do things that would generally need human intelligence to get done.**

This means creating algorithms (or sets of rules) to sort, study, and draw predictions from data.

Just like a child becoming a smarter adult, AI systems "learn" thanks to experience.

## What is OpenAI?

**[OpenAI](https://openai.com) is a research company that is focused on AI and machine learning.**

The company was founded by several people, including Jack Hughes (one of the co-founders of Akamai Technologies) and Elon Musk (the founder of Tesla, SpaceX, and several other startups).

OpenAI's goal is to "advance digital intelligence in the way that is most likely to benefit humanity as a whole."

And the best of all? They make it easy for us to use their [GPT](https://en.wikipedia.org/wiki/Generative_pre-trained_transformer) models in our projects. I will show you how.

https://twitter.com/sama/status/1610666441027772416

## What is GPT?

GPT, which stands for Generative Pre-trained Transformer, is an advanced type of artificial intelligence model that belongs to a family called (Large) Language Models (LLMs).

So, what does GPT do?

Well, **it's designed to understand and generate human-like text** based on the input it receives.

It can read and analyze large amounts of text data and then use that knowledge to generate coherent and contextually appropriate responses or completions.

Imagine having a really smart assistant that can understand what you're saying or writing and then provide helpful and accurate information in response.

That's what GPT does, but on a much larger and more sophisticated scale.

**GPT has been trained on astronomical amounts of data from the internet**, books, articles, and other sources to develop a deep understanding of language patterns and context.

This training helps GPT generate text that sounds remarkably human-like.

It can be used for a wide range of applications, such as answering questions, writing essays, providing recommendations, and even creating code.

That being said, remember that **GPT is just one example of AI technologies**.

By the way, if you still have questions about GPT, I wrote [another article](https://benjamincrozat.com/llm-ai) that may answer them. 🙂

## The OpenAI REST API

Using PHP, you can send requests to [OpenAI's REST API](https://openai.com/api/) and work with their GPT models for tasks involving natural language processing and generation (in over 26 different languages!), as well as code understanding and generation.

Each model have their specificities and cost.

Yep, **OpenAI isn't free**!

## GPT models pricing

First, you should know **it's free to start (with $5 of credit)** and quite cheap after that.

Model | Input | Output
----- | ----- | ------
GPT-4 (32K context) | $0.06 | $0.12 
GPT-4 (8K context) | $0.03 | $0.06 
GPT-3.5 (16K context) | $0.003 | $0.004
GPT-3.5 (4K context) | $0.0015 | $0.002

*1K tokens = ~750 words* ([learn more about tokens](https://openai.com/api/pricing/#faq-token))

I recommend you to get up to speed by playing with GPT using [OpenAI's playground](https://platform.openai.com/playground).

[Create an account](https://platform.openai.com/signup), mess with GPT in the playground, see how the different models perform and join me for the next step!

## How to use the OpenAI's API with a PHP client (openai-php/client)

The best way to learn is to build. Let's get started by setting up the package and by performing a basic request.

We will focus on the `gpt-3.5-turbo` model. It's cheap, fast and this is the same model that powers ChatGPT (by the way, I wrote [a great tutorial to create plugins for it](https://benjamincrozat.com/chatgpt-plugin-laravel)). That being said, feel free to use `gpt-3.5-turbo-16k` if you have tons of text to give to the model, or `gpt-4` if you need GPT to be smarter.

### Installation

First, create a bare-minimum PHP project:

```bash
# Create a directory.
mkdir openai-test

# Go into the directory.
cd openai-test

# Create an empty file.
touch index.php
```

Next, install the [OpenAI client](https://github.com/openai-php/client):

```bash
composer require openai-php/client
```

Then, open the project in your favorite code editor and copy and paste this snippet:

```php
<?php

require 'vendor/autoload.php';

$client = OpenAI::client('YOUR_API_KEY');
```

[**You can generate your own API key here.**](https://beta.openai.com/account/api-keys)

### Usage

```php
$data = $client->chat()->create([
    'model' => 'gpt-3.5-turbo',
    'messages' => [[
        'role' => 'user',
        'content' => 'Hello!',
     ]],
]);

// Hello there! How can I assist you today?
echo $data['choices'][0]['message']['content'];
```

## How to use the OpenAI Laravel wrapper (openai-php/laravel)

The [OpenAI Laravel wrapper](https://github.com/openai-php/laravel) is a package made to help developers get started even more easily with GPT.

The package supports:
- Listing the available models for your account (gpt-4, gpt-3.5-turbo, etc.).
- Using completions (letting AI complete a piece of text).
- Chatting with a model, just like in ChatGPT.
- Transcribing an audio file (useful for podcasts for instance).
- And so much more! This is an extensive package.

### Installation

Install the package via Composer:

```bash
composer require openai-php/laravel
```

### Usage

First, make sure [**you have generated your own API key**](https://beta.openai.com/account/api-keys).

Then, publish the configuration file:

```bash
php artisan vendor:publish --provider="OpenAI\Laravel\ServiceProvider"
```

Finally, add your API key it in your *.env* file:

```
OPENAI_API_KEY=your-api-key
```

The Facade makes it super convenient to get started:

```php
$data = OpenAI::chat()->create([
    'model' => 'gpt-3.5-turbo',
    'messages' => [[
        'role' => 'user',
        'content' => 'Hello!',
    ]],
])

// Hello there! How can I assist you today?
echo $data['choices'][0]['message']['content'];
```

As you can see, there are differences with the vanilla PHP client:
1. We skip creating an OpenAI client instance, since the package already did it and stored the instance in the container.
2. We call the Facade instead of a newly created object.

## Build a powerful spam detection tool in 5 minutes

Let's say you have a comment system.

You want to make sure the user isn't spamming you.

This was a hard problem to solve. Luckily, AI can help like it's nothing.

1. Choose the model you want to use. It can be `gpt-3.5-turbo`, `gpt-3.5-turbo-16k`, or `gpt-4`.
2. Create a system prompt that defines the purpose of the model. We tell it it's a spam detection tool and give it some rules to follow.
3. Create a user prompt that contains the potentially spammy comment.

```php
$data = OpenAI::chat()->create([
    'model' => 'gpt-3.5-turbo',
    'messages' => [[
        'role' => 'system',
        'content' => <<<'PROMPT'
You are a spam detection tool. Every prompt you get is a user-generated input from my commenting system. Tell me if it should pass validation or not.

The only rules to follow are:
- No self-promotion
- No offensive statements
PROMPT,
    ], [
        'role' => 'user',
        'content' => 'Get rich with Bitcoins, now!',
    ]],
]);

// Not valid. This is self-promotion and potentially a scam.
echo $data['choices'][0]['message']['content'];
```

How incredible is that? Building this spam detection tool required almost zero effort.

But what if we change the system prompt to generate a more exploitable reply woth JSON? Here it is:

```php
<<<PROMPT
You are a spam detection tool. Every prompt you get is a user-generated input from my commenting system. Tell me if it should pass validation or not.

The only rules to follow are:
- No self-promotion
- No offensive statements

Reply with the following JSON:

{
    "pass": true,
    "reason": "foo"
}

The "reason" key should thoroughly describe why the input passes validation or not.
PROMPT,
```

Now, for the same *"Get rich with Bitcoins, now!"* comment, the `gpt-3.5-model` replies with:

```php
// {
//     "pass": false,
//     "reason": "This input should not pass validation because it is promoting a get-rich-quick scheme related to cryptocurrencies, which is often associated with fraudulent activities."
// }
echo $data['choices'][0]['message']['content'];
```

From there, you can experiment and refine this spam detection tool even more. 💪

## Even without openai-php/client, using OpenAI's API is super easy

While openai-php/client is time saving and extremely useful, some people (like me) might prefer to avoid dependencies. This is how easy it is to send requests to OpenAI's API using Laravel's HTTP client:

```php
namespace App\Actions;

use Illuminate\Support\Facades\Http;

class DoSomething
{
    public function do() : string
	{
		$response = Http::withToken(config('services.openai.api_key'))
			->post('https://api.openai.com/v1/chat/completions', [
				'model' => 'gpt-3.5-turbo',
				'messages' => [
					[
						'role' => 'user',
						'content' => 'I want you to do this thing.'
					],
				],
			])
			->throw()
			->json();

		return $response['choices'][0]['message']['content'];
	}
}
```

Then, you can test this code using the `fake()` method of the HTTP client's Facade. Here's an example written with Pest:

```php
use App\Actions\DoSomething;
use Illuminate\Http\Client\Request;
use Illuminate\Support\Facades\Http;

it('asks GPT to do a thing', function () {
    Http::fake([
        'api.openai.com/v1/chat/completions' => Http::response([
            'choices' => [['message' => ['content' => 'Lorem ipsum dolor sit amet.']]],
        ]),
    ]);

    $result = (new DoSomething)->do();

    $this->assertEquals('Lorem ipsum dolor sit amet.', $result);
  
    Http::assertSent(function (Request $request) {
	    // You can also test that:
	    // - You are using the right model ("gpt-3.5-turbo" for instance).
	    // - You sent the right prompt. Because it might contain dynamic
	    // values or be different depending on some parameters.
	});
});
```

## Conclusion

GPT is the basis for a variety of [great products](https://www.producthunt.com/search?q=ai).

Your imagination is the limit. I hope you will create something unique thanks to the power of AI!