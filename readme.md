The Pirate Bay node.js client
=============================
[![Build Status](https://travis-ci.org/t3chnoboy/thepiratebay.svg?branch=master)](https://travis-ci.org/t3chnoboy/thepiratebay)
[![NPM version](https://badge.fury.io/js/thepiratebay.svg)](http://badge.fury.io/js/thepiratebay)
[![Dependency Status](https://gemnasium.com/t3chnoboy/thepiratebay.svg)](https://gemnasium.com/t3chnoboy/thepiratebay)

<p align="center">
  <img src="https://i.imgur.com/xP3s8Xum.png"/>
</p>

## Installation
[![NPM](https://nodei.co/npm/thepiratebay.png?downloads=true)](https://nodei.co/npm/thepiratebay/)

Install using npm:
```sh
npm install thepiratebay
```

## Usage

```javascript
  const tpb = require('thepiratebay');
```
All methods are asynchronous!
You can use promises, es6 generators, or async/await

Using promises:
```javascript
  tpb.search('Game of Thrones', {
  	category: '205'
  })
  .then(function(results){
  	console.log(results);
  })
  .catch(function(err){
  	console.log(err);
  });
```

Using ES7 async/await
```javascript
async search() {
  const searchResults = await tpb.search({
    category: '205', page: '3', orderBy: '5'
  })
}
```

## Methods

### getTorrent
```javascript
  /* takes an id or a link */
  tpb.getTorrent('10676856')
  .then(function(results){
    console.log(results);
  })
  .catch(function(err){
    console.log(err);
  });

/*
output:
  {
    name: 'The Amazing Spider-Man 2 (2014) 1080p BrRip x264 - YIFY',
    filesCount: 2,
    size: '2.06 GiB (2209149731 Bytes)',
    seeders: '14142',
    leechers: '3140',
    uploadDate: '2014-08-02 08:15:25 GMT',
    torrentLink: undefined,
    magnetLink: 'magnet:?xt=urn:btih:0259f6b98a7ca160a36f13457c89344c7dd34000&dn=The+Amazing+Spider-Man+2+%282014%29+1080p+BrRip+x264+-+YIFY&tr=udp%3A%2F%2Ftracker.openbittorrent.com%3A80&tr=udp%3A%2F%2Ftracker.publicbt.com%3A80&tr=udp%3A%2F%2Ftracker.istole.it%3A6969&tr=udp%3A%2F%2Fopen.demonii.com%3A1337',
    link: 'http://thepiratebay.se/torrent/10676856/',
    id: '10676856',
    description: '-------------------------------------------------------------------------------\n\n-------------------------------------------------------------------------------\n\n\nGet all YIFYs newest releases first at \n\nAlso there you will find a list of upcoming uploads, instant chat, account registration and an effective movie search.\n\n\n-------------------------------------------------------------------------------\n\n-------------------------------------------------------------------------------\t\n\n \nhttp://www.imdb.com/title/tt1872181/\n\n\nIMDB RATING: 7.3\n\nFORMAT.......................: MP4\nCODEC........................: X264\nGENRE........................: Action\nFILE SIZE....................: 2.06 GB\nRESOLUTION...................: 1920*800\nFRAME RATE...................: 23.976 fps\nLANGUAGE.....................: English\nSUBTITLES....................: NONE\nRUNTIME......................: 141 mins\n\n\n\nWe\'ve always known that Spider-Man\'s most important conflict has been within himself: the struggle between the ordinary obligations of Peter Parker and the extraordinary responsibilities of Spider-Man. But in The Amazing Spider-Man 2, Peter Parker finds that his greatest battle is about to begin. It\'s great to be Spider-Man (Andrew Garfield). For Peter Parker, there\'s no feeling quite like swinging between skyscrapers, embracing being the hero, and spending time with Gwen (Emma Stone). But being Spider-Man comes at a price: only Spider-Man can protect his fellow New Yorkers from the formidable villains that threaten the city. With the emergence of Electro (Jamie Foxx), Peter must confront a foe far more powerful than he. And as his old friend, Harry Osborn (Dane DeHaan), returns, Peter comes to realize that all of his enemies have one thing in common: Oscorp. Directed by Marc Webb. Produced by Avi Arad and Matt Tolmach. Screenplay by Alex Kurtzman & Roberto Orci & Jeff Pinkner. Screen Story by Alex Kurtzman & Roberto Orci & Jeff Pinkner and James Vanderbilt. Based on the Marvel comic book by Stan Lee and Steve Ditko.\n \nhttp://istoreimg.com/i/53dc81f88e33e.html \n \nhttp://istoreimg.com/i/53dc81f8c0913.html \n \nhttp://istoreimg.com/i/53dc81f8f1e0f.html',
    picture: 'http://image.bayimg.com/bdca01a243abf68d192fe74aa14ad35fa1a99add.jpg'
  }
*/
```

### topTorrents
http://thepiratebay.se/top
```javascript
  tpb.topTorrents() // returns top 100 torrents
  tpb.topTorrents('400') // returns top 100 torrents for the category '400' aka Games
```

### recentTorrents
http://thepiratebay.se/recent
```javascript
  tpb.recentTorrents() // returns the most recent torrents
```

### userTorrents
http://thepiratebay.se/user/YIFY/3/5/0
```javascript
  tpb.userTorrents('YIFY', { page: '3', orderBy: '5' })
```

### getCategories
```javascript
  tpb.getCategories();

/* returns an array of categories
[
  ...
  { name: 'Video',
    id: '200',
    subcategories:
     [ { id: '201', name: 'Movies' },
       { id: '202', name: 'Movies DVDR' },
       { id: '203', name: 'Music videos' },
       { id: '204', name: 'Movie clips' },
       { id: '205', name: 'TV shows' },
       { id: '206', name: 'Handheld' },
       { id: '207', name: 'HD - Movies' },
       { id: '208', name: 'HD - TV shows' },
       { id: '209', name: '3D' },
       { id: '299', name: 'Other' } ]
     }
  ...
] */
```
### search
```javascript
  // takes a search query and options
  tpb.search('Game of Thrones', { category: '205', page: '3', orderBy: '5' })

/* returns an array of search results:
[
  {
    name: 'Game of Thrones (2014)(dvd5) Season 4 DVD 1 SAM TBS',
    size: '4.17 GiB',
    link: 'http://thepiratebay.se/torrent/10013794/Game_of_Thrones_(2014)(dvd5)_Season_4_DVD_1_SAM_TBS',
    category: { id: '200', name: 'Video' },
    seeders: '125',
    leechers: '552',
    uploadDate: 'Today 00:57',
    magnetLink: 'magnet:?xt=urn:btih:4e6a2304fed5841c04b16d61a0bac5c67973acab&dn=Game+of+Thrones+%282014%29%28dvd5%29+Season+4+DVD+1+SAM+TBS&tr=udp%3A%2F%2Ftracker.openbittorrent.com%3A80&tr=udp%3A%2F%2Ftracker.publicbt.com%3A80&tr=udp%3A%2F%2Ftracker.istole.it%3A6969&tr=udp%3A%2F%2Ftracker.ccc.de%3A80&tr=udp%3A%2F%2Fopen.demonii.com%3A1337',
    subcategory: { id: '202', name: 'Movies DVDR' },
    torrentLink: '//piratebaytorrents.info/10013794/Game_of_Thrones_(2014)(dvd5)_Season_4_DVD_1_SAM_TBS.10013794.TPB.torrent'
  },
  ...
]
*/
```
#### Search query options:

* category
  * 0   - all
  * 101 - 699
* page
  * 0 - 99
* orderBy
  * 1  - name desc
  * 2  - name asc
  * 3  - date desc
  * 4  - date asc
  * 5  - size desc
  * 6  - size asc
  * 7  - seeds desc
  * 8  - seeds asc
  * 9  - leeches desc
  * 10 - leeches asc
