# Settle API Specification

The Settle APIs formalized in an OpenAPI Description document.

Machine-readable API descriptions are ubiquitous nowadays and [OpenAPI](https://www.openapis.org/) is **the most broadly adopted industry standard for describing new APIs**.

## Advantages of Using OpenAPI

Having our APIs formally described in a machine-readable format allows automated tools to process it, instantly opening the door to:

- **Description Validation and Linting**: Check that the description file is syntactically correct and adheres to a specific version of the Specification and the rest of our teams formatting guidelines.
- **Data Validation**: Check that the data flowing through our APIs (in both directions) is correct, during development and once deployed.
- **Documentation Generation**: Create traditional human-readable documentation based on the machine-readable description, which always stays up-to-date.
- **Code Generation**: Create both server and client code in any programming language, freeing developers from having to perform data validation or write SDK glue code, for example.
- **Graphical Editors**: Allow easy creation of description files using a GUI instead of typing them by hand.
- **Mock Servers**: Create fake servers providing example responses which we and our third-party developers can start testing with before single line of code is written.
- **Security Analysis**: Discover possible vulnerabilities at the API design stage instead of much, much later.

On top of this, the OpenAPI Specification also provides us with:
- **A non-proprietary format**: You have a say in the future direction of the Specification!
- **The most developed tooling ecosystem**: As a direct result of the previous statement, OpenAPI offers a vast number of tools to work with it. Just take a quick look at [OpenAPI.Tools](https://openapi.tools/).
- **A format readable by both machines and humans**: Even though writing OpenAPI documents by hand is not the most convenient way of doing it *(See [Best Practices](https://oai.github.io/Documentation/best-practices.html))*, they are plain text files which can be easily browsed in case something needs to be debugged.
