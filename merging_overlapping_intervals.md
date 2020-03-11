Merging Overlapping Intervals

Given a set of ranges determine the overlapping ranges and merge them. Print the final size and ranges.

Input's first line indicates the number of input ranges followed by the ranges.

Input:
4
0 1
2 4
6 7
3 5

Output:
3
0 1
2 5
6 7

Input:
4
2 6
1 3
8 10
13 18

Output:
3
1 6
8 10
13 18

Java based solution (not space optimized). Run Time - O(n log(n)) because of sorting followed by linear progression.

```java
import java.util.Iterator;
import java.util.Scanner;
import java.util.Set;
import java.util.TreeSet;


public class MergeOverlappingIntervals {

    private static class Range implements Comparable<Range> {
        private int start;
        private int end;

        public Range(int start, int end) {
            this.start = start;
            this.end = end;
        }

        public boolean isInRange(Range range) {
            return this.start <= range.start && this.end >= range.start ||
                    range.start <= this.start && range.end >= this.start;
        }

        public Range merge(Range range) {
            int x = Math.min(this.start, range.start);
            int y = Math.max(this.end, range.end);
            return new Range(x, y);
        }

        public String toString() {
            return this.start + " " + this.end;
        }

        @Override
        public int compareTo(Range that) {
            return this.start - that.start;
        }
    }

    static void mergeOverlappingIntervals(Set<Range> ranges) {
        if(ranges.isEmpty()) return;

        Iterator<Range> it = ranges.iterator();
        Range previous = it.next();

        Set<Range> adjusted = new TreeSet<>();
        while(it.hasNext()){
            Range current = it.next();
            if(previous.isInRange(current)){
                previous = previous.merge(current);
            } else{
                adjusted.add(previous);
                previous = current;
            }
        }
        adjusted.add(previous);

        System.out.println(adjusted.size());
        adjusted.stream().forEach(System.out::println);

    }

    public static void main(String[] args) {
        Set<Range> ranges = new TreeSet<>();
        Scanner scanner = new Scanner(System.in);
        int count = Integer.parseInt(scanner.nextLine());

        while (count > 0 && scanner.hasNextLine()) {
            String input = scanner.nextLine();
            String[] entry = input.split(" ");
            Range range = new Range(Integer.parseInt(entry[0]), Integer.parseInt(entry[1]));
            ranges.add(range);
            count--;
        }
        
        mergeOverlappingIntervals(ranges);
    }
}
```