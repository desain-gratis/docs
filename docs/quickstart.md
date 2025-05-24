---
sidebar_position: 1
---

# Quickstart

Get started by **creating a new API in under 5 minutes**. The API will support "CRUD" (Create-Read-Update-Delete) operations.

### What you'll need

- [go](https://go.dev/doc/install) version 1.23 or above


## Clone the repository

Cloning the template api repository [here](https://github.com/desain-gratis/template-api).

```bash
git clone https://github.com/desain-gratis/template-api.git my-api
```

You can type this command into Command Prompt, Powershell, Terminal, or any other integrated terminal of your code editor.

The command also installs all necessary dependencies you need to run Docusaurus.

## Run the API

Run the service:

```bash
cd my-api
make run
```

The `cd` command changes the directory you're working with. In order to work with your newly created Docusaurus site, you'll need to navigate the terminal there.


## Sync data into the API

In **another** terminal, run the following command:

```bash
make sync-data
```

## Check the data

```bash
curl -H "X-Namespace: quickstart" --url "http://localhost:9505/greeting"
```

You can pipe the data from curl to [jq](https://jqlang.org/) JSON formatting tool,

```bash
curl -H "X-Namespace: quickstart" --url "http://localhost:9505/greeting" | jq
```

and then get this output:

```json
{
  "success": [
    {
      "id": "1",
      "message": "Hello, World!"
    }
  ]
}
```

## Add another entry

Add a new entry by using HTTP POST. 

```bash
curl -X POST -H "X-Namespace: quickstart" --url "http://localhost:9505/greeting" -d '{"id": "2", "message": "Halo"}' | jq
```

```json
{
  "success": {
    "id": "2",
    "message": "Halo"
  }
}
```

Check the newly added entry:

```bash
curl -H "X-Namespace: quickstart" --url "http://localhost:9505/greeting" | jq
```

```json
{
  "success": [
    {
      "id": "1",
      "message": "Hello, World!"
    },
    {
      "id": "2",
      "message": "Halo"
    }
  ]
}
```

You can also check by `id` reference key:

```bash
curl -H "X-Namespace: quickstart" --url "http://localhost:9505/greeting?id=2" | jq
```

```json
{
  "success": [
    {
      "id": "2",
      "message": "Halo"
    }
  ]
}
```


## Modify entry

The API uses "UPSERT" operation. So both "insert" / and "update" are using the same HTTP POST command.

If the entry have the same ID, it will overwrite the previous one.

```

```bash
curl -X POST -H "X-Namespace: quickstart" --url "http://localhost:9505/greeting" -d '{"id": "2", "message": "Halo, Dunia!"}' | jq
```

```json
{
  "success": {
    "id": "2",
    "message": "Halo, Dunia!"
  }
}
```

Check the modification:

```bash
curl -H "X-Namespace: quickstart" --url "http://localhost:9505/greeting" | jq
```

```json
{
  "success": [
    {
      "id": "1",
      "message": "Hello, World!"
    },
    {
      "id": "2",
      "message": "Halo, Dunia!"
    }
  ]
}
```

## Delete entry

```bash
curl -X DELETE -H "X-Namespace: quickstart" --url "http://localhost:9505/greeting?id=2" | jq
```

It should return the deleted data.

```json
{
  "success": {
    "id": "2",
    "message": "Halo, Dunia!"
  }
}
```

Check the deletion:

```bash
curl -H "X-Namespace: quickstart" --url "http://localhost:9505/greeting" | jq
```

```json
{
  "success": [
    {
      "id": "1",
      "message": "Hello, World!"
    }
  ]
}
```


That's all!
