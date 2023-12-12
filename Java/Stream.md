
#### Stream

: 자바 8부터 나온 기술로 자바 8 이전에서는 for, foreach 문을 사용해서 요소를 하나씩 꺼내서 처리했으나 로직이 복잡하거나 코드의 양이 많아지면 많은 문제가 발생하는 것을 방지하기 위해 나타난 기술입니다. 스트림을 통해 배열, 컬렉션 인스턴스에 함수 여러 개를 조합해서 결과를 필터링하고 가공된 결과를 얻을 수 있고 람다를 통해 코드를 간결하게 만들 수 있습니다.

----

스트림의 세 가지 기능

+ 생성하기
    - 배열/ 컬렉션/ 빈 스트림
    - Stream.builder()/ Stream.generate()/ Stream.iterate()
    - 기본타입/ String/ 파일 스트림
    - 병렬 스트림/ 스트림 연결

+ 가공하기
    - 필터링
    - 맵핑
    - 분류
    - 반복

+ 결과
    - 최종적인 결과물


          전체 -> 맵핑 -> 필터링 1 -> 필터링 2 -> 결과 만들기 -> 결과물


생성

(1) 배열

    String[] arr = new String[]{"ㄱ", "ㄴ", "ㄷ"};
    Stream<String> stream = Arrays.stream(arr);
    Stream<String> streamOfArrayPart = 
    Arrays.stream(arr, 1, 3); // 1~2 요소 [ㄴ, ㄷ]


(2) 컬렉션

    List<String> list = Arrays.asList("ㄱ", "ㄴ", "ㄷ");
    Stream<String> stream = list.stream();
    Stream<String> parallelStream = list.parallelStream(); // 병렬 처리 스트림


(3) 빈 스트림


    public Stream<String> streamOf(List<String> list) {
        return list == null || list.isEmpty() ? Stream.empty()  : list.stream();
    }



(4) Stream.builder()

     Stream<String> builderStream =
                Stream.<String>builder()
                        .add("자바")
                        .add("파이썬")
                        .add("html")
                        .build(); // [자바, 파이썬, html]



















    
