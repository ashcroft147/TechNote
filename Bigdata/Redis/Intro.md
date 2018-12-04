## Redis로 할 수 있는것 
- 5 data types (string, list, set, sorted set, hash)
    - +2 special types (bitmap & hyperloglog)
- 160 commands
    - 명령어를 통해서 코드를 사용하는 것보다 더욱 빠른 performance를 사용할 수 있다. 
- Lua scripts add flexibility

## Redis는  ?
- Key Data-Structures.. not just Key Value/String
    - Value has 5 data types
    - also bitmaps and Hyperloglogs
- Run's in-memory
    - very fast reads and writes
- The only limitation is physical memory
    - RLEC was created to solve memory limits

## Redis Used
- redis.io의 document를 보면 쉽게 사용가능
- 주로 Cache layer에서 사용
    - 2nd-class database
    - Some even a 1st class : 대게 잠시 후에는 필요가 없어지는 데이터를 관리하는 경우(trading)
- Pub/Sub engine
- confin in single text file
- single-threaded
- Pub/Sub
- Queues
- Caching
- Real time analysis of what is hapening

## use cases
1. 홈페이지에 리스팅된 최신 item을 보여주는 경우
2. deletion and filtering
3. leaderboards and related problems
4. order by user votes and time
5. implement expires on items



## Nighthawk Cluster
 - horizontally, vertically scalable

## 참고자료
- [redislabs](https://redislabs.com/redis-enterprise-documentation/concepts-architecture/)

- [redis io](https://redis.io/)