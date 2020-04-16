
# Welcome to Content Monetization Platform

## Commands  

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.

```javascript hl_lines="3 4 5"

async function putDiscoverBlacklistToS3 () {
    const discoverBlacklist = await gsheets.getSheetRows(discoverBlacklistSheet)
    const pkgArray = discoverBlacklist.map(r => r[0])
    const pkgArrayTrimmed = pkgArray.map(r => (r||'').trim())
    const csvAsString = pkgArrayTrimmed.join('\n')
    const filename = 'discover_blacklist_' + moment().format("MMM Do YY").replace(/ /g, "_").concat(".csv");
    const params = {
        Bucket: config.samsungDiscoverBucket.bucket,
        Body: csvAsString,
        Key: filename
    };
    console.log(params);
    await s3Upload(params)
    console.log('discover blacklist uploaded ', filename);
}


```

!!! Example

1. Each campaign can contain only one target entry in mongodb
2. Same package from two different sources is considered as different campaigns and can be uniquely identified by campaign_id
3. Exact match (with case) will be performed on all keys except for location & state.
4. For location and state, strings are converted to lowercase and checked if that string is present in the clients data. Eg. 'delhi' in mongo will match      'delhi', 'Delhi', 'New delhi', 'Greater Delhi', etc
