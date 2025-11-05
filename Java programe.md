
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
### 3) **To find the second MAX**
  **A. Java8**
```java
  Optional<Integer> first = nums.stream().sorted(Comparator.reverseOrder()).skip(1).findFirst();
```
  **B. Brute force**
```java
public class App {
    public static void main(String[] args) {
        List<Integer> nums = Arrays.asList(1, 4, 6, 8, 19, 2);
        int max = Integer.MIN_VALUE;
        int secondMax = Integer.MIN_VALUE;
        for (int n : nums) {
            if (n > max) {
                secondMax = max;
                max = n;
            } else if (n > secondMax && n < max) {
                secondMax = n;
            }
        }
    }
}
```
### 4) **Ascending order based on digit**
  **A. Java8**
```java
  import java.util.*;

public class Main {
    public static void main(String[] args) {
        List<Integer> nums = Arrays.asList(123, 10, 3, 123);

        // Sort ascending by number of digits
        nums.sort(Comparator.comparingInt(n -> String.valueOf(n).length()));

        System.out.println(nums);
    }
}

```
  **B. Brute force**
```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        List<Integer> nums = new ArrayList<>(Arrays.asList(123, 10, 3, 123));

        for (int i = 0; i < nums.size(); i++) {
            for (int j = i + 1; j < nums.size(); j++) {
                // Compare by digit length
                int len1 = String.valueOf(nums.get(i)).length();
                int len2 = String.valueOf(nums.get(j)).length();

                // Swap if out of order (ascending by digit length)
                if (len1 > len2) {
                    int temp = nums.get(i);
                    nums.set(i, nums.get(j));
                    nums.set(j, temp);
                }
            }
        }

        System.out.println(nums);
    }
}
```
