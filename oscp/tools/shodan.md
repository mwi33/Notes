# Shodan.io
## Search headers
Information about web connected devices is contained in the banner, and example is provided below.   The banner below has 5 properties:

1. Data;
2. ip_str;
3. port;
4. org; and
5. location.

Frequently the data property contains much more data then in the example below.

```json
{
    "data": "Moxa Nport Device
            Status: Authentication disabled
            Name: NP5232I_4728
            MAC: 00:90:e8:47:10:2d",
    "ip_str": "46.252.132.235",
    "port": 4800,
    "org": "SingTel Mobile",
    "location": {
        "country_code": "SG"
    }
}
```

if we wanted to find more 'Moxa Nport' devices, we could simply search for 'Moxa Nport'.

We can also filter on any properties by using the 'filter:value' key-value pair.

e.g. countre:SG (for singapore).

## Resources
### Links
https://help.shodan.io/the-basics/search-query-fundamentals

### API / Python

### Search filters
https://www.shodan.io/search/filters
https://github.com/JavierOlmedo/shodan-filters

#### Interesting search filters
has_screenshot  >> true/false
"authentication disabled"

## Search tags and syntax


