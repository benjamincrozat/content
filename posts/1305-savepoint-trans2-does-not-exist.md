---
Image: https://res.cloudinary.com/benjamincrozat-com/image/fetch/c_scale,f_webp,q_auto,w_1200/https://github.com/benjamincrozat/content/assets/3613731/36803bc1-0c15-4824-87c0-09b3e3077756
Title: Fix "1305 SAVEPOINT trans2 does not exist" in Laravel
Description: Have you ever encountered the "1305 SAVEPOINT trans2 does not exist" error while running Laravel? I have a solution for you.
Canonical: 
Audio:
Published at: 2023-12-14
Modified at:
Categories: databases, laravel, testing
---

## Understanding "1305 SAVEPOINT trans2 does not exist"

Have you ever encountered the *"1305 SAVEPOINT trans2 does not exist"* error in production or while running your Laravel tests?

I have no clue if it's a common issue, but it can be quite puzzling, especially when it appears unexpectedly.

The error *"1305 SAVEPOINT trans2 does not exist"* typically pops up in Laravel applications during database transactions.

One of the primary causes of this error is nested transactions (when a transaction is started within another transaction). You may have forgot to commit or rollback a transaction and started a new one.

## Potential fixes for "1305 SAVEPOINT trans2 does not exist"

1. I double checked that I wasn't actually nesting transactions. For instance, you I started logging all database queries occuring during my tests by using `DB::enableQueryLog()` and `DB::getQueryLog()`. In my case, this confirmed there were no nested transactions. So step two may also be the answer for you.
2. Modifying how my tests manage the database was effective. I started using the `Illuminate\Foundation\Testing\RefreshDatabase` trait instead of the `Illuminate\Foundation\Testing\LazilyRefreshDatabase` trait. Don't ask me why, I have no idea. 😅
