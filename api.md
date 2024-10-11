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

### Tasks

#### Fetch tasks

Fetches a list of tasks

```
ANY /api/tasks/fetch?done=(0/1)&limit=(amount of maximum returned entries)
```

#### Add new task

Adds a new task

```
ANY /api/tasks/add?title=(title text)&description=(task description)&due_date=(Optional due date)
```

#### Edit task

Edit an existing task

```
ANY /api/tasks/edit?task=(task ID)&title=(title text)&description=(task description)&due_date=(Optional due date)&done=(0/1)
```

#### Remove task

Remove an existing task

```
ANY /api/tasks/remove?task=(task ID)
```

### Inventory

#### Fetch inventory

Fetches the entire inventory

```
ANY /api/inventory/fetch
```

#### Add new inventory item

Adds a new inventory item

```
ANY /api/inventory/add?name=(item name)&description=(item description)&location=(Optional location text)&group=(group ident text)&photo=(Photo to be used, use POST for file uploads)
```

#### Edit inventory item

Edit an existing inventory item

```
ANY /api/inventory/edit?item=(item ID)&name=(item name)&description=(item description)&location=(Optional location text)&group=(group ident text)&photo=(Photo to be used, use POST for file uploads)
```

#### Increment inventory item count

Increments the inventory items count

```
ANY /api/inventory/amount/inc?item=(item ID)
```

#### Decrement inventory item count

Decrements the inventory items count

```
ANY /api/inventory/amount/dec?item=(item ID)
```

#### Remove inventory item

Remove an existing inventory item

```
ANY /api/inventory/remove?item=(item ID)
```

### Calendar

#### Fetch calendar entries

Fetches calendar entries between a specific date range

```
ANY /api/calendar/fetch?date_from=(inclusive starting date, if not provided current date is used)&date_till=(inclusive end date, if not provided current date +30 days is used)
```

#### Add calendar entry

Add a new calendar entry

```
ANY /api/calendar/add?name=(entry name)&date_from=(starting date of event)&date_till=(end date of event)&class=(event class descriptor)
```

#### Edit calendar entry

Edit an existing calendar entry

```
ANY /api/calendar/edit?ident=(entry item ID)&name=(entry name)&date_from=(starting date of event)&date_till=(end date of event)&class=(event class descriptor)
```

#### Remove calendar entry

Remove an existing calendar entry

```
ANY /api/calendar/remove?ident=(entry item ID)
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