---
Image: https://res.cloudinary.com/benjamincrozat-com/image/fetch/c_scale,f_webp,q_auto,w_1200/https://life-long-bunny.fra1.digitaloceanspaces.com/media-library/production/199/1CNkzVv7g5MYP5B4g5JdY4xXmsKFiZ-metaZmlsZS11cGxvYWRzLmpwZw%3D%3D-.jpg
Title: Single or multiple file uploads with Laravel, step by step
Description: 
Canonical: 
Audio:
Published at: 
Modified at: 
Categories: laravel
---

## Introduction

What I love the most with Laravel is its ability to make anything easier, which lets you focus on your goals.

Today, I will show you how to create a basic form that handles file uploads; single or multiple files. This often is a subject feared by developers. But stop worrying and follow me!

## Create your form

For the sake of simplicity, let's create the ugliest form known to mankind that will allow us to select an image to upload.

Create the view:

```bash
php artisan make:view photos-upload-form
```

Fill the view with my our awesome form:

```blade
@if (session('status'))
    <p>{{ session('status') }}</p>
@endif

<form method="POST" action="/upload-photos" enctype="multipart/form-data">
    @csrf

	  <div>
        <label for="photos">Photos</label>

        <input
            type="file"
            name="photos"
            accept="image/*"
        />
    </div>

    @error('photos')
        <p>{{ $message }}</p>
    @enderror

	  <button>
        Upload
    </button>
</form>
```

1. We display a flash message to let the user know their photos have been uploaded successfully.
2. We create a basic form and add the `@csrf` directive to [protect against CSRF attacks](/419-page-expired-laravel).
3. We display any validation error that might occur.

## Define the route that handles file uploads

```php
use Illuminate\Support\Facades\Route;
use App\Http\Controllers\UploadPhotosController;

Route::view('/upload-photos', 'photos-upload-form');

Route::post('/upload-photos', UploadPhotosController::class);

```

1. Create a route to display the form. Instead of creating a controller that only returns a view, let's instead create a view route to keep things simple.
2. Create another route that answers to POST requests.

## Validate the uploaded file

```php
use Illuminate\Http\Request;
use Illuminate\Validation\Rule;
use Illuminate\Validation\Rules\File;

class UploadPhotosController
{
	public function __invoke(Request $request)
	{
		$rules = File::image()
			->min(1024) // 1 MB
			->max(1024 * 12) // 12 MB
			->dimensions(
				Rule::dimensions()->maxWidth(512)->maxHeight(512)
			);
		
		$request->validate([
			'some-name' => ['required', $rules],
		]);
	}
}
```

## Store the uploaded file

Once the file has been validated, we need to move it out of PHP's temporary system folder.

Here's how easy it is using the `$request` object Laravel provides:

```php
use Illuminate\Http\Request;

class UploadPhotosController
{
	public function __invoke(Request $request)
	{
		$path = $request
			->file('some-name')
			->store('some-folder');
	}
}
```

1. We get the file using `$request->file('some-name')` (which is still stored in PHP's temporary system folder).
2. We move the file from PHP's temporary system folder to the folder of your choice in your default file system (check your *.env* file). The final name of the file will be a unique ID and the extension will be appended automatically based on the mime-type.

If you want to specify a disk that differs from the one you use by default, the `store()` method accepts a second parameter.

```php
$path = $request
	->file('some-name')
	->store('some-folder', 'some-disk');
```

**Warning**: if you are using a remote storage like S3, DigitalOcean Spaces, or whatever, there will be a second upload. This is completely normal. The user first uploads the file into PHP's temporary system folder through the form you made so it can validate the file. Then, your server will upload the file to whatever remote service you use.

## Handle multiple file uploads with two simple changes