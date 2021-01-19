# getTvhProgram.sh
bash commands to get information from TVHeadend Server epg API



Similarly as my getMythProgram.sh bash script. This one will pull from a TVH server using its API. 
Which I reference from the TVH-API-docs


so far i tested a few stanzas:
*using  limit & channel name which works
#you can get the list from http://TVH_SERVER:9981/api/channel/list

*Don't forget to change my ip to yours when testing.

*eg from mine I tested 'comet'

http://192.168.1.218:9981/api/epg/events/grid?limit=1&channel=comet

```
{"totalCount":24,"entries":[{"eventId":817,"episodeId":818,"channelName":"comet","channelUuid":"cf544d99dc70845ef8956eb12f67f544","channelNumber":"16.3","start":1611025201,"stop":1611028801,"title":"Quantum Leap","description":"As a blind pianist in 1964, Sam has the chance to foil the murder of the musician's girlfriend (Cynthia Bain).","nextEventId":819}]}
```

*After reading the API docs more I saw the NOW option for only those currently playing 
*The following shows all 
http://192.168.1.218:9981/api/epg/events/grid?mode=now

```
{"totalCount":9,"entries":[{"eventId":47,"episodeId":48,"channelName":"KEVU-DT","channelUuid":"df5c5000a9440fe40be8db499403ee36","channelNumber":"34.2","start":1611025199,"stop":1611028799,"title":"The Drew Barrymore Show","nextEventId":49},{"eventId":275,"episodeId":276,"channelName":"DABL","channelUuid":"86266e279730052fd8546fe2c18b8aa4","channelNumber":"23.2","start":1611025199,"stop":1611028799,"title":"The Drew Barrymore Show","nextEventId":277},{"eventId":213,"episodeId":214,"channelName":"KLSR-HD","channelUuid":"83768a3c4222ded7ff7798937c728771","channelNumber":"34.1","start":1611025199,"stop":1611026999,"title":"Oregon's News @7","nextEventId":215},{"eventId":269,"episodeId":270,"channelName":"KEVU-HD","channelUuid":"52255ad28ad2f35f7c118f4dd8ce2733","channelNumber":"23.1","start":1611025199,"stop":1611028799,"title":"The Drew Barrymore Show","nextEventId":271},{"eventId":293,"episodeId":294,"channelName":"OPB-HD Channel","channelUuid":"9a31c087f7223bf2a169319b818e9f04","channelNumber":"28.1","start":1611025201,"stop":1611028801,"title":"PBS NewsHour","nextEventId":295},{"eventId":817,"episodeId":818,"channelName":"comet","channelUuid":"cf544d99dc70845ef8956eb12f67f544","channelNumber":"16.3","start":1611025201,"stop":1611028801,"title":"Quantum Leap","description":"As a blind pianist in 1964, Sam has the chance to foil the murder of the musician's girlfriend (Cynthia Bain).","nextEventId":819},{"eventId":823,"episodeId":824,"channelName":"CW Plus","channelUuid":"9d94c6bb1e08ccb355a26823a29965ba","channelNumber":"16.2","start":1611025201,"stop":1611027001,"title":"Family Guy","description":"When Chris' Mexican girlfriend, Isabella, gets deported, he steps up to take care of her twin babies, only to find she can't return to the U.S.","nextEventId":825},{"eventId":65,"episodeId":66,"channelName":"CBS13","channelUuid":"e3dbc14ddfdafc4fd38bfca36e8a2c0a","channelNumber":"13.1","start":1611025201,"stop":1611027001,"title":"Jeopardy!","description":"The Emmy-winning quiz show features a unique answer-and-question format.","nextEventId":67},{"eventId":15,"episodeId":16,"channelName":"NBC16","channelUuid":"90551674f3341e9cd781b234ccf3a6a2","channelNumber":"16.1","start":1611025201,"stop":1611027001,"title":"The Big Bang Theory","nextEventId":17}]}
```



