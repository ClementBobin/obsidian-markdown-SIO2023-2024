HTTP status codes are used to indicate the outcome of a client's request to a server. They provide information about the result of the request and the current state of the server-client interaction. Here is a list of common HTTP status codes along with their descriptions: 
## Informational (1xx) 
- **100 Continue:** The server has received the request headers and the client should proceed to send the request body.
- **101 Switching Protocols:** The server acknowledges that the client is switching to a different protocol. 
- **102 Processing:** The server has received and is processing the request, but no response is available yet. 
- **103 Early Hints:** Indicates that the server is sending hints to the client even before the final response is available.
## Successful (2xx) 
- **200 OK:** The request was successful, and the server has returned the requested data. 
- **201 Created:** The request has been fulfilled, resulting in the creation of a new resource. 
- **202 Accepted:** The request has been accepted for processing, but the processing has not been completed. 
- **203 Non-Authoritative Information:** The server successfully processed the request, but the response might be from a third-party source.
- **204 No Content:** The server successfully processed the request but has no content to send back. 
- **205 Reset Content:** The server instructs the client to reset the document view, clearing the form's input fields.
- **206 Partial Content:** The server is delivering only part of the resource due to a range header sent by the client. 
- **207 Multi-Status:** The response conveys information about multiple resources' status. 
- **208 Already Reported:** The members of a DAV binding have been enumerated already. 
- **226 IM Used:** The server has fulfilled the request for the resource, and the response is a representation of the result of one or more instance-manipulations applied to the current instance.
## Redirection (3xx) 
- **300 Multiple Choices:** Indicates multiple options for the resource, from which the client can choose. 
- **301 Moved Permanently:** The requested resource has been permanently moved to a new location. 
- **302 Found:** The requested resource is temporarily moved to a different location. 
- **303 See Other:** The response to the request can be found under a different URI.
- **304 Not Modified:** The client's cached copy is still valid, and there is no need to send a new request. 
- **305 Use Proxy:** The requested resource must be accessed through the proxy specified in the Location header. 
- **306 Switch Proxy:** No longer used. Originally meant "Subsequent requests should use the specified proxy."
- **307 Temporary Redirect:** The requested resource is temporarily moved to a different location, and the client should use the original request method to retrieve it. 
- **308 Permanent Redirect:** The requested resource is permanently moved to a different location, and the client should use the original request method to retrieve it.
## Client Error (4xx) 
- **400 Bad Request:** The server could not understand the request due to malformed syntax or invalid parameters. 
- **401 Unauthorized:** The client must authenticate itself to get the requested response. 
- **403 Forbidden:** The client does not have permission to access the requested resource. 
- **404 Not Found:** The server could not find the requested resource. 
- **405 Method Not Allowed:** The method specified in the request is not allowed for the resource. 
- **406 Not Acceptable:** The requested resource is only capable of generating content not acceptable according to the client's accept headers. 
- **407 Proxy Authentication Required:** The client must first authenticate itself with the proxy. 
- **408 Request Timeout:** The client did not produce a request within the time the server was prepared to wait. 
- **409 Conflict:** The request could not be completed due to a conflict with the current state of the target resource. 
- **410 Gone:** The target resource is no longer available at the server and no forwarding address is known. 
- **411 Length Required:** The server refuses to accept the request without a defined Content-Length. 
- **412 Precondition Failed:** One or more conditions specified in the request header fields evaluated to false. 
- **413 Payload Too Large:** The server refuses to process the request because the request payload is larger than the server is willing or able to process. 
- **414 URI Too Long:** The server is refusing to service the request because the request-target is longer than the server is willing to interpret. 
- **415 Unsupported Media Type:** The origin server is refusing to service the request because the payload is in a format not supported by this method on the target resource. 
- **416 Range Not Satisfiable:** None of the ranges in the request's Range header field overlap the current extent of the selected resource or that the set of ranges requested has been rejected due to invalid ranges or an excessive request of small or overlapping ranges. 
- **417 Expectation Failed:** The expectation given in the request's Expect header field could not be met by at least one of the inbound servers. 
- **418 I'm a teapot:** Any attempt to brew coffee with a teapot should result in the error code "418 I'm a teapot". The resulting entity body MAY be short and stout. 
- **421 Misdirected Request:** The request was directed at a server that is not able to produce a response. This can be sent by a server that is not configured to produce responses for the combination of scheme and authority that are included in the request URI. 
- **422 Unprocessable Entity:** The server understands the content type of the request entity, and the syntax of the request entity is correct, but it was unable to process the contained instructions. 
- **423 Locked:** The source or destination resource of a method is locked. 
- **424 Failed Dependency:** The method could not be performed on the resource because the requested action depended on another action and that other action failed. 
- **425 Too Early:** The server is unwilling to risk processing a request that might be replayed. 
- **426 Upgrade Required:** The server refuses to perform the request using the current protocol but might be willing to do so after the client upgrades to a different protocol. 
- **428 Precondition Required:** The origin server requires the request to be conditional. 
- **429 Too Many Requests:** The user has sent too many requests in a given amount of time ("rate limiting"). 
- **431 Request Header Fields Too Large:** The server is unwilling to process the request because its header fields are too large. 
- **451 Unavailable For Legal Reasons:** The server is denying access to the resource as a consequence of a legal demand.
## Server Error (5xx) 
- **500 Internal Server Error:** A generic error message indicating that the server has encountered an unexpected condition. 
- **501 Not Implemented:** The server does not have the functionality required to fulfill the request. 
- **502 Bad Gateway:** The server, acting as a gateway, received an invalid response from the upstream server. 
- **503 Service Unavailable:** The server is currently unable to handle the request due to temporary overloading or maintenance. 
- **504 Gateway Timeout:** The server, while acting as a gateway or proxy, did not receive a timely response from the upstream server or some other auxiliary server it needed to access in order to complete the request. 
- **505 HTTP Version Not Supported:** The server does not support, or refuses to support, the major version of HTTP that was used in the request message. 
- **506 Variant Also Negotiates:** Transparent content negotiation for the request results in a circular reference. 
- **507 Insufficient Storage:** The method could not be performed on the resource because the server is unable to store the representation needed to successfully complete the request. 
- **508 Loop Detected:** The server detected an infinite loop while processing the request. 
- **510 Not Extended:** Further extensions to the request are required for the server to fulfill it. 
- **511 Network Authentication Required:** The client needs to authenticate to gain network access. 
- **599 Network Connect Timeout Error:** This status code is not specified in any RFCs, but is used by some HTTP proxies to signal a network connect timeout error.

[And many more... ](https://umbraco.com/knowledge-base/http-status-codes/)

Please note that this is not an exhaustive list, but it covers many of the commonly encountered status codes in web development. Understanding these codes can help you diagnose and troubleshoot issues during server-client communication.