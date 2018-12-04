# Golfmanager API

## searchAvailability

List available slots.

Authentication: public or private depending on the tenant configuration

| Argument | Type     | Required | Description |
|----------|----------|----------|-------------|
| start    | datetime | yes      | The start of the search period |
| end      | datetime | yes      | The end of the search period   |
| slots    | int      | no       | The number of green fees (default is 1)   |

Example:

```bash
curl https://test.golfmanager.es/amura/ebookings/searchAvailability.api \
 -d start="2018-10-23T16:20:00.000Z" \
 -d end="2018-10-23T17:20:00.000Z" \
 -d slots=2
```

Response:

Return a list of slots:

| Argument | Type     | Required | Description |
|----------|----------|----------|-------------|
| id          | int           | yes      | The reservation type id |
| max         | int           | no       | The maximum number of slots allowed  |
| min         | int           | no       | The minimum number of slots allowed  |
| multiple    | int           | no       | In case this type must be reserved in multiples   |
| price       | float         | yes      | The price per slot including taxes  |
| start       | datetime      | yes      | The date of this slot  |

Example:

```json
[
  {
    "id": 1,
    "max": 4,
    "min": null,
    "multiple": null,
    "name": "Green Fee 18 hoyos",
    "price": 50,
    "start": "2018-11-09T10:00:00+02:00"
  },
  {
    "id": 3,
    "max": 4,
    "min": null,
    "multiple": null,
    "name": "Green Fee 9 hoyos",
    "price": 35,
    "start": "2018-11-09T10:00:00+02:00"
  },
  {
    "id": 33,
    "max": 4,
    "min": 2,
    "multiple": 2,
    "name": "Pack 2 GF+ Buggy",
    "price": 59,
    "start": "2018-11-09T10:00:00+02:00"
  }
]
```



## makeReservation

Make a reservation. The reservation needs to be confirmed before a period of time configured by the tenant. After that it will be automatically released.

Authentication: public or private depending on the tenant configuration

Arguments: an array of reservation objects. Each reservations must specify:

| Argument | Type     | Required | Description |
|----------|----------|----------|-------------|
| type       | int         | yes      | The id obtained from searchAvailability  |
| start       | datetime      | yes      | The date of this slot  |

Example:

```bash
curl https://test.golfmanager.es/amura/ebookings/makeReservation.api \
 -d 'reservations=[{"idType":3,"start":"2018-11-09T08:20:00.000Z"}]'
```

Response:

Return the sale information to complete the payment if it needs to be prepaid 

Example:

```json
{  
   "cart":{  
      "idSale":5448,
      "quantity":1,
      "total":10,
      "units":1
   }
}
```





Golfmanager's API Terms of Service
---

- Thank you for using Golfmanager! When you develop on the Golfmanager Platform,
you agree to be bound by the following terms, so please read them carefully. 

- The API is provided as-is and without any warranty whatsoever. Golfmanager is not liable for any 
damage due to unavailable or incorrect APIs.

- Whilst Golfmanager uses all reasonable endeavours to correct any errors or omissions on the
Golfmanager Platform as soon as practicable once they have been brought to Golfmanager's
attention, Golfmanager makes no promises, guarantees, representations or warranties of
any kind whatsoever (express or implied).

- Abuse or excessively frequent requests to Golfmanager via the API may result in 
the temporary or permanent suspension of your Account's access to the API. Golfmanager,
in our sole discretion, will determine abuse or excessive usage of the API. We will make
a reasonable attempt to warn you via email prior to suspension.

- Golfmanager has the right to change these General API Terms and Conditions and 
any Specific API Terms and Conditions.