# AlphaReign
Docs, About, Etc


AlphaReign consists of several parts that make up the entire system.  By all means, not everything is required, but if something doesn't work your probably SOL.  I will try and work through issues that people create on github for the correct repositories, but my time is limited, so don't expect instant feedback.  If you become annoying, I won't answer you at all.  If you contribute, you will get much more of my time (not that's it's that valuable to you, but it is to me)

So, first things first.  AlphaReign's main search engine is ElasticSearch.  If you don't know what that is, or how it works, better start studying.  There are two different languages.  This is mostly because I didn't have time to convert the website (in PHP) over to Javascript (what the scraper is written in).  Any help to do so, would be greatly appreciated.  It should actually be pretty straight forward, just haven't had the time.

So, you have PHP and Javascript to deal with.  If you don't know either, this probably isn't the place for you.  Other things to worry about are the webserver (nginx / apache), the database (MySQL / MariaDB), the package managers (npm / composer) and probably a slew of other things I haven't thought about.

Anyway, back to the start.  AR's search engine is ElasticSearch.  We use the scraper to listen to the DHT and add torrents to ElasticSearch when one is request of it.  When the scraper is asked for a torrent, it passes it along the DHT network, but also grabs the torrent hash and makes a request to others to grab what information it can.  Once it has that information, it upserts that data into ElasticSearch.

The scraper also updates seeders / leechers and category information.  We do this in separate systems, because a) this was done piecemeal and b) some information needs to get updated constantly (seeders / leechers)

These two processes (categorize.js / scrape.js) run continuously and grab the last updated torrents and process them.  If you know javascript, you will see what I mean.

That's one side.

The other side of the equation is the website.  Now, since we have everything in ElasticSearch, we could write the website in anything.  PHP was the down and dirty for me, but ideally it would be in whatever language you know best.

That being said, it does all the user authentication, and pushind data around that's used on the website.  Things like flagging, commenting, etc.  Comments, flags, voting is stored in the database.  We push the votes and flags to ElasticSearch so we can filter on it along with resolving the data quickly from a search.

That about sums it up.  I am sure I am missing a bunch of info, so, if you have questsions, ask them.  I will try and get to them, but it won't be instant