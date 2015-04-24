sofo
====

"sofo" is Couch in Esperanto. Or so I hear.

**Status**:
Researching. Development not yet started.  Currently on hold as other work takes priority.

## Purpose

REST access to Couchbase related APIs.

The couchbase ecosystem provides several miscellaneous APIs.  For example, sync_gateway provides a REST API for accessing
data it is syncing and for administering it. CBFS also provides access via REST.  Couchbase 2.0 provides admin access via
REST as well

## CHALLENGE:

### Create an elixir library that can be published to hex.pm

#### Needed functionality-

-- CRUD for access to data on the open port. 
-- Ability to load Views thru the sync gateway
-- APIs that talk to the admin port (should be a seperate module from the public port) that:
  - add & update users and create sessions on the admin API
  - The elixir side will be maps, the data pushed to the database will be JSON.  This is a JSON database
  - Have some way to support multiple "databases" (what sync_gateway calls them, couchbase calls them buckets) as we will be segregating some data this way. So the APIs can't assum the db name.
-- Tests that test all of this. 
#### Here's some docs: 
  - CouchBase Sync Gateway API Reference: http://developer.couchbase.com/mobile/develop/references/sync-gateway/index.html
  - Sync Gateway general Guide:http://developer.couchbase.com/mobile/develop/guides/sync-gateway/index.html
Here's the dependencies you'll want to use (these are vetted so please don't roll your own or go with something else without talking about it first.)
  - An elixir library for making REST calls:  https://github.com/edgurgel/httpoison
  - An elixir library to convert JSON to MAPS and back: https://github.com/devinus/poison
  - You will need to support various types of data coming from the database... eg: attachments as well as json documents (I think, see how sync_gateway handles this) Here's an example from an existing library: https://github.com/nirvana/couchie/blob/master/lib/transcoder.ex
  - Elixir testing:  http://elixir-lang.org/getting-started/mix-otp/docs-tests-and-pipelines.html
  - Check out github.com/nirvana/couchie for a previous API I wrote to access couchbase (but using a different SDK that's not appropriate for this project.)
  - 
####  You'll need to--
- Get couchbase running on your machine
- Get sync_gateway for your machine
- Set up a bucket for the gateway
- Make a elixir project called sofo, which will be mainly used to run the tests (check out elixirs built in unit testing framework
