## sed를 활용한 문제 출제 및 공부
```
파일 내부 test.txt
ttttt
rrrrr
rwoori
hihi
```
**1. 이름끝 부분을 fisa으로 변경하세요**

답: sed 's/X/woori/' test.txt

**2. 두 번 째 라인을 삭제해주세요**
   
답: sed '2d' test.txt

**3. hi부분을 검색해주세요**
   
답: sed -n '/hi/p' test.txt

**4. test1.txt 파일의 4번째 줄에 "fisa" 텍스트를 삽입하고 test2.txt 파일에 다시 기록하세요**

sed '4 i\fisa' test1.txt > test2.txt
```
'test1.txt'
one
two
three
four
five
```

**5. test.txt 파일의 3번째부터 5번째까지의 행 범위를 삭제하세요**

sed '3,5d' test.txt
```
'test.txt'
one
two
three
four
five
```

**6. 이름 정보가 있는 name.txt에서 이름중에 성이 김씨인 사람을 출력하시오.**

답: sed -n '/kim/p' name.txt

**7. color.txt 문서에 있는 black단어를 white로 변경하시오.**

답: sed '/black/s/black/white/' color.txt

**8. 이메일 정보가 있는 email.txt 파일에서 이메일을 ABCDEF@naver.com에서 앞에 3글자만 남기고 뒤는 XXXX로 대체하시오. (ex. kimyh9797@naver.com -> kimXXXX@naver.com)**

답: sed 's/(.{3})\w*[^@]/\1xxxx/' email.txt

**9.전화번호를 전부 1로 대체하세요**

답: sed 's/[0-9]/1/g' test.txt
```
파일 내부 test.txt
010-1234-5678
```

**10. test.txt 파일에 fisa로 끝나는 행을 찾아서 뒤에 "hello"를 추가하세요**

 sed '/fisa$/a\hello' test.txt
```
'test.txt'
cloud
engineering
fisa
team
```
