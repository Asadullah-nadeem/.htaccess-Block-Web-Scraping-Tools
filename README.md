# Block Specific User Agents and Enhance Website Security in `.htaccess`

This `.htaccess` snippet is designed to block specific user agents commonly associated with web scraping, unauthorized access attempts, and direct IP access. It also includes protection for the `.htaccess` file itself to prevent unauthorized viewing or modification.

## Rules Description

1. **Enable Rewrite Engine**: Activates the mod_rewrite module.
2. **Block User Agents**:
   - Prevents access from tools and bots like:
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
3. **Block Direct IP Access**:
   - Ensures the website is only accessible via the domain name (e.g., `codeaxe.co.in`).
4. **Protect `.htaccess`**:
   - Prevents unauthorized access to the `.htaccess` file itself.

## Usage

1. **Copy and Paste the Snippet**  
   Add the following code to the `.htaccess` file located in the root directory of your website:

   ```apache
   # Enable Rewrite Engine
   RewriteEngine On

   # Block specific user agents
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

   # Block direct IP access
   RewriteCond %{HTTP_HOST} !^codeaxe\.co\.in [NC]
   RewriteRule .* - [F,L]

   # Protect .htaccess file
   <Files ".htaccess">
     Order Allow,Deny
     Deny from all
   </Files>