*using curl in shell piped out through jq gives a nice format vs long lines.
```
curl -s 'http://kelsie:1234@192.168.1.218:9981/api/epg/events/grid?mode=now'|jq
{
  "totalCount": 9,
  "entries": [
    {
      "eventId": 47,
      "episodeId": 48,
      "channelName": "KEVU-DT",
      "channelUuid": "df5c5000a9440fe40be8db499403ee36",
      "channelNumber": "34.2",
      "start": 1611025199,
      "stop": 1611028799,
      "title": "The Drew Barrymore Show",
      "nextEventId": 49
    },
    {
      "eventId": 275,
      "episodeId": 276,
      "channelName": "DABL",
      "channelUuid": "86266e279730052fd8546fe2c18b8aa4",
      "channelNumber": "23.2",
      "start": 1611025199,
      "stop": 1611028799,
      "title": "The Drew Barrymore Show",
      "nextEventId": 277
    },
    {
      "eventId": 269,
      "episodeId": 270,
      "channelName": "KEVU-HD",
      "channelUuid": "52255ad28ad2f35f7c118f4dd8ce2733",
      "channelNumber": "23.1",
      "start": 1611025199,
      "stop": 1611028799,
      "title": "The Drew Barrymore Show",
      "nextEventId": 271
    },
    {
      "eventId": 293,
      "episodeId": 294,
      "channelName": "OPB-HD Channel",
      "channelUuid": "9a31c087f7223bf2a169319b818e9f04",
      "channelNumber": "28.1",
      "start": 1611025201,
      "stop": 1611028801,
      "title": "PBS NewsHour",
      "nextEventId": 295
    },
    {
      "eventId": 817,
      "episodeId": 818,
      "channelName": "comet",
      "channelUuid": "cf544d99dc70845ef8956eb12f67f544",
      "channelNumber": "16.3",
      "start": 1611025201,
      "stop": 1611028801,
      "title": "Quantum Leap",
      "description": "As a blind pianist in 1964, Sam has the chance to foil the murder of the musician's girlfriend (Cynthia Bain).",
      "nextEventId": 819
    },
    {
      "eventId": 215,
      "episodeId": 216,
      "channelName": "KLSR-HD",
      "channelUuid": "83768a3c4222ded7ff7798937c728771",
      "channelNumber": "34.1",
      "start": 1611026999,
      "stop": 1611028799,
      "title": "Judge Judy",
      "nextEventId": 217
    },
    {
      "eventId": 825,
      "episodeId": 826,
      "channelName": "CW Plus",
      "channelUuid": "9d94c6bb1e08ccb355a26823a29965ba",
      "channelNumber": "16.2",
      "start": 1611027001,
      "stop": 1611028801,
      "title": "Family Guy",
      "description": "When Peter's boss (Carrie Fisher) tells him he needs to pick up the pace, Lois goes to the brewery to help him.",
      "nextEventId": 827
    },
    {
      "eventId": 67,
      "episodeId": 68,
      "channelName": "CBS13",
      "channelUuid": "e3dbc14ddfdafc4fd38bfca36e8a2c0a",
      "channelNumber": "13.1",
      "start": 1611027001,
      "stop": 1611028801,
      "title": "Wheel of Fortune",
      "description": "In a classic game-show version of &quot;Hangman,&quot; contestants solve word puzzles for cash and prizes.",
      "nextEventId": 69
    },
    {
      "eventId": 17,
      "episodeId": 18,
      "channelName": "NBC16",
      "channelUuid": "90551674f3341e9cd781b234ccf3a6a2",
      "channelNumber": "16.1",
      "start": 1611027001,
      "stop": 1611028801,
      "title": "The Big Bang Theory",
      "nextEventId": 19
    }
  ]
}
```

*Getting one channel again by NAME but parsed through jq
```
curl -s 'http://kelsie:1234@192.168.1.218:9981/api/epg/events/grid?mode=now&channel=CBS13'|jq
{
  "totalCount": 1,
  "entries": [
    {
      "eventId": 67,
      "episodeId": 68,
      "channelName": "CBS13",
      "channelUuid": "e3dbc14ddfdafc4fd38bfca36e8a2c0a",
      "channelNumber": "13.1",
      "start": 1611027001,
      "stop": 1611028801,
      "title": "Wheel of Fortune",
      "description": "In a classic game-show version of &quot;Hangman,&quot; contestants solve word puzzles for cash and prizes.",
      "nextEventId": 69
    }
  ]
}
```

