## Problem setting

给一个expiring map， 你可以一直往里面put东西，这些东西都有个过期值，一旦过期就get不到了。
//put(null, null, 2000);

// 10:00:00 - put(10, 25, 5000)
/*
* (10, (25, 10:00:05))
// 10:00:04 - get(10) -> 25
// 10:00:05 - get(10) -> null
// 10:00:06 - get(10) -> null

## Solution

```java
class ExpiringMap {
    HashMap<Integer, Item> map = new HashMap<>();
    
    class Item {
        private int val;
        private long expiringTime;
        public Item(int val, long duration) {
            this.val = val;
            this.expiringTime = duration + System.currentTimeMillis();
        }
    }
    
    public void put(int key, int val, long duration) {
        map.put(key, new Item(val, duration));
    }
    
    public Integer get(int key) {
        if (!map.containsKey(key))
            return null;
        else {
            if (map.get(key).expiringTime <= System.currentTimeMillis()) {
                map.remove(key);
                return null;
            }
            else
                return map.get(key).val;
        }
    }
}
```