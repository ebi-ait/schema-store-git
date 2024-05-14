# versioning method

tag with _<checklist-id>_-_<version>_

# requirements from a checklist store

## get a single checklist by version

used by ENA validator, HCA validator, etc.

The url to get version 2.1.1 of checklist climate would be:
https://github.com/ait/schema/blob/climate-v2.1.1/climate.json

raw url
https://raw.githubusercontent.com/amnonkhen/schema-store/av2/a.json?token=GHSAT0AAAAAACMIUC3TJKQ2I6XX5OBRYWYWZSDOTTQ
https://raw.githubusercontent.com/amnonkhen/schema-store/av1/a.json?token=GHSAT0AAAAAACMIUC3TEGUB5OXTEEC2WD4EZSDOTGA

thin wrapper api

schema.ebi.org/a/1.1.1 -> translated to the relevant git url

The checklist and tag need to match:

https://github.com/ait/schema/blob/climate-v2.1.1/sample.json
-> HTTP 400
tag does not match checklist

### cons for this approach
1. cloning a tag would show incorrect versions 

## get all checklists with a specific tag
This tag should not be a versioned checklist tag.

Example scenarios: 
- get latest checklists

field a 2.1.0 = will accept only 2.1.0
field a ~2.1.0 = will accept 2.1.0-2.2.0 (not inclusive)
field a ^2.1.0 = will accept 2.1.0-3 (not inclusive)


A checklist called a
uses fields:
a - v 1.2.3
b - v 2.4.0

would be saved in the "fragments" repo like this":
```json
{
    "a": "1.2.234",
    "b": "2.4.0",
    "c": "3.8.0"
}
```

When we release checklist a:
1. replace fields with the contents of specified version - resolve actual version according to semver markers: `~,^`
3. save as a schema file
4. commit to the released schema repo
5. tag with the next version - if needed (if we go with copied files per version, there is no need to tag)


