# No published OpenAPI

Logiwa publishes a complete, publicly readable API reference at <https://developer.logiwa.com/>
covering **81 operations**, but it publishes **no OpenAPI, Swagger, AsyncAPI, GraphQL SDL, WSDL
or .proto document**. This directory is intentionally empty of specs.

## What was probed (2026-08-25)

Every path below was probed on **developer.logiwa.com, app.logiwa.com, appapi.logiwa.com,
wms.logiwa.com, wmsapi.logiwa.com, dev.logiwa.com and www.logiwa.com**:

`/openapi.json` · `/openapi.yaml` · `/swagger.json` · `/swagger/v1/swagger.json` ·
`/v1/openapi.json` · `/api-docs` · `/swagger` · `/redoc` · `/asyncapi.yaml` · `/graphql` ·
`/.well-known/agent-card.json` · `/.well-known/agent.json` · `?wsdl` · `/service.asmx?wsdl`

Results:

| Host class | Hosts | Result |
|---|---|---|
| Docs | `developer.logiwa.com` | **404** on every spec path |
| Application | `app.logiwa.com`, `wms.logiwa.com`, `dev.logiwa.com` | **302** to login for every path |
| API gateway | `appapi.logiwa.com`, `wmsapi.logiwa.com` | **401 `Token is not valid`** on every path (blanket catch-all — this is *not* evidence a spec exists behind it) |
| Marketing | `www.logiwa.com` | **404** |

## What the docs are instead

The reference is an AngularJS application backed by two of Logiwa's own public POST endpoints —
`POST /api/Menu/GetMenuList` and `POST /api/EndPointApi/GetEndPointDetail` — which return the
navigation tree (122 nodes) and per-endpoint HTML (description, filters, properties, and example
request/response/error JSON). Everything in this repository's derived artifacts was read from
that public surface. No credentials were used and no access control was defeated.

## Confirmed live, and consistent with the docs

- `POST https://app.logiwa.com/en/api/IntegrationApi/LookUp` → **401**
  `{"Message":"Authorization has been denied for this request."}` — matches the documented envelope.
- `POST https://appapi.logiwa.com/token` → **200**
  `{"expires_in":0,".error":"invalid_grant",".error_description":"Username cannot be empty."}` — the
  documented password grant is live.

So the API is real and the documented base path and auth flow are correct; only the
machine-readable contract is missing.
