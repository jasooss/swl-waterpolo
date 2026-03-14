// manifest.json
{
  "name": "SWL Water Polo League",
  "short_name": "SWL",
  "start_url": "/index.html",
  "display": "standalone",
  "background_color": "#eef3f9",
  "theme_color": "#0a4da3",
  "icons": [
    {
      "src": "swl_logo.png",
      "sizes": "192x192",
      "type": "image/png"
    },
    {
      "src": "swl_logo.png",
      "sizes": "512x512",
      "type": "image/png"
    }
  ]
}

// sw.js
self.addEventListener('install', function(event) {
  event.waitUntil(
    caches.open('swl-cache-v1').then(function(cache) {
      return cache.addAll([
        '/index.html',
        '/swl_logo.png',
        '/manifest.json'
      ]);
    })
  );
});

self.addEventListener('fetch', function(event) {
  event.respondWith(
    caches.match(event.request).then(function(response) {
      return response || fetch(event.request);
    })
  );
});

