```mermaid
sequenceDiagram
    title Shipping Ships API

participant Client
participant Python
participant JSONServer
participant ShipView
participant Database
Client->>Python:GET request to "/ships"
Python->>JSONServer:Run do_GET() method
JSONServer->>ShipView:Run list_ships() function
ShipView->>Database:Fetch instances of 'ships' entity from SQLite database
Database->>ShipView:Return list of ship instances as object representations
loop 
ShipView->ShipView:

note right of ShipView:for each object representation in returned ships list,

note right of ShipView:append to 'ships' list as Python dictionary
end
note right of ShipView:Convert to JSON encoded string and store in serialized list
note right of ShipView
ShipView->>JSONServer:Return Serialized Python list of ships
JSONServer-->>Client: Here's all yer ships (in JSON format)

```