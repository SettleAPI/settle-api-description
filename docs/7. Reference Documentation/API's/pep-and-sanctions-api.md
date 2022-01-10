# PEP and Sanctions API

Search for persons and companies of political, criminal, or economic interest in datasets from:

- [EveryPolitician.org](https://everypolitician.org/)
- [OpenSanctions.org](https://www.opensanctions.org/).

## HTTP Request

```Http
GET /api/search/:search_term HTTP/1.1
Content-Type: application/json
Host: check.settle.dev
```
#####
```json json_schema
{
  "title": "Path Parameter",
  "type": "object",
  "properties": {
    "search_term": {
      "type": "string",
      "description": "Name of Person, Company or Legal Entity."
    }
  }
}
```
#####
```js title="JavaScript / Fetch Example"
const searchTerm = encodeURI('Erna Solberg');

fetch(`https://check.settle.dev/api/search/${searchTerm}`, {
  'method': 'GET',
  'headers': {
    'Content-Type': 'application/json'
  }
})
  .then(response => {
    console.log(response);
  })
  .catch(err => {
    console.error(err);
  });
```

## Contribution

The **API** is licensed under the **MIT** license. If you would like to **contribute** to the **API**, please feel free to **fork the repo and send us a pull request**. Or if you have a comment, question, or suggestion for improvements, please [raise an issue](https://github.com/SettleAPI/pep-and-sanctions-api/issues).

### License
[MIT](https://github.com/SettleAPI/pep-and-sanctions-api/blob/prod/LICENSE) © [Settle Group](https://settle.eu/) / [Christian Wick](https://github.com/iamchriswick)