---
Image: https://res.cloudinary.com/benjamincrozat-com/image/fetch/c_scale,f_webp,q_auto,w_1200/
Title: How to Create a Stats Widget in Filament
Description: Learn how to create and customize a stats widget in Filament for displaying real-time statistics.
Canonical:
Audio:
Published at: 2024-06-06
Modified at:
Categories: filament
---

## Introduction

Let me walk you through creating a custom stats widget in Filament to display real-time statistics on your dashboard.

Filament can be used outside of Laravel as well, but for this article, I'll assume you're using the framework.

## Creating the Stats Widget

Let’s start by generating the necessary widget structure with the following command:

```bash
php artisan make:filament-widget PostsStats --stats-overview
```

This spins up a widget class in `app/Filament/Widgets/PostsStats.php`, which is your canvas for the next steps, where we'll inject some life into those stats!

## Registering the Widget in Your Dashboard

Pop open `app/Providers/Filament/AdminPanelProvider.php`. Here’s where you'll add the widget to be displayed right on the main dashboard:

```php
use App\Filament\Widgets\PostsStats;

class AdminPanelProvider extends PanelProvider
{
    public function panel(Panel $panel): Panel
    {
        $panel
            …
            ->widgets([
                Widgets\AccountWidget::class,
                Widgets\FilamentInfoWidget::class,
                PostsStats::class,
            ])
            …
    }
}
```

## Registering the Widget in Your Resource

If your focus is on a specific resource, like posts in this article, modify the resource page class `app/Filament/Resources/PostResource/Pages/ListPosts.php`:

```php
use App\Filament\Widgets\PostsStats;

public static function getHeaderWidgets(): array
{
    return [
        PostsStats::class,
    ];
}
```

## Customizing the Widget

Navigate to your widget class at `app/Filament/Widgets/PostsStats.php`. Here, let's set up some dynamic fetching of data from our `Post` model:

```php
public function mount(): void
{
    $this->totalPosts = Post::count();
    $this->totalViews = Post::sum('views');
    $this->averageReadTime = Post::average('read_time');
}
```

## Enhancing the Widget with Cards

In the same widget class, define cards to display your statistics. Each card will represent a different facet of your blog's performance:

```php
use Filament\Widgets\StatsOverviewWidget\Card;

protected function getCards(): array
{
    return [
        Card::make('Total Posts', $this->totalPosts),

        Card::make('Total Views', $this->totalViews)
             ->description('This month')
             ->descriptionIcon('heroicon-s-trending-up')
             ->color('success'),

        Card::make('Average Read Time', $this->averageReadTime . ' minutes')
             ->description('Average across all posts')
             ->color('warning'),
    ];
}
```

## Automatically Refresh the Widget

For our example, this isn't super useful, unless you have an army of writers constantly publishing content, but know that you can automatically refresh a widget at a given interval. In `app/Filament/Widgets/PostsStats.php`, adjust the `$pollingInterval`:

```php
protected static ?string $pollingInterval = '60s';
```

## Spread the Widget on Different Columns Across Different Screen Sizes

Adjust the appearance and responsiveness of your widget by setting `columnSpan` in the widget class to ensure it adapts to different screen sizes:

```php
protected int | string | array $columnSpan = [
    'md' => 4,
    'xl' => 6,
];
```

## Conclusion

And that's it! You've now equipped your Filament admin panel with a custom stats widget tailored for monitoring blog posts statistics. Now, tweak it, make it your own, test it, and deploy it!