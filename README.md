# portfolioadmin.epromn8n.click (versi 2)

Situs statis, tanpa build. Upload isi folder ini apa adanya:
- index.html
- img/ (20 file WebP)

## Yang perlu kamu ganti sendiri
- img/profile.webp  -> ganti dengan foto headshot (lihat saran di chat). Rasio 3:4, minimal 900x1200 px.
- Teks di index.html: cari "Open for freelance projects", (removed in v3), dan angka follower, lalu sesuaikan.

## Pasang di subdomain
1. DNS: buat record `portfolioadmin` di zona `epromn8n.click` (A ke IP server, atau CNAME ke host statis).
2. Server: arahkan document root subdomain ke folder ini.
   Caddy:
       portfolioadmin.epromn8n.click {
           root * /var/www/portfolioadmin
           file_server
           encode zstd gzip
       }
   nginx:
       server {
           server_name portfolioadmin.epromn8n.click;
           root /var/www/portfolioadmin;
           index index.html;
           location /img/ { expires 30d; }
       }
3. HTTPS: Caddy otomatis; nginx: certbot --nginx -d portfolioadmin.epromn8n.click
