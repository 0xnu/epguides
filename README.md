# EPGuides

EPGuides - Electronic Program Guide - is a useful and straightforward tv program data covering countries across the globe. It's free to use, updated every seven days, and provides simple array access to the downloaded XML structures.

## EPG Data

Supports Belgium, France, Germany, and United Kingdom TV Channels at the moment:

 - **Albania, Argentina, Belgium, France, Germany and United Kingdom (combined epg, but it is large):**
 	- XML Format: ```https://www.epgapi.ml/epg```

 - **Albania:**
    - XML Format: ```https://www.epgapi.ml/al```

 - **Argentina:**
    - XML Format: ```https://www.epgapi.ml/ar```

 - **Belgium:**
    - XML Format: ```https://www.epgapi.ml/be```

 - **France:**
 	- XML Format: ```https://www.epgapi.ml/fr```

 - **Germany:**
 	- XML Format: ```https://www.epgapi.ml/de```

 - **United Kingdom:**
 	- XML Format: ```https://www.epgapi.ml/uk```

## JSON Format

Need the EPG data in JSON format? You can parse the XML output asynchronously without the callback hell using xml2js. Don't forget to replace **epg** with the country code in the URL if you need it for a specific country.

```javascript
var eyes = require('eyes'),
    http = require('http'),
    async = require('async'),
    xml2js = require('xml2js');

async.waterfall([
    function(callback) {
        http.get('https://www.epgapi.ml/epg', function(res) {
            var response_data = '';
            res.setEncoding('utf8');
            res.on('data', function(chunk) {
                response_data += chunk;
            });
            res.on('end', function() {
                callback(null, response_data)
            });
            res.on('error', function(err) {
                callback(err);
            });
        });
    },
    function(xml, callback) {
        var parser = new xml2js.Parser();
        parser.parseString(xml, function(err, result) {
            if (err) {
                callback(err);
            } else {
                callback(null, result);
            }
        });
    },
    function(json, callback) {
        // do something useful with the json
        eyes.inspect(json);
        callback();
    }
], function(err, result) {
    if (err) {
        console.log('Got error');
        console.log(err);
    } else {
        console.log('Done.');
    }
});
```

## Need a guide for your country, got issues or questions?

:sunglasses: :wave: [Email Me](mailto:oketunjifinbarrs@gmail.com)