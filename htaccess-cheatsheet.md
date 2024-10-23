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




# Step 2
Header set Report-To "{\"group\":\"default\",\"max_age\":10886400,\"endpoints\":[{\"url\":\"https://f3krgt39.uriports.com/reports\"}],\"include_subdomains\":true}
Header set Reporting-Endpoints "default=\"https://f3krgt39.uriports.com/reports\"

# Step 3
Header set NEL "{\"report_to\":\"default\",\"max_age\":2592000,\"include_subdomains\":true,\"failure_fraction\":1.0}


# Step 4
Header set Content-Security-Policy-Report-Only "default-src 'self'; font-src 'self'; img-src 'self'; script-src 'self'; style-src 'self'; frame-ancestors 'self'; report-uri https://f3krgt39.uriports.com/reports/report; report-to default"

# Step 5
Header set Permissions-Policy-Report-Only "microphone=();report-to=default, camera=(self \"https://www.example.com\");report-to=default, fullscreen=*;report-to=default, payment=self;report-to=default"

# Step 6
Header set Cross-Origin-Embedder-Policy-Report-Only "require-corp; report-to=\"default\""
Header set Cross-Origin-Opener-Policy-Report-Only "same-origin; report-to=\"default\""
```
