# Apache-Rate_Limit_Patch


## Patch-1. Rate Limiting with `mod_ratelimit`

Rate limiting is a technique used to limit how many requests a user can send in a short period, helping to prevent server overload and ensuring fair usage.

## Steps to Configure

1. **Enable the Module**
First, enable the `mod_ratelimit` module by running the following commands:

```
a2enmod ratelimit
service apache2 restart
```
---
This enables the module and restarts Apache to apply the changes.
---

2. **Add the Configuration**

Next, you'll need to configure the rate limiting for specific endpoints. Open your Apache configuration file (e.g., /etc/apache2/apache2.conf or the relevant VirtualHost file in /etc/apache2/sites-available/) and add the following configuration:

```
<Location "/create-file">
    SetOutputFilter RATE_LIMIT
    SetEnv rate-limit 10
</Location>
```

Explanation:
This configuration limits requests to 10 per second for the /create-file endpoint.
You can adjust the rate-limit value to match your desired rate of requests per second.

3. **Restart Apache**

Once you've added the configuration, save the file and restart Apache to apply the changes:
```
service apache2 restart
```

---
---

# Patch-2. Limit Connections from a Single IP with mod_limitipconn

The `mod_limitipconn` module helps prevent a single user (IP address) from making too many simultaneous connections to your Apache server, which can help protect your server from resource abuse and potential DoS attacks.

## Steps to Configure:

1. **Install `mod_limitipconn`:**

   Run the following commands to install and enable the module:

```
   sudo apt install libapache2-mod-limitipconn
   sudo a2enmod limitipconn
   sudo service apache2 restart
```

2. **Configure the Module:**

You can configure the module by adding directives to the Apache configuration file (e.g., /etc/apache2/apache2.conf or /etc/apache2/sites-available/000-default.conf).

Example configuration to limit connections:

```
<IfModule mod_limitipconn.c>
    <Location />
        MaxConnPerIP 1
    </Location>
</IfModule>
```

This example limits each IP address to a maximum of 1 connection.
You can adjust the MaxConnPerIP value to suit your needs.

3. **Restart Apache:**

After making the necessary changes, restart Apache to apply the configuration:
```
sudo service apache2 restart
```


