## Redis
Redis is an in-memory data structure store, used as a distributed, in-memory key–value database, cache and message broker, with optional durability. It can be used as a cache for user sessions and storing data that will be requested frequently to make the backend faster.

Redis can be installed on nodejs using:
```bash
pnpm install redis
```

Setting up Redis is a function of two steps:
```ts
//src/utils/redis.utils.ts
import {createClient} from 'redis';
import config from "config";

export const RedisClient = createClient({url: config.get<...>(...)});

export const ConnectRedis = async(redisClient: any | RedisClientType) =>{
	try{
		await RedisClient.connect();
	} catch(error) {
		setTimeout(ConnectRedis, 5000);	
	}
}
```
### Issues
- Remember to add redisurl to  the `*.env`,  `custom-enviromental-variables.ts` and `validate-env.util.ts`.

## TypeORM