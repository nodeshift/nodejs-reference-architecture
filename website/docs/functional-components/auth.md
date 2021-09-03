---
sidebar_position: 1
---


# Authentication

## Recommended Components

- Passport - http://www.passportjs.org/
  Passport is authentication middleware for Node.js. Extremely flexible and modular, Passport can be unobtrusively dropped in to any Express-based web application. Is based on strategies which allows for a large number of integrations.

- HelmetJS - https://helmetjs.github.io/
  Helmet helps you secure your Express apps by setting various HTTP headers. It’s not a silver bullet, but it can help!

- IBM Cloud AppID https://cloud.ibm.com/docs/services/appid
  App ID helps developers to easily add authentication to their web and mobile apps with few lines of code, and secure their Cloud-native applications and services on IBM Cloud.

- Istio - https://istio.io/
  Istio provides a service mesh, includes security features https://istio.io/docs/tasks/security/
  IBM provides an Istio Adapter for App Identity and Access https://istio.io/docs/reference/config/policy-and-telemetry/adapters/app-identity-access-adapter/

## Guidance

- Use Helmet to configure http headers to address security attacks.

- Use Passport to handle your web strategy

- Use a web strategy based on AppID whenever possible.

- There is a difference between a WebApp/BFF(Backend for Frontend) and a pure Backend API that never deals with a Frontend like a Web Browser. Knowning this difference will help you understand the requirements in terms of security.

- A Frontend WebApp should never handle end user credentials such as username/password, it should always delegate to an Authorization Server for example AppID service. https://github.com/ibm-cloud-security/appid-video-tutorials/blob/master/02a-simple-node-web-app/app.js

- A pure Backend API that never deals with a fronted should never be concern of redirecting or dealing with end users, they would require an access/AOI token or assume the proxy/gateway in front is already handling this and not require token at all. https://github.com/ibm-cloud-security/appid-video-tutorials/blob/master/02b-simple-node-backend-app/app.js

- The browser/client should never have access to access token.

- The Authorization Server will interact with the user and once is authenticated it will return to the browser with a grant code, which in turn can be used by the Web App request an access token. With this access token the WebApp can access a Backend API for a resource.

- Use the refresh token whenever possible, this avoids re-authentication.

- Do not use OAUTH2 implicit grant (https://tools.ietf.org/html/rfc6749#section-4.2), instead use the Authorization code workflow (https://tools.ietf.org/html/rfc6749#section-4.1) whenever possible.

- Use OIDC ID token for authentication, they are represented as JSON Web Token (JWT) and it contains the requested claims.

- When using Istio:

  - Istio Adapter for AppID can handle the authentication and authorization of the client, this leaves the nodejs service without the responsibilities of handling authentication or authorization. https://github.com/ibm-cloud-security/app-identity-and-access-adapter

  - Using Istio you can handle authorization based on roles for the nodejs service, for example all authenticated users can read data via http method GET, but only users with `role=admin` are allowed to write data via http method POST.

## Learning Resources

- [Technologies Under the Hood (OAuth2, OIDC, JWT, Bearer Token)](https://www.youtube.com/watch?v=ndlk-ZhKGXM&list=PLbAYXkuqwrX2WLQqR0LUtjT77d4hisvfK&index=2)

- [Protecting Node.js Web Applications with IBM Cloud App ID](https://www.youtube.com/watch?v=6roa1ZOvwtw&list=PLbAYXkuqwrX2WLQqR0LUtjT77d4hisvfK&index=3)

- [Protecting Node.js Backend Application with IBM Cloud App ID](https://www.youtube.com/watch?v=jJLSgkHpZwA&list=PLbAYXkuqwrX2WLQqR0LUtjT77d4hisvfK&index=4)
