# Introduction


# Terminology

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in {{!RFC2119}}.

- Media Server
- Channel
- Viewer


# Overview



# Protocol Operation

## Create viewer resource

### Request
~~~
POST /channel/<channelId>
Content-type: application/json
Body:
{}
~~~

### Response
~~~
Status: 201
Location: Resource URL
Content-type: application/json
Body:
{
   "offer": "...",
   "mediaStreams": [
      {"msid", "senderId"}
   ]
}
~~~

## Send SDP answer

### Request
~~~
PUT /channel/<channelId>/<viewerId>
Content-type: application/json
Body:
{
   "answer": "..."
}
~~~

### Response
~~~
Status: 204
~~~

## Send SDP ICE candidate

### Request
~~~
PATCH /channel/:channelId/:viewerId
{
   "candidate": "..."
}
~~~

### Response
~~~
Status: 204
~~~
