# Letterboxd iOS X-Callback-URL Support

As of version 2.0, Letterboxd for iOS added x-callback-url support.

## Scheme

Following the x-callback-url [specification](http://x-callback-url.com/specifications/), the scheme for Letterboxd iOS is

`letterboxd://x-callback-url/[action]?[action parameters]&[x-callback parameters]`

## Actions

### /search

#### Parameters

- **query** (_optional_ STRING)
The search query.

- **type** (_optional_ STRING)
One of `film`, `member`, `list`, `review`, `contributor` (cast & crew) and `all`. Defaults to `all`.

### /addToWatchlist

#### Parameters

- **name** (_optional_ STRING)
The name of the film. The value is used as a search query, and the correct result will need to be confirmed before continuing.

### /log
Add a new log entry for a film

#### Parameters

- **name** (_optional_ STRING)
The name of the film. The value is used as a search query, and the correct result will need to be confirmed before continuing.

- **date** (_optional_ STRING)
ISO8601 formatted date that you watched the film, i.e. `YYYY-MM-DD`. If not present, the default diary date will not be set.

- **rewatch** (_optional_ BOOLEAN)
Indication that this logging was a rewatch. Only valid if `date` is specified.

- **tags** (_optional_ STRING)
Comma separated list of tags.

- **review** (_optional_ STRING)
A review of the film. The text can include the following HTML tags:
`<strong> <em> <b> <i> <a href=""> <blockquote>`

- **containsSpoilers** (_optional_ BOOLEAN)
Indicates that the review text contains spoilers. Only valid if review text is present.

- **rating** (_optional_ DOUBLE)
A rating from 0.5 to 5, at 0.5 intervals. A 0 is interpreted as no rating.

- **like** (_optional_ BOOLEAN)
On creation of the log entry, your relationship to the film will be updated to show that you like the film.

- **shareOnFacebook** (_optional_ BOOLEAN)
Enables sharing the review to Facebook. Only valid if review text is present, and you have linked a Facebook account.

_note: For Boolean parameters, use `true` or `false` as parameter values, e.g. `rewatch=true`_

## x-callback parameters

**__This is optional but recommended for better user experience__**

x-callback-url defines several parameters with specific purposes, all of which are optional. These parameters should be passed as query args in the URL, in the format `key1=value1&key2=value2`. All values should be URL encoded strings.

- **x-success** : URL to open on completion of the requested action. If not provided, the user will stay in the Letterboxd app after the action is successfully completed.

- **x-cancel** : URL to open if the requested action is cancelled by the user. If not provided, the user will stay in the Letterboxd app after the action is cancelled.

- **x-error** : URL to open if the requested action generates an error or failed to complete. In such case, Letterboxd app will report the failure to the user, and return to the source app. If not present, user will stay in the Letterboxd app.
