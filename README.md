# fluent-bit-testing

This repo helps to test the fluentbit setup using docker-compose.


# To Test
Start up the require containers using docker compose:

  `docker-compose up`

In another window (from the git repo root directory) create a log entry:

  echo '{"log":"(See full trace by running task with --trace)\n","stream":"stderr","time":"2020-11-16T12:30:16.275664751Z"}' >> logs/test-deploy-58d54d8c67_default_container-name-123456786.log


In a couple of min query the ES pod:

  curl "localhost:9200/_search?pretty"   -H 'Content-Type: application/json'


The results should be similar to:

 {
   "took" : 3,
   "timed_out" : false,
   "_shards" : {
     "total" : 2,
     "successful" : 2,
     "skipped" : 0,
 # fluent-bit-testing
     "failed" : 0
   },
   "hits" : {
     "total" : {
       "value" : 1,
       "relation" : "eq"
     },
 # fluent-bit-testing
     "max_score" : 1.0,
     "hits" : [
       {
         "_index" : "fluent-bit",
         "_type" : "_doc",
         "_id" : "1JOf0nUBGko4AhiEcxpg",
         "_score" : 1.0,
         "_source" : {
           "@timestamp" : "2020-11-16T12:30:16.275Z",
           "log" : "(See full trace by running task with --trace)\n",
           "stream" : "stderr",
           "time" : "2020-11-16T12:30:16.275664751Z"
         }
       }
     ]
   }
 } 
