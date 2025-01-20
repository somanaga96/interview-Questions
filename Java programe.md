
### 1) **Duplicate and NonDuplicate printing**
```java
public class Main {
    @Test
    public void test() {
        String name = "heello";
        name.chars().distinct().forEach(x -> System.out.print((char) x+" "));
        //output : helo
        System.out.println();
        Map<String, Integer> count = new HashMap<>();
        for (String c : name.split("")) {
            if (count.containsKey(c)) {
                count.put(c, count.get(c) + 1);
            } else {
                count.put(c, 1);
            }
        }

       count.entrySet().stream().filter(x -> x.getValue() > 1).forEach(x->System.out.print(x.getKey()+" "));
        //output : el
    }
}
```
