  rewrite ^/((urllist|sitemap).*\.(xml|txt)(\.gz)?)$
/vbseo_sitemap/vbseo_getsitemap.php?sitemap=$1 last;

  error_page   404  /404.php;

  if ($request_filename ~ \.php$ ) {
    rewrite ^(.*)$ /vbseo.php last;
  }

  if (!-e $request_filename) {
    rewrite ^/(.*)$ /vbseo.php last;
  }

      # We don't want to allow the browsers to see .hidden linux/unix
files
      location ~ /\. { deny  all; access_log off; log_not_found off; }

      location ~ /(images/|clientscript/).* {
        access_log      off;
        expires         max;
        add_header Pragma public;
        add_header Cache-Control "public, must-revalidate,
proxy-revalidate";
         try_files $uri $uri/ /vbseo.php?$args;
  }
