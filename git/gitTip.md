## <a name="gitignore"></a> .gitignore 적용 안될 때  

.gitignore 파일 추가 후, ignore 적용이 안될 땐 root directory에서 git bash를 열어 다음 커맨드를 실행한다.  

``git rm -r --cached .``  
``git add .``  
``git commit -m "fixed untracked files"``  

cached과 add 뒤에 한칸 공백 후 . 도 꼭 입력할 것!  
