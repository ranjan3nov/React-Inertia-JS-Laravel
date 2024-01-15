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

3. **Create app.blade.php and copy the syntax from official documention andd this line**

```blade
@viteReactRefresh
```

4. **Delete this unecessary file**

> Delete resources/views/welcome.blade.php

> Delete public/js/bootstrap.js

5. **Create a middleware and register it**

```bash
php artisan inertia:middleware
```

> _Once the middleware has been published, register the HandleInertiaRequests middleware in your App\Http\Kernel as the last item in your web middleware group._

> 'web' => [
    // ...
    \App\Http\Middleware\HandleInertiaRequests::class,
>    ],

6. **Install necessary NPM packages:**

```bash
npm i @inertiajs/react @vitejs/plugin-react react react-dom
```

7. **Follow Vite React plugin setup:**

_Vite React plugin documentation_

8. **Modify app.js to app.jsx:**

```jsx
import React from "react";
import { createRoot } from "react-dom/client";
import { createInertiaApp } from "@inertiajs/inertia-react";
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

9. **Create Pages/Index.jsx:**

```jsx
import React from "react";

const Index = () => {
    return <h1>This is a test component</h1>;
};

export default Index;
```

10. **Install InertiaJS React package:**

```bash
Install InertiaJS React package:
```

11. **Create a route using Inertia in web.php file.**

```php
use Inertia\Inertia;

Route::get('/', function () {
    return Inertia::render('Index');
});
```

*All set! Your Laravel application is now configured with InertiaJS without using any starter kit. Feel free to customize and build upon this foundation for your project.*
