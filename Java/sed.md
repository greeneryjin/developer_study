
1. 이름끝 부분을 fisa으로 변경하세요  sed 's/X/woori/' test.txt
2. 3번 째 라인을 삭제해주세요 sed '3d' test.txt
3. hi부분을 검색해주세요 sed -n '/hi/p' test.txt
4. test1.txt 파일의 4번째 줄에 "fisa" 텍스트를 삽입하고 test2.txt 파일에 다시 기록하세요
sed '4 i\fisa' test1.txt > test2.txt
5. test.txt 파일의 3번째부터 5번째까지의 행 범위를 삭제하세요
sed '3,5d' test.txt
6. name.txt 이름중에 성이 김씨인 사람 출력
	sed -n '/kim/p' name.txt
7. 문서에서 오타를 발견 project.txt에서 Checklist를 CheckList로 변경
	sed '/Checklist/s/Checklist/CheckList/' samplefile.txt
8. test.txt 파일에 fisa로 끝나는 행을 찾아서 뒤에 "hello"를 추가하세요
sed '/fisa$/a\hello' test.txt
9. 전화번호를 전부 1로 대체하세요 sed 's/[0-9]/1/g' test.txt
10. 이메일을 ABCDEF@naver.com에서 앞에 3글자만 남기고 뒤는 XXXX로 대체
	(ex. kimyh9797@naver.com -> kimXXXX@naver.com)
sed 's/\(.\{3\}\)\w*[^@]/\1xxxx/' email.txt
