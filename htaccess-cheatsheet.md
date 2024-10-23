# .htaccess Cheatsheet

```apacheconf


Reporting-Endpoints


# Content Security
<IfModule mod_headers.c>
    Header set Content-Security-Policy "default-src 'self'; report-to csp-endpoint"
    Header set Reporting-Endpoints "https://example.com/csp-reports"
</IfModule>


# CORs
# Blanket allow access to external websites to load assets
Header set Access-Control-Allow-Origin "*"
```
