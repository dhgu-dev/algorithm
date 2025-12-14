# Hash

## [베스트앨범](https://school.programmers.co.kr/learn/courses/30/lessons/42579)

```
import java.util.*;
import java.util.stream.*;

public class Solution {
    public class Music implements Comparable<Music> {
        public int played;
        public int id;
        public String genre;
        
        public Music(String genre, int played, int id) {
            this.genre = genre;
            this.played = played;
            this.id = id;
        }
        
        @Override
        public int compareTo(Music other) {
            if(this.played == other.played) return this.id - other.id;
            return other.played - this.played;
        }
    }
    
    public int[] solution(String[] genres, int[] plays) {
        return IntStream.range(0, genres.length)
            .mapToObj(i -> new Music(genres[i], plays[i], i))
            .collect(Collectors.groupingBy(music -> music.genre))
            .entrySet().stream()
            .sorted((a, b) -> sum(b.getValue()) - sum(a.getValue()))
            .flatMap(entry -> entry.getValue().stream().sorted().limit(2))
            .mapToInt(music -> music.id).toArray();
    }
    
    int sum(List<Music> musics) {
        int answer = 0;
        for(Music music : musics) {
            answer += music.played;
        }
        return answer;
    }
}
```