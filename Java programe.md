
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
### 2) **Duplicate and NonDuplicate and Unique printing**
**A. Duplicate printing**
```java
public class App {
    public static void main(String[] args) {
        List<Integer> nums = Arrays.asList(1, 1, 2, 3, 4, 0, 1, 5, 4, 0, 1);
        List<Integer> ans = new ArrayList<>();
        for (int i = 0; i < nums.size(); i++) {
            int count = 0;

            for (int j = 0; j < nums.size(); j++) {
                if (nums.get(i).equals(nums.get(j))) {
                    count++;
                }
            }
            if (count > 1 && !ans.contains(nums.get(i))) {
                ans.add(nums.get(i));
            }
        }
        System.out.println(ans);
    }
}
//output
//[1, 4, 0]
```
**B. NonDuplicate printing**
```java

public class App {
    public static void main(String[] args) {
        List<Integer> nums = Arrays.asList(1, 1, 2, 3, 4, 0, 1, 5, 4, 0, 1);
        List<Integer> ans = new ArrayList<>();
        for (int i = 0; i < nums.size(); i++) {
            int count = 0;

            for (int j = 0; j < nums.size(); j++) {
                if (nums.get(i).equals(nums.get(j))) {
                    count++;
                }
            }
            if (count == 1 && !ans.contains(nums.get(i))) {
                ans.add(nums.get(i));
            }
        }
        System.out.println(ans);
    }
}
//output
//[2, 3, 5]
```
**C. Unique printing**
```java
//I-Java 8

public class App {
    public static void main(String[] args) {
        List<Integer> nums = Arrays.asList(1, 1, 2, 3, 4, 0, 1, 5, 4, 0, 1);
        nums.stream().distinct().forEach(System.out::println);
    }
}
//output
//[1, 2, 3, 4, 0, 5]

//II-brute force
public class App {
    public static void main(String[] args) {
        List<Integer> nums = Arrays.asList(1, 1, 2, 3, 4, 0, 1, 5, 4, 0, 1);
        for (int i = 0; i < nums.size(); i++) {
            if (!ans.contains(nums.get(i))) {
                ans.add(nums.get(i));
            }
        }
        System.out.println(ans);
    }
}
//output
//[1, 2, 3, 4, 0, 5]
```
