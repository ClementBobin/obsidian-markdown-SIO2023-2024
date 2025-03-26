## Overview

Scalar provides seamless integrations with various frameworks and platforms, making API development easier and more efficient. It supports a wide range of technologies, including:

### Supported Integrations

- **Backend Frameworks**:
    
    - .NET
        
    - Nitro
        
    - Platformatic
        
    - FastAPI
        
    - Hono
        
    - NestJS
        
    - Nuxt
        
    - Rust
        
    - AdonisJS
        
    - Elysia
        
    - Express
        
    - Fastify
        
    - GO
        
    - Laravel
        
    - Litestar
        
    - Next.js
        
- **Frontend & Documentation**:
    
    - HTML
        
    - React
        
    - Vue.js
        
    - Docusaurus
        

## Installation

To install Scalar in a .NET project, run:

```sh
dotnet add package Scalar.AspNetCore
```

For other frameworks, check the [official Scalar documentation](https://scalar.com/#integrations).

## Usage

Here’s a basic example of using Scalar with .NET:

```csharp
using Scalar.AspNetCore;

var builder = WebApplication.CreateBuilder();

builder.Services.AddOpenApi();

var app = builder.Build();

app.MapOpenApi();

if (app.Environment.IsDevelopment())
{
    app.MapScalarApiReference();
}

app.MapGet("/", () => "Hello world!");

app.Run();
```

## OpenAPI Support

Once Scalar is integrated, you can:

- **Import JSON**: Use the generated OpenAPI JSON in the [Scalar Client](./Scalar%20API%20Client) or [Scalar Docs](./Scalar%20Dashboard) for better API exploration.
    
- **Download OpenAPI JSON**: Export the OpenAPI specification to integrate with third-party tools or documentation platforms.
## Prebuilt Examples

For ready-to-use implementations in different frameworks, check out the [Scalar API Examples Repository](https://github.com/ClementBobin/Api):

- [Fastify](https://github.com/ClementBobin/Api/tree/FastifyPrisma)
    
- [Express](https://github.com/ClementBobin/Api/tree/ExpressPrisma)
    
- [NextJS](https://github.com/ClementBobin/Api/tree/NextJsPrisma)
    
- [Laravel](https://github.com/ClementBobin/Api/tree/Laravel)
    

For additional integrations, visit the official [Scalar Integrations Page](https://scalar.com/#integrations).