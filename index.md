# v1
# Jackpot Banner API

123

This information is for Evolution’s operators and affiliates on how to integrate the Jackpot value into websites and
banners. This information is targeted at technical teams and developers.

For general Jackpot information, download the Jackpot factsheet from the Evolution Client Area or speak to your
Evolution Key Account Manager for more information.

Please note: This document is confidential and is intended only for Evolution’s operators and affiliates.

## What is the jackpot banner api?

The Jackpot Banner API service allows you to promote the Jackpot features on both Live Casino Hold’em and Live Caribbean
Stud Poker with close to real-time information regarding the size of the Jackpot.

This service can be integrated into banner images or a text-based amount on your websites and therefore can also be
called directly from your browsers.

## Technical set-up manual

A public read-only HTTP endpoint exposed to the world without authentication with a JSON payload of jackpot amounts in
multiple currencies is required. If banner generation is needed, this should be handled by operators themselves.

The recommended use of the Jackpot Banner API is in the form of periodic server-to-server calls with some delay between
requests (e.g. 1 minute) and with caching of the result on the operator's site.

## Request format

There are multiple ways to request the Jackpot amounts depending on whether information about all the Jackpots or a
specific Jackpot in the system are needed.

A HTTP GET request to one of the following URLs need to be made. See the previous section for the format of the returned
JSON.

The service is accessible at the following URL: `https://<host>/api/jackpot/v1/pot` Operators should use their regular
host name.

## Request samples

NB: In the following examples `https://jpapi.evolutiongaming.com/` is used as the host name.

Operators should use their Live Casino host name address instead of `https://jpapi.evolutiongaming.com/`

Affiliates should use either the operator’s host name or the public host name `https://jpapi.evolutiongaming.com/`

In request sample url `lgeqrzs5bkkaalua` is the Jackpot ID

| Http get request sample                                                            | Returns                                                                    | Jackpot  |
|------------------------------------------------------------------------------------|----------------------------------------------------------------------------|----------|
| https://jpapi.evolutiongaming.com/api/jackpot/v1/pot                               | Returns Jackpot amounts for all Jackpots in all currencies                 | All      |
| https://jpapi.evolutiongaming.com/api/jackpot/v1/pot/lgeqrzs5bkkaalua              | Returns Jackpot amounts for a specific Jackpot in all available currencies | Specific |
| https://jpapi.evolutiongaming.com/api/jackpot/v1/pot/lgeqrzs5bkkaalua?currency=SEK | Returns Jackpot amount for a specific Jackpot in a specific currency       | Specific |

**IMPORTANT**: Please test your HTTP GET Request URL in any browser. It should return the Jackpot ID(s) and amount(s).

Please see samples of the response below. If you receive an error message saying 'The requested resource could not be
found', make sure that the spelling of the host name, Jackpot ID and currency code are correct.

## Supported currencies

The Jackpot amount can be read in the following currencies:

| AED | DOP | LAK | SAR |
| --- | --- | --- | --- |
| AFN | DZD | LBP | SBD |
| ALL | EGP | LKR | SCR |
| AMD | ERN | LRD | SEK |
| ANG | ETB | LSL | SHP |
| AOA | EUR | LYD | SLL |
| ARS | FJD | MAD | SOS |
| AUD | FKP | MDL | SRD |
| AWG | GBP | MGA | STD |
| AZN | GEL | MKD | SYP |
| BAM | GHS | MMK | SZL |
| BBD | GIP | MNT | THB |
| BDT | GMD | MOP | TJS |
| BGN | GNF | MRO | TMT |
| BIF | GTQ | MUR | TND |
| BMD | GYD | MVR | TOP |
| BND | HKD | MWK | TRY |
| BOB | HNL | MXN | TTD |
| BRL | HRK | MYR | TWD |
| BSD | HTG | NAD | TZS |
| BTN | HUF | NGN | UAH |
| BWP | IDR | NIO | UGX |
| BYN | ILS | NOK | USD |
| BZD | INR | NPR | UYU |
| CAD | IQD | NZD | UZS |
| CDF | IRR | PAB | VEF |
| CHF | ISK | PEN | VND |
| CLP | JMD | PGK | VUV |
| CNY | JPY | PHP | WST |
| COP | KES | PKR | XAF |
| CRC | KGS | PLN | XCD |
| CUC | KHR | QAR | XOF |
| CVE | KMF | RON | XPF |
| CZK | KRW | RSD | YER |
| DJF | KYD | RUB | ZAR |
| DK  | KZT | RWF |     |

## Active Jackpot IDs (as of 14 July 2017)

| Jackpot                                        | Jackpot ID       |
|------------------------------------------------|------------------|
| Caribbean Stud Poker Jackpot                   | lgeqrzs5bkkaalua |
| Casino Hold'em Jumbo 7 Jackpot                 | lro5gnm5cd4qac5x |
| Texas Hold'em Bonus Poker - First Five Jackpot | mbe53sxodctqaals |

