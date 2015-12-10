# mongoose-i18n-localize

mongoose-i18n-localize is a mongoose plugin to support i18n and localization in your mongoose schemas.

It seems like [mongoose-i18n](https://github.com/elrolito/mongoose-i18n) is not longer supported and I didn't get it to work on my machine, so I decided to write my own version.

## Usage

```
npm install mongoose-i18n-localize
```

Create your schema:

```
var mongoose = require('mongoose');
var mongooseI18n = require('mongoose-i18n-localize');

var schema = new mongoose.Schema({
	name: {
		type: String,
		i18n: true
	}
});

schema.plugin(mongooseI18n, {
	locales: ['en', 'de']
});

var Model = mongoose.model('Name', schema);
```

This will create a structure like:

```
{
	name: {
		en: String,
		de: String
	}
}
```

All validators of `name` get assigned to `name.en` and `name.de`.

mongoose-i18n-localize adds the methods `toObjectTranslated(resource, locale)` and `toJSONTranslated(resource, locale)` to the i18n schema. To get a localized object to locale `en`, just do:

```
Model.find(function(err, resources) {
	var localizedResources = Model.schema.toJSONTranslated(resources, 'en');
})
```

`localizedResources` has now the following structure:

```
[
	{
		name: {
			en: 'hello',
			de: 'hallo',
			localized: 'hello'
		}
	}
]
```

Use `toObjectTranslated` or `toJSONTranslated` according to `toObject` or `toJSON`.

# Tests

To run the tests you need a local MongoDB instance available. Run with:

```
npm test
```
# Issues

Please use the GitHub issue tracker to raise any problems or feature requests.

If you would like to submit a pull request with any changes you make, please feel free!
