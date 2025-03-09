# Data Structure Design Patterns

### Dynamically updating the priorityQueue when an object's value changes
- If we change the attr of an object in a PQ and if that attr contributes to the comparator, the PQ will not be updated dynamically
- In order to update it, we first need to remove the original object, update the attr and then put it back in
- Remove and contains in PQ take O(N) time, hence this will slow down the app while adding new items, tho lookup will be fast
- We should rather just keep adding to the PQ and set one of the attrs in the original object(that is not part of the comparator) to null 
- At the time of lookup, poll out all the elements where the object attr is null and then return the first element where that attr was not null

```java
// Option 1: using remove and add in PQ makes the code readable, but slows down the update operation, the read operation is O(1), but the update is now O(N)

public void changeRating(String food, int newRating) {
        FoodItem item = foodItems.get(food);
        if(item != null){
            Queue<FoodItem> queue = cuisines.get(item.cuisine);
            if(queue != null){
                queue.remove(item);
                item.rating = newRating;
                queue.add(item);
            }
        }
    }
    
    public String highestRated(String cuisine) {
        return cuisines.get(cuisine).peek().food;
    }

// Option 2: make both update and read O(logN) by modifying an attr of the object that is not part of comparator

public void changeRating(String food, int newRating) {
        FoodItem item = foodItems.get(food);
        FoodItem newItem = new FoodItem(food, item.cuisine, newRating);
        foodItems.put(food, newItem);
        cuisines.get(item.cuisine).add(newItem);
        item.cuisine = "";
        
    }
    
    public String highestRated(String cuisine) {
        Queue<FoodItem> q =  cuisines.get(cuisine);
        while(!q.isEmpty() && "".equals(q.peek().cuisine)){
            q.poll();
        }
        return q.peek().food;
    }

```

### TreeMap
- To retrieve a key that is greatest but less than or equal to the given key, use treemap.floorKey(input_key)

