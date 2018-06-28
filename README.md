# Letterboxd iOS X-Callback-URL Support

As of version 2.0, Letterboxd for iOS adds x-callback-url support.

## Scheme

Following the x-callback-url [specification](http://x-callback-url.com/specifications/), the scheme for Letterboxd iOS is:

`letterboxd://x-callback-url/[action]?[action parameters]&[x-callback parameters]`

## Actions

### /search

#### Parameters

- **query** (_optional_ STRING)
The search query.

- **type** (_optional_ STRING)
One of `film`, `member`, `list`, `review`, `contributor` (cast & crew) or `all`. Defaults to `all`.

### /addToWatchlist

#### Parameters

- **name** (_optional_ STRING)
The name of the film. The value is used as a search query, and the correct result will need to be manually confirmed before continuing.

### /log
Add a new log entry (diary entry or review) for a film.

#### Parameters

- **name** (_optional_ STRING)
The name of the film. The value is used as a search query, and the correct result will need to be manually confirmed before continuing.

- **date** (_optional_ STRING)
ISO8601-formatted date that you watched the film, i.e. `YYYY-MM-DD`. If absent, no diary date will be set.

- **rewatch** (_optional_ BOOLEAN)
Indicates that this viewing is a rewatch (as opposed to a first-time watch). Only valid if `date` is specified.

- **tags** (_optional_ STRING)
Comma-separated list of tags.

- **review** (_optional_ STRING)
A review of the film. The text can include these HTML tags:
`<strong> <em> <b> <i> <a href=""> <blockquote>`

- **containsSpoilers** (_optional_ BOOLEAN)
Indicates that the review text contains spoilers. Only valid if `review` is specified.

- **rating** (_optional_ DOUBLE)
A rating from 0.5 to 5, at 0.5 intervals. 0 is interpreted as no rating.

- **like** (_optional_ BOOLEAN)
Indicates that your relationship to the film should be updated to show that you liked the film.

- **shareOnFacebook** (_optional_ BOOLEAN)
Enables sharing of the review to Facebook. Only valid if `review` is specified and you have also linked a Facebook account to your profile in [Settings](https://letterboxd.com/settings/connections/).

_Note: For Boolean parameters, use `true` or `false` as parameter values, e.g. `rewatch=true`_

## x-callback parameters

**__This is optional but recommended for better user experience__**

x-callback-url defines several parameters with specific purposes, all of which are optional. These parameters should be passed as query parameters in the URL using the format `key1=value1&key2=value2`. All values should be URL-encoded strings.

- **x-success** : URL to open upon completion of the requested action. If absent, the user will remain in the Letterboxd app once the action is successfully completed.

- **x-cancel** : URL to open if the requested action is cancelled by the user. If absent, the user will remain in the Letterboxd app if the action is cancelled.

- **x-error** : URL to open if the requested action generates an error or fails to complete. In such case, the Letterboxd app will report the failure to the user, and return to the source app. If absent, the user will remain in the Letterboxd app.

## Examples

Some example uses of the URL scheme in action.

### [Drafts](https://agiletortoise.com/drafts/) actions

— [Search Letterboxd](https://drafts4-actions.agiletortoise.com/a/2LG)
Search the selected text in the Letterboxd app. Supported values for the type parameter are `film`, `member`, `list`, `review`, `contributor` (cast & crew) or `all`.

— [Add Film to Watchlist](https://drafts4-actions.agiletortoise.com/a/2LH)
Opens the Letterboxd app and uses the selected text to search for a film to add to your Watchlist. Following confirmation of the correct title, the film is added to your Watchlist and you are returned to the Drafts app.

— [Log Film with Review](https://drafts4-actions.agiletortoise.com/a/2LE)
Converts Markdown text to HTML, then opens the Letterboxd app and performs a search using the title of the note as the film name. Following confirmation of the correct film, a new review is populated.

### [Apple Workflow](https://workflow.is) actions

— [Search for Film](https://workflow.is/workflows/b2b734228ecc407e8ae2d6a48f10ce07)

— [Log Film](https://workflow.is/workflows/db50057e19c047809ea69733f5c49be8)

— [Add Film to Watchlist](https://workflow.is/workflows/8fd01a9f19c84c20a7403fc15c1a2321)

— [Add multiple Films to Watchlist](https://workflow.is/workflows/c6041fef94234a01bbbe60a8ed45cd34)

— [Log Review from input](https://workflow.is/workflows/7c6b37b20fb34da4aba54025d83df074) (compatible with Apple Watch!)

## Contribution

If you find any faults or wish to suggest improvements, please open an [Issue](https://github.com/Letterboxd/letterboxd-ios-x-callback-url/issues).
