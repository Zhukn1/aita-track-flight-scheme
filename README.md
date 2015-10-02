# App in the Air "Track Flight" Button

The main purpose of the repo is to allow booking app developers
integrate "Track Flight" button which will open installed "App in the Air" app
and add a flight to user's "My Flights" list.

*This is preview version of the API so please let us know any comments you have*

For now only iOS is supported (starting from App in the Air 5.1),
Android coming soon ([email us](mailto:support@appintheair.mobi) to get early access).

## Implementation ##
A flight can be added using `appintheair://` URL Scheme.

Host URL will look like: `appintheair://trip`.

Before presenting "Track Flight" button in your UI you probably should check if App in the Air is installed on the current device using `UIApplication.sharedApplication().canOpenURL(url)` call.

**Required Params**

| Param name             | Value          | Comment                                            |
| ---------------------- | -------------- | -------------------------------------------------- |
| `source`               | `mybookingapp` | url scheme of the initiating app                   |
| `flight[0].from`       | `JFK`          | origin airport code (prefers iata, but icao is ok) |
| `flight[0].to`         | `LAX`          | destination airport code                           |
| `flight[0].number`     | `137`          | flight number                                      |
| `flight[0].carrier`    | `AA`           | carrier code (prefers iata, but icao is ok)        |
| `flight[0].departure`  | `1445580900`   | LOCAL departure datetime                           |
| `flight[0].arrival  `  | `1445583600`   | LOCAL arrival datetime                             |

**Optional Params (TBD)**

| Param name             | Value          | Comment                                               |
| ---------------------- | -------------- | ----------------------------------------------------- |
| `flight[0].bookRef`    | `FAK3BR`       | booking reference code                                |
| `flight[0].seat`       | `13A`          | seat number                                           |
| `flight[0].fare`       | `Y`            | fare that was used to book a flight (acc. to airline) |
| `flight[0].class`      | `Economy`      | class of the ticket                                   |
If you have more than 1 flight in one trip (multi-leg flight), than supply several flights as `flight[0] flight[1] etc`.

Don't forget to make it url-safe before passing to `canOpenURL:` or `openURL:`.

Example URL:
`appintheair://trip?source=aita&flight%5B0%5D.from=JFK&flight%5B0%5D.to=LAX&flight%5B0%5D.number=1377&flight%5B0%5D.carrier=AA&flight%5B0%5D.departure=1445580900&flight%5B0%5D.arrival=1445583600`

### Important note ###
Before submitting your app to the AppStore you must send us your app description, screenshots of your interface with one of our buttons and your url-scheme (`source` param) to [support@appintheair.mobi](mailto:support@appintheair.mobi) in order to be whitelisted by our app.

---
As of iOS9 you need to whitelist app you're going to open using `openURL:` under `LSApplicationQueriesSchemes` key in your `Info.plist` file.

If you don't have such key you can add it like this:
```
<key>LSApplicationQueriesSchemes</key>
<array>
<string>appintheair</string>
</array>
```

## Design Guidelines ##
You should place the button on the final screen of your booking flow, i.e. after the user's booked the flight.

Blue button if the preferred one, but you can also use white / black depending on your screen background.

Preferred size: 135x40 pts (270x80 px for @2x)

![](http://spronin.github.io/img/aita-track-en/aita_blue_en.png)

![](http://spronin.github.io/img/aita-track-en/aita_black_en.png)

![](http://spronin.github.io/img/aita-track-en/aita_white_en.png)

**[english .svg](http://spronin.github.io/svg/SVG_Outlined.zip)**

![](http://spronin.github.io/img/aita-track-ru/aita_blue_ru.png)

![](http://spronin.github.io/img/aita-track-ru/aita_black_ru.png)

![](http://spronin.github.io/img/aita-track-ru/aita_white_ru.png)

**[russian .svg](http://spronin.github.io/svg/SVG_RU_Outlined.zip)**

### Example usage ###
**TDB example screen from andgo.travel**