# Block Specific User Agents in `.htaccess`

This `.htaccess` snippet is designed to block specific user agents commonly used for web scraping, penetration testing, or unauthorized data mining. It ensures that your website is protected from automated tools that may exploit your resources.

## Rules Description

- **RewriteCond**: Each condition checks for a specific user agent or pattern in the `User-Agent` HTTP header.
- **Blocked User Agents**: 
  - HTTrack
  - wget
  - curl
  - libwww
  - python
  - WinHTTrack
  - Nmap Scripting Engine
  - Go-http-client
  - apachebench
  - Any User-Agent containing "crawler", "spider", or "scanner".
- **RewriteRule**: Denies access (`[F,L]`) if any of the conditions are met.

## Usage

1. Copy and paste the following snippet into the `.htaccess` file in the root directory of your website:
   ```apache
   RewriteCond %{HTTP_USER_AGENT} HTTrack [NC,OR]
   RewriteCond %{HTTP_USER_AGENT} wget [NC,OR]
   RewriteCond %{HTTP_USER_AGENT} curl [NC,OR]
   RewriteCond %{HTTP_USER_AGENT} libwww [NC,OR]
   RewriteCond %{HTTP_USER_AGENT} python [NC,OR]
   RewriteCond %{HTTP_USER_AGENT} WinHTTrack [NC,OR]
   RewriteCond %{HTTP_USER_AGENT} "Nmap Scripting Engine" [NC,OR]
   RewriteCond %{HTTP_USER_AGENT} Go-http-client [NC,OR]
   RewriteCond %{HTTP_USER_AGENT} apachebench [NC,OR]
   RewriteCond %{HTTP_USER_AGENT} ^.*(crawler|spider|scanner).* [NC]
   RewriteRule .* - [F,L]