## Response format

### Amounts for all active jackpots in the system

`GET /api/jackpot/v1/pot`

```json

{
  "jackpots": [
    {
      "jackpotId": "lgbdmsoxoxxqae45",
      "name": "Caribbean Stud Poker Jackpot",
      "amount": {
        "EUR": 1983456.25,
        "SEK": 20345667.45,
        "DKK": 31344682.57
      }
    },
    {
      "jackpotId": "lgjq2tp3ic2aaafu",
      "name": "Holdem Jackpot",
      "amount": {
        "EUR": 13456.25,
        "SEK": 345667.45,
        "DKK": 344682.57
      }
    }
  ]
}

```

### Amount of a specific jackpot in all currencies

`GET /api/jackpot/v1/pot/{jackpotId}`

```json


{
  "jackpotId": "lgbdmsoxoxxqae45",
  "name": "Caribbean Stud Poker Jackpot",
  "amount": {
    "EUR": 1983456.25,
    "SEK": 20345667.45,
    "DKK": 31344682.57
  }
}
```

### Amount of a specific jackpot in a specific currency

`GET /api/jackpot/v1/pot/{jackpotId}?currency={currencyCode}`

```json

{
  "jackpotId": "lgbdmsoxoxxqae45",
  "name": "Caribbean Stud Poker Jackpot",
  "amount": {
    "SEK": 20345667.45
  }
}
```

## Response encoding

The service can return either a plain text JSON or gzip-compressed response. The clients indicate which content encoding
they prefer using an Accept-Encoding header.

By default, (if the client doesn't send an Accept-Encoding header in the request) or if asked for Accept-Content:
identity the service responds with uncompressed plain JSON content.

If the client request contains an Accept-Encoding: * or Accept-Encoding: gzip header then gzip-compressed content will
be returned which will be properly indicated with a Content-Encoding: gzip response header.

## Examples

Request without explicitly passing an Accept-Encoding header:

```shell
curl -i https://jpapi.evolutiongaming.com/api/jackpot/v1/pot
```

Or with an Accept-Encoding: identity header:

```shell
curl -i --header "Accept-Encoding: identity"  https://jpapi.evolutiongaming.com/api/jackpot/v1/pot
```

Return an uncompressed response:

```text
HTTP/1.1 200 OK

Last-Modified: Tue, 11 Jul 2017 16:07:27 GMT

Access-Control-Allow-Origin: *

Access-Control-Allow-Methods: GET

Cache-Control: max-age=10, must-revalidate

Server: akka-http/10.0.9

Date: Tue, 11 Jul 2017 16:07:41 GMT

Connection: close

Content-Type: application/json

Content-Length: 5093
```

Request with an Accept-Encoding: * header:

```shell
curl -i --header "Accept-Encoding: *"  https://jpapi.evolutiongaming.com/api/jackpot/v1/pot
```

Or with an Accept-Encoding: gzip header:

```shell
curl -i --header "Accept-Encoding: gzip"  https://jpapi.evolutiongaming.com/api/jackpot/v1/pot
```

Returns a gzip-compressed response:

```text

HTTP/1.1 200 OK

Last-Modified: Fri, 14 Jul 2017 06:13:37 GMT

Access-Control-Allow-Origin: *

Access-Control-Allow-Methods: GET

Cache-Control: max-age=10, must-revalidate

Content-Encoding: gzip

Server: akka-http/10.0.9

Date: Fri, 14 Jul 2017 06:13:54 GMT

Connection: close

Content-Type: application/json

Content-Length: 2414
```

## Usage of the client

Example

```angular2html

<!doctype html>
<html ng-app="jackpots-demo">
<head>
    <title>Jackpot API Demo</title>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.2/angular.min.js"></script>
    <script>
        angular.module('jackpots-demo', [])
                .controller('JackpotController', function ($scope, $http) {
                    $http
                            .get('https://jpapi.evolutiongaming.com/api/jackpot/v1/pot')
                            .then(function (response) {
                                $scope.jackpots = response.data.jackpots;
                            });
                });
    </script>
</head>
<body>

<table ng-controller="JackpotController">
    <tr>
        <th>Jackpot ID</th>
        <th>Jackpot name</th>
        <th>Amounts</th>
    </tr>
    <tr ng-repeat="jackpot in jackpots">
        <td>{{jackpot.jackpotId}}</td>
        <td>{{jackpot.name}}</td>
        <td>
            <div ng-repeat="(currency,amount) in jackpot.amount">{{amount}} {{currency}}</div>
        </td>
    </tr>
</table>
</body>
</html>
```

## Throttling

Requests to the Jackpot Banner API service will be throttled on a per IP basis. The throttling rate will be set to the
limit of 10 requests per second from a single IP address.

For more information, please contact your Evolution KAM or Integrations Manager.