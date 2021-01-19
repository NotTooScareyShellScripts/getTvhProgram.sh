# getTvhProgram.sh
bash command line commands to get information from TVHeadend Server epg API



Similarly as my getMythProgram.sh bash script. This one will pull from a TVH server using its API. 
Which I reference from the TVH-API-docs


#so far i tested using  limit & channel name which works
#you can get the list from http://TVH_SERVER:9981/api/channel/list

#eg from mine I tested 'comet'
http://192.168.1.218:9981/api/epg/events/grid?limit=1&channel=comet

```
{"totalCount":24,"entries":[{"eventId":817,"episodeId":818,"channelName":"comet","channelUuid":"cf544d99dc70845ef8956eb12f67f544","channelNumber":"16.3","start":1611025201,"stop":1611028801,"title":"Quantum Leap","description":"As a blind pianist in 1964, Sam has the chance to foil the murder of the musician's girlfriend (Cynthia Bain).","nextEventId":819}]}
```

Note in the JSON output it uses UNIX EPOC times, which are great for easy math getting duration of a show!
Just subtract start from stop for the duration in seconds.






eg. for Summary Grid
#
http://TVH_SERVER:9981/api/epg/events/grid


 
 
 
 

