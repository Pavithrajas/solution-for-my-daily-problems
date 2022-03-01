* Following query is the example to get value from json field (column) and to get the first item in the list, and to convert the timestamp to epoch, 
converting string to int/timestamp 

    ```
    Query: select booking_no, created_on, ((request_payload -> 'dcp' -> 'deliveryQuote' -> 'theatres' -> 0 ->> 'deliveryDate')::int 
    - extract(epoch from (request_payload -> 'dcp' ->> 'deliveryDate')::timestamp) from bookings where created_on < '2022-02-28 06:05:31.667';
   
    Explanation: 
    Lets say I have a bookings table with request_payload as a jsonb column. Sample request_payload jsonb value as below,
          {
            "dcp": {
              "deliveryDate": "2021-02-02T23:59:59+00:00",
              "deliveryQuote": {
                "theatres": [
                  {
                    "id": "abcd",
                    "price": 0,
                    "timezone": "Asia/Kolkata",
                    "deliveryDate": 1612290599
                  }
                ]
              }
            }
          }
     
     So if i want to get `deliveryDate` which is under `dcp` field, then we have to get like this, request_payload -> 'dcp' ->> 'deliveryDate'
     Note: 
     ->  will give jsonb value 
     ->> will give string value 
     to convert the string to int we have to use ::int 
     to convert the string to timestamp we have to use ::timestamp 
     to convert timestamp to epoch we have to use extract(epoch from timestamp value)
    ```
    
    
