## Dear users

We recently receive contribution offers from some of you guys. We really appriciate it. Your help means the world to us.

TeaTV applications are not (yet) open source. We have a plan to support add-ons, from that you can make your own add-on and submit in our store or install locally. 

It's not implemented for now. So if you want to contribute. Please follow our temporary documentation below. Thank you so much!

## Contribution guide

TeaTV application searches movie/tv/anime links on the web (using __Nodejs__):
1. Step 1 (Provider Crawler): From input information, search accross supported providers for embed links
2. Step 2 (Url Resolver): Convert embed links (host) to direct links.

Note:
- `provider`: free movie online website, like `5movies.to`, `www.primewire.ag`
- `host`: video hosting website, like `openload`, `streamango`
- `link`: 
    + `embed link`: video link that only play on web, like `https://openload.co/embed/aoiV82o6DQ0`
    + `direct link`: video link that return a video file, can be played on player, like `http://vjs.zencdn.net/v/oceans.mp4`

So there are two ways for you to contribute. __Add more providers__ & __Add more hosts__ to our supported list. Write your code with the structure below and email it to us [(teatv.official@gmail.com)](mailto:teatv.official@gmail.com).

Note: Keep in mind that the coding structure is subject to change and when our add-on system launches, we will provide another document with clear sample code and demo app.

### Adding more providers

```javascript
const events = {
    emitLinkEmbed(domain, embedLink, title) {
        console.log(domain, embedLink, title)
    }
}

const search = info => {

    // your code get embedlink from info

    // once you get an embed links, send it through event
    // this event is use for sending single embed link
    // one provider can have mutilple embed links, loop through all the embed and send via events.
    events.emitLinkEmbed(domain, embedLink, title);
}

module.exports = { search };
```

- Leave the events function, only change code inside function search

- `info`: object
    + `title`: String
    + `video_type`: String {`movie`, `tv`, `anime_tv`, `anime_movie`}
    + `year`: Integer
    + `season`: Integer
    + `season`: Integer
- `events.emitLinkEmbed`: function with params
    + `domain`: String. (like: `https://flixanity.mobi`)
    + `embedLink`: String. (like: `https://openload.co/embed/aoiV82o6DQ0`)
    + `title`: String
### Adding more hosts

```javascript

const youNameTheFunction = async embedLink => {
    // your code

    return { result, data };
}

module.exports = youNameTheFunction;

```

- function `youNameTheFunction(embedLink: String) : Promise<linkObj>`

- param:
    + `embedLink`: String. (like: `https://openload.co/embed/aoiV82o6DQ0`)

- return: `Promise<linkObj>`
    + `linkObj`: Object
        + `result`: Array of Objects. Required
            + `label`: String {`NOR`, `SD`, `360p`, `480p`, `720p`, `HD`, `1080p`} 
            + `file`: String (direct link)
        + `data`: Object. Required. (can be empty object)
            + `fileName`: String
            + `cookie`: String
