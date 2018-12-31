# mywiki
My learnings

### REST API Design - Best Practices

#### API Design

| Area          | Remarks       |
| ------------- | ------------- |
| Consumer is a developer  | Keep it simple  |
| Developer friendly  | It should be friendly to the developer and be explorable via a web browser address bar  |
| Pragmatism vs Idealism  | It should use web standards where they make sense  |
| Adoption  | It should be simple, intuitive and easy to integrate to make adoption pleasant  |
| Scale  | Through adoption we can achieve scale  |

#### What is REST

| Context          | Remarks       |
| ------------- | ------------- |
| IS  | An architectural style  |
| IS NOT  | A specification  |
| IS NOT  | A W3C standard  |
| DOES NOT  | Have a standards body backing it  |
| DOES NOT  | Have a standards body to define a linking technique  |

#### Why REST

| Area          | Remarks       |
| ------------- | ------------- |
| Scalability  | In terms of dissemination (ability to adopt, grow, interact and disperse information rapidly) and not performance  |
| Generality  | Standards specification for data transfer over HTTP  |
| Independence  | APIs independent from one another  |
| Latency (Caching)  | Reduced latency due to caching. First class citizen in REST architecture. Should always be in the back of developers mind when designing REST APIs  |
| Security  | HTTP specification allows you to support security via certain HTTP headers  |
| Encapsulation  | Lot of domain (business) specific information that need not be exposed to a REST caller. Only show things that you need to show  |

#### Why JSON

| Area          | Remarks       |
| ------------- | ------------- |
| Ubiquity  | Most web based applications can read JSON. By pupularity, top 3 - (JavaScript > Java > Ruby)  |
| Simplicity  | Very simple grammar, supports primitive strings and complex objects via maps  |
| Readbility  | Easy to add to and change over time  |
| Scalability  | Easy to add to and change over time  |
| Flexibility  | Represent almost anything you want in it  |

#### Design Time Considerations

| Outline       | Remarks       |
| ------------- | ------------- |
| Base URL  | URLs don't mean a lot in the world of REST. You should NOT design your APIs based on what URL you're going to give to people. You should think about Media-Types and Collections and Instances. Allow web browsers and REST clients to hit the same endpoint.  |
| Versioning  | URL (Pragmatism) vs Media-Type (Idealism). A lot of developers opt for URL versioning. Keep it a whole number. Add data to JSON payload and not break existing clients  |
| Resource Format  | Media-Type - Content-Type - application/json. Retain camelCase. Underscores for property/function names are unconventional for JS. Date/Time/Timestamp - ISO 8601, Use UTC!  |
| Return Values  | JSON object should at least have one property - HREF. HREF - Distributed Hypermedia is paramount! Response Body for POST - return the representation in the response payload when feasible  |
| Content Negotiation  | Accept header, Header values are comma delimited in order of preference *GET /applications/pp123* *Accept: application/json, text/plain* Resource extension overrides Accept header (useful for legacy apps which don't support Accept header translations)  |
| References (Linking)  | Hypermedia is paramount. Linking is fundamental to scalability. Tricky in JSON, XML uses XLink (W3C standard) *expand query parameter - "?expand=xxxxx"* Always a complex object, always a map with an HREF property  |
| Pagination  | Collection Resource supports query parameters: Offset, Limit For example - *.../applications?offset=50&limit=25*  |
| Query Parameters  | Offset and Limit in a noSQL DB might not be integers, they can be characters based on your data store.  |
| Associations  | Many to Many Associations, include HREF links to groups. Each mapping is a resource  |
| Errors  | 1. As descriptive as possible 2. As much information as possible 3. Developers are your customers *Example - HTTP 409 conflict error*  |
| IDs  | 1. IDs should be opaque 2. Should be globally unique 3. Avoid sequential numbers (contention, fusking) 4. Good candidates - UUID, 'Url64'  |
| Method Overloading  | *POST /applications/pp123?_method=DELETE*  |
| Resource Expansion  |   |
| Partial Responses  | PATCH/PUT  |
| Caching and ETags  | ETag is an HTTP Header that has a randomly generated string. Used by cache servers. You can't use caching servers in front of SSL connections. Public cache servers cannot be used, instead the provider has to have that infrastructure  |
| Security  | 1. Avoid sessions when possible 2. Authenticate every request if necessary (Stateless) 3. Authorize based on resource content, NOT URL! 4. OAuth 1.0a (digest based authentication for every request), Oauth2 (handshake over SSL and then it migrates to a potentially plain-text protocol using bearer tokens), over SSL ONLY 5. Use API Keys instead of Username/Passwords 6. Digest based authentication using key derivation functions 7. HTTP 401 (Unauthenticated) vs 403 (Unauthorized)  |
| Multi-Tenancy  |   |
| Maintenance  | 1. Use HTTP Redirects 2. Create abstraction layer/endpoints when migrating 3. Use well defined custom Media-Types  |

