# jky_front

> A Vue.js project

#jky
nginx部署
server {
    listen       3001;
    server_name  localhost;

    #charset koi8-r;

    #access_log  logs/host.access.log  main;

    root /work/jky_front/dist;

     location ~ .*\.(gif|jpg|jpeg|png)$ {
      root /work/jky_front/dist;
       if ($request_uri   ~ .*uploads* ) {
         proxy_pass http://120.55.116.161:1234;
        }
      if (-f $request_filename) {
        expires 1d;
        break;
      }
    }

    location ~ .*\.(js|css)$ {
     root /work/jky_front/dist;
     if (-f $request_filename) {
        expires 1d;
        break;
      }
    }
   location / {
      rewrite ^~.*/?(.*)$ /$1;
      try_files $uri $uri/ /index.html;
   }

     location ~ ^/(api|download|template)/ {

      #rewrite ^~api/?(.*)$ /$1 break;

      proxy_pass http://120.55.116.161:1234;
   }

}



## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report

# run unit tests
npm run unit

# run e2e tests
npm run e2e

# run all tests
npm test
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
