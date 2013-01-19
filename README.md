node-torrent
============


##Concept

```javascript

var Torrent = require('torrent')

Torrent.config({
	syncTracker : 'http://mytracker.site.com'
})

var transmission = Torrent.transmission({
	//port : 9091,
	//host : 'localhost',
	//username : 'admin',
	//password : 'password1'
})
var rtorrent = Torrent.rtorrent({
	//port : 9092,
	//host : 'localhost',
	//username : 'admin',
	//password : 'password1',
	//path : '/RPC1'
})
var utorrent = Torrent.utorrent({
	//port : 9093,
	//host : 'localhost',
	//username : 'admin',
	//password : 'password1'
})

var torrent = transmission.add('/my/path')

torrent.on('complete', function() {
	console.log('complete!');

	torrent.files.forEach(function(file) {
		console.log(file.path)
		console.log(file.size)
		console.log(file.name)
		console.log(file.have)
	});

	console.log(torrent.status)//SEED, # Seeding
	console.log(torrent.statusCode)//6, # Seeding

	//config.syncTracker will be used to take load of the main torrent
	//send the torrent between to torrent cleints
	rtorrent.sync(torrent)

});
torrent.on('status', function() {
	console.log(torrent.status)//SEED, # Seeding
	console.log(torrent.statusCode)//6, # Seeding
});
torrent.on('add', function() {
	//torrent was added to the client
});
torrent.on('start', function() {
	//fire when the torrent starts
});
torrent.on('stop', function() {
	//fire when the torrent stops
});
torrent.on('removed', function(withData) {
	//fire when the torrent has been removed
});

torrent.on('active', function() {
	//torrent got its first peer.
	//will only be called once.

	torrent.peers(function(err, peers) {
		peers.forEach(function(peer) {
			console.log(file.ip)
			console.log(file.port)
			console.log(file.hostname)
			console.log(file.client)
		});
	})
});

console.log(torrent.status)//CHECK, # Seeding
console.log(torrent.statusCode)//2, # Seeding


```