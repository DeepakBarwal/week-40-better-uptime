![steps](./steps.png)

```bash
docker run -p 6379:6379 redis

# Optional
docker exec -it <container_id> sh
redis-cli
XADD EverPing:website * id 1 url google.com
XADD EverPing:website * id 2 url api.startup.com
XREAD COUNT 1 BLOCK 2000 STREAMS EverPing:website $
XREAD COUNT 10 STREAMS EverPing:website 0

# In the same consumer group, workers will read different items always
XGROUP CREATE EverPing:website india $
XGROUP CREATE EverPing:website usa $
XGROUP CREATE EverPing:website africa $
XREADGROUP GROUP india COUNT 2 STREAMS EverPing:website >
```
