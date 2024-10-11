# API

## Introduction

Beginning with v3.1 HortusFox features a REST API, so you can perform operations on your workspace via third party software.
In order to be able to use the API feature, you need to enable it in your admin dashboard as well as generate an API key to be able to access this feature.

<img src="gfx/Screenshot 2024-05-15 153024.png" alt="screenshot"/>

You can then use the generated API key from your third party software to perform API queries. You can also deactivate an API key or entirely remove it.
You can generate as many API keys as you want. 

**IMPORTANT**: Although not explicitly specified in the below endpoints, you must provide a parameter `token` for each API call providing your API token:
```
?token=(your API token)
```

## API endpoints

### Plants

#### Get plant details

Returns default and custom plant attributes of a plant.

```
ANY /api/plants/get?plant=(plant ID)
```

#### Update plant default attribute

Updates a default attribute of a plant

```
ANY /api/plants/update?plant=(plant ID)&attribute=(attribute name)&value=(new value)
```

#### Delete a plant

Deletes a plant from your database. Note: If you just want to move a plant to the history, you can just use the update plant method and set history = 1.

```
ANY /api/plants/remove?plant=(plant ID)
```

#### Get list of plants

Returns a plant list from a location

```
ANY /api/plants/list?location=(plant location ID)&limit=(max amount of returned results)&from=(start from this ID)&sort=(asc/desc)
```

#### Search for plants

Search through the plant database

```
ANY /api/plants/search?expression=(search token)&limit=(max amount of returned results)
```

#### Add custom plant attribute

Adds a custom plant attribute to a specific plant

```
ANY /api/plants/attributes/add?plant=(plant ID)&label=(attribute label)&datatype=(bool/int/double/string/datetime)&content=(data content)
```

#### Edit custom plant attribute

Edits an existing custom plant attribute of a specific plant

```
ANY /api/plants/attributes/edit?attribute=(attribute ID)&label=(attribute label)&datatype=(bool/int/double/string/datetime)&content=(data content)
```

#### Remove custom plant attribute

Removes an existing custom plant attribute of a specific plant

```
ANY /api/plants/attributes/remove?attribute=(attribute ID)
```

#### Update preview photo

Updates a plants preview photo by uploading a photo or by linking an external photo

```
ANY /api/plants/photo/update?plant=(plant ID)&external=0/1&photo=(link or photo file via POST)
```

#### Add gallery photo

Upload a gallery photo or add an external photo

```
ANY /api/plants/gallery/add?plant=(plant ID)&label=(item label text)&external=0/1&photo=(link or photo file via POST)
```

#### Edit gallery photo

Edit a gallery photo item

```
ANY /api/plants/gallery/edit?plant=(plant ID)&item=(gallery item ID)&label=(item label text)
```

#### Remove gallery photo

Remove a gallery photo item

```
ANY /api/plants/gallery/remove?item=(gallery item ID)
```

#### Add plant log entry

Adds a new entry to a plants log

```
ANY /api/plants/log/add?plant=(plant ID)&content=(Log content)
```

#### Edit plant log entry

Edits an existing entry of a plants log

```
ANY /api/plants/log/edit?logid=(log item ID)&content=(Log content)
```

#### Remove plant log entry

Removes an existing entry of a plants log

```
ANY /api/plants/log/remove?logid=(log item ID)
```

#### Fetch plant log

Fetches the plant log of a specific plant

```
ANY /api/plants/log/fetch?plant=(plant ID)&paginate=(starting number, descending order)&limit=(amount of maximum returned entries)
```

### API call results

The returned responses of an API call depends on whether the operation succeeded or failed.

A success response typically returns the following JSON.

```json
{
    "code": 200
}
```

Additionally depending on the API endpoint a `data` field can also be provided with further data.

```json
{
    "code": 200,
    "data": ...
}
```

A response indicating an error will return the following response

```json
{
    "code": 500,
    "msg": "(Error message with further details)"
}
```

<p><hr/></p>

[Go back](index.md)