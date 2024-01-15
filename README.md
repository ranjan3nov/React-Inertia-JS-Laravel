# InertiaJS - React Installation Guide for Laravel

This guide outlines the steps to set up InertiaJS in a Laravel application without using any starter kit.

## Instructions:

1. **Create a new Laravel app:**

```bash
Laravel new YourAppName
```

2. **Install InertiaJS**

```bash
composer require inertiajs/inertia-laravel
```

3. **Create app.blade.php and paste the following**

```blade
    <!DOCTYPE html>
    <html>
      <head>
        <meta charset="utf-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0" />
        @viteReactRefresh
        @vite('resources/js/app.jsx')
        @inertiaHead
      </head>
      <body>
        @inertia
      </body>
    </html>
```

4. **Modify the following**

> Delete resources/views/welcome.blade.php

> Delete resources/js/bootstrap.js


5. **Create a middleware and register it**

```bash
php artisan inertia:middleware
```

> _Once the middleware has been published, register the HandleInertiaRequests middleware in your App\Http\Kernel as the last item in your web middleware group._

```php
    'web' => [
        // ...
      \App\Http\Middleware\HandleInertiaRequests::class,
        ],
```

6. **Install necessary NPM packages:**

```bash
npm i @inertiajs/react @vitejs/plugin-react react react-dom
```

7. **Follow Vite React plugin setup:**

_Vite React plugin documentation_

> https://www.npmjs.com/package/@vitejs/plugin-react

```php
import { defineConfig } from 'vite';
import laravel from 'laravel-vite-plugin';
import react from '@vitejs/plugin-react'


export default defineConfig({
    plugins: [
        react(),
        laravel({
            input: ['resources/css/app.css', 'resources/js/app.js'],
            refresh: true,
        }),
    ],
});

```

8. **Modify app.js to app.jsx:**

```jsx
import React from "react";
import { createRoot } from "react-dom/client";
import { createInertiaApp } from "@inertiajs/react";
import { resolvePageComponent } from "laravel-vite-plugin/inertia-helpers";

createInertiaApp({
    resolve: (name) =>
        resolvePageComponent(
            `./Pages/${name}.jsx`,
            import.meta.glob("./Pages/**/*.jsx")
        ),
    setup({ el, App, props }) {
        createRoot(el).render(<App {...props} />);
    },
});
```

9. **Create resources/js/Pages/Index.jsx:**

```jsx
import React from "react";

const Index = () => {
    return <h1>This is a test component</h1>;
};

export default Index;
```

10. **Install InertiaJS React package:**

```bash
npm install @inertiajs/react
```

11. **Create a route using Inertia in web.php file.**

```php
use Inertia\Inertia;

Route::get('/', function () {
    return Inertia::render('Index');
});
```

*All set! Your Laravel application is now configured with InertiaJS without using any starter kit. Feel free to customize and build upon this foundation for your project.*