*This will give you a nice channel list in json
```
curl -s 'http://user:passwd@TVH_SERVER:9981/api/channel/grid?sort=number'|jq

```
{
  "entries": [
    {
      "uuid": "e3dbc14ddfdafc4fd38bfca36e8a2c0a",
      "enabled": true,
      "autoname": true,
      "name": "CBS13",
      "number": "13.1",
      "epgauto": true,
      "epggrab": [],
      "dvr_pre_time": 0,
      "dvr_pst_time": 0,
      "epg_running": -1,
      "services": [
        "9e9c4112e3d895b6986ec0132b374509"
      ],
      "tags": [
        "d7050e9df03fc86abde7fb5b04502df5",
        "ce74bb7a975412b626629cfea79aca20",
        "11fdd6edafcbbecf6475fd992530d200"
      ],
      "bouquet": ""
    },
    {
      "uuid": "e51803cab122b7739a65926dd773e950",
      "enabled": true,
      "autoname": true,
      "name": "TBD",
      "number": "13.2",
      "epgauto": true,
      "epggrab": [],
      "dvr_pre_time": 0,
      "dvr_pst_time": 0,
      "epg_running": -1,
      "services": [
        "5a99c6600b304f153e88cea9341ec9b8"
      ],
      "tags": [
        "d7050e9df03fc86abde7fb5b04502df5",
        "ce74bb7a975412b626629cfea79aca20",
        "11fdd6edafcbbecf6475fd992530d200"
      ],
      "bouquet": ""
    },
    {
      "uuid": "027bd039eddf1bf87ac0e4a3b235a40c",
      "enabled": true,
      "autoname": true,
      "name": "Charge!",
      "number": "13.3",
      "epgauto": true,
      "epggrab": [],
      "dvr_pre_time": 0,
      "dvr_pst_time": 0,
      "epg_running": -1,
      "services": [
        "14697001fdbefc17089d0ae3c3f87e0e"
      ],
      "tags": [
        "d7050e9df03fc86abde7fb5b04502df5",
        "ce74bb7a975412b626629cfea79aca20",
        "11fdd6edafcbbecf6475fd992530d200"
      ],
      "bouquet": ""
    },
    {
      "uuid": "90551674f3341e9cd781b234ccf3a6a2",
      "enabled": true,
      "autoname": true,
      "name": "NBC16",
      "number": "16.1",
      "epgauto": true,
      "epggrab": [],
      "dvr_pre_time": 0,
      "dvr_pst_time": 0,
      "epg_running": -1,
      "services": [
        "46e5363d58f3835135f5cc2908482056"
      ],
      "tags": [
        "d7050e9df03fc86abde7fb5b04502df5",
        "ce74bb7a975412b626629cfea79aca20",
        "11fdd6edafcbbecf6475fd992530d200"
      ],
      "bouquet": ""
    },
    {
      "uuid": "9d94c6bb1e08ccb355a26823a29965ba",
      "enabled": true,
      "autoname": true,
      "name": "CW Plus",
      "number": "16.2",
      "epgauto": true,
      "epggrab": [],
      "dvr_pre_time": 0,
      "dvr_pst_time": 0,
      "epg_running": -1,
      "services": [
        "7c87b2fed991fbd6fae7651be9eefdc6"
      ],
      "tags": [
        "d7050e9df03fc86abde7fb5b04502df5",
        "ce74bb7a975412b626629cfea79aca20",
        "11fdd6edafcbbecf6475fd992530d200"
      ],
      "bouquet": ""
    },
    {
      "uuid": "cf544d99dc70845ef8956eb12f67f544",
      "enabled": true,
      "autoname": true,
      "name": "comet",
      "number": "16.3",
      "epgauto": true,
      "epggrab": [],
      "dvr_pre_time": 0,
      "dvr_pst_time": 0,
      "epg_running": -1,
      "services": [
        "c8512c8f99e8ce6d4664403fb3f80c23"
      ],
      "tags": [
        "d7050e9df03fc86abde7fb5b04502df5",
        "ce74bb7a975412b626629cfea79aca20",
        "11fdd6edafcbbecf6475fd992530d200"
      ],
      "bouquet": ""
    },
    {
      "uuid": "52255ad28ad2f35f7c118f4dd8ce2733",
      "enabled": true,
      "autoname": true,
      "name": "KEVU-HD",
      "number": "23.1",
      "epgauto": true,
      "epggrab": [],
      "dvr_pre_time": 0,
      "dvr_pst_time": 0,
      "epg_running": -1,
      "services": [
        "1861c937e36510d4d181e6db9ac4b80f"
      ],
      "tags": [
        "d7050e9df03fc86abde7fb5b04502df5",
        "ce74bb7a975412b626629cfea79aca20",
        "11fdd6edafcbbecf6475fd992530d200"
      ],
      "bouquet": ""
    },
    {
      "uuid": "86266e279730052fd8546fe2c18b8aa4",
      "enabled": true,
      "autoname": true,
      "name": "DABL",
      "number": "23.2",
      "epgauto": true,
      "epggrab": [],
      "dvr_pre_time": 0,
      "dvr_pst_time": 0,
      "epg_running": -1,
      "services": [
        "2272a17f1165a1ad95b169c1586baf14"
      ],
      "tags": [
        "d7050e9df03fc86abde7fb5b04502df5",
        "ce74bb7a975412b626629cfea79aca20",
        "11fdd6edafcbbecf6475fd992530d200"
      ],
      "bouquet": ""
    },
    {
      "uuid": "9a31c087f7223bf2a169319b818e9f04",
      "enabled": true,
      "autoname": true,
      "name": "OPB-HD Channel",
      "number": "28.1",
      "epgauto": true,
      "epggrab": [],
      "dvr_pre_time": 0,
      "dvr_pst_time": 0,
      "epg_running": -1,
      "services": [
        "43f4f262431045934e8cefae46dfa0d5"
      ],
      "tags": [
        "d7050e9df03fc86abde7fb5b04502df5",
        "ce74bb7a975412b626629cfea79aca20",
        "11fdd6edafcbbecf6475fd992530d200"
      ],
      "bouquet": ""
    },
    {
      "uuid": "5cb16135817e51e6b9ff74e5203bccaf",
      "enabled": true,
      "autoname": true,
      "name": "OPBPlus",
      "number": "28.2",
      "epgauto": true,
      "epggrab": [],
      "dvr_pre_time": 0,
      "dvr_pst_time": 0,
      "epg_running": -1,
      "services": [
        "7605364189caadff0b76176353edaa25"
      ],
      "tags": [
        "d7050e9df03fc86abde7fb5b04502df5",
        "ce74bb7a975412b626629cfea79aca20",
        "11fdd6edafcbbecf6475fd992530d200"
      ],
      "bouquet": ""
    },
    {
      "uuid": "3e93e45c972f7423413ebdce07233278",
      "enabled": true,
      "autoname": true,
      "name": "OPBKids",
      "number": "28.3",
      "epgauto": true,
      "epggrab": [],
      "dvr_pre_time": 0,
      "dvr_pst_time": 0,
      "epg_running": -1,
      "services": [
        "9d49471cfd816cff52f4a7a0d6970313"
      ],
      "tags": [
        "d7050e9df03fc86abde7fb5b04502df5",
        "ce74bb7a975412b626629cfea79aca20",
        "11fdd6edafcbbecf6475fd992530d200"
      ],
      "bouquet": ""
    },
    {
      "uuid": "62ff00f6c4bf770c1ae5384678b891ef",
      "enabled": true,
      "autoname": true,
      "name": "OPB-FM",
      "number": "28.4",
      "epgauto": true,
      "epggrab": [],
      "dvr_pre_time": 0,
      "dvr_pst_time": 0,
      "epg_running": -1,
      "services": [
        "42195a7c05dde7f43f70ac319b089b4b"
      ],
      "tags": [
        "d7050e9df03fc86abde7fb5b04502df5",
        "ce74bb7a975412b626629cfea79aca20",
        "11fdd6edafcbbecf6475fd992530d200"
      ],
      "bouquet": ""
    },
    {
      "uuid": "83768a3c4222ded7ff7798937c728771",
      "enabled": true,
      "autoname": true,
      "name": "KLSR-HD",
      "number": "34.1",
      "epgauto": true,
      "epggrab": [],
      "dvr_pre_time": 0,
      "dvr_pst_time": 0,
      "epg_running": -1,
      "services": [
        "e394df4fdb2da0c4122c202095dbaa86"
      ],
      "tags": [
        "d7050e9df03fc86abde7fb5b04502df5",
        "ce74bb7a975412b626629cfea79aca20",
        "11fdd6edafcbbecf6475fd992530d200"
      ],
      "bouquet": ""
    },
    {
      "uuid": "df5c5000a9440fe40be8db499403ee36",
      "enabled": true,
      "autoname": true,
      "name": "KEVU-DT",
      "number": "34.2",
      "epgauto": true,
      "epggrab": [],
      "dvr_pre_time": 0,
      "dvr_pst_time": 0,
      "epg_running": -1,
      "services": [
        "22cc0657256838b857dad77a83259663"
      ],
      "tags": [
        "d7050e9df03fc86abde7fb5b04502df5",
        "ce74bb7a975412b626629cfea79aca20",
        "11fdd6edafcbbecf6475fd992530d200"
      ],
      "bouquet": ""
    }
  ],
  "total": 14
}




```



Note in the JSON output it uses UNIX EPOC times, which are great for easy math getting duration of a show!
Just subtract start from stop for the duration in seconds.






eg. for Summary Grid
#
http://TVH_SERVER:9981/api/epg/events/grid


 
 
 
 

