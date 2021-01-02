# English Wikipedia Extractor
영어 위키피디아 plain text를 얻기 위한 WikiExtractor
- 💾Github: https://github.com/nawnoes/WikiExtractor
### 개선내용
- [apertium/WikiExtractor](https://wiki.apertium.org/wiki/Wikipedia_Extractor)의 경우 문서의 제목 아래에 <pages\>와 같은 태그들이 보여 영어 위키피디아의 plain text를 얻는데 불편함이 있었다. 

  ```python
  def clean_html(raw_html):
    cleanr = re.compile('<.*?>')
    cleantext = re.sub(cleanr, '', raw_html)
    return cleantext
  ```
  을 사용하여 html 태그들을 삭제
 - 문서 본문이 아무것도 없는 경우, 해당 문서 건너 뛰기
```python
    def WikiDocumentSentences(out, id, title, tags, text):
    header = '\n{0}{1}'.format(title, "|||".join(tags))
    text = clean(text)

    if text.isspace() or len(compact(text,structure=False))==0:
        return
    out.reserve(len(header) + len(text))
    print(header, file=out)
    for line in compact(text, structure=False):
        print(line, file=out)
```
    
### 사용법
##### 1. Wiki Dump 다운로드
  ![](https://images.velog.io/images/nawnoes/post/5a4f71b1-e3e5-463e-8c16-5bc59ceca50f/image.png)
[enwikisource dump](https://dumps.wikimedia.org/enwikisource/20210101/)에서 덤프 파일 다운로드
![](https://images.velog.io/images/nawnoes/post/34f19fb6-13a3-4bb6-99d7-9b61f3973e45/image.png)
##### 2. 덤프 파일 저장 후 명령어 실행
- https://github.com/nawnoes/WikiExtractor 에서 `WikiExtractor.py` 다운로드
- `WikiExtractor.py` 소스 경로에서 아래 명령어 실행

```
python3 WikiExtractor.py --infn [다운받은덤프파일명].xml.bz2
```
  > 다운로드 받은 덤프파일의 경로 지정에 주의한다. 
  
##### 3. 생성확인
아래와 같은 양식으로 `WikiExtractor.py`와 같은 경로에 2.03GB의 `wiki.txt` 파일 생성
```
제목
본문텍스트

제목
본문텍스트
...
```
![](https://images.velog.io/images/nawnoes/post/091d3e3f-c7a4-4e1c-b7e6-ae1d01eaf6d7/image.png)
    
## Reference
[/Wikipedia Extractor](https://wiki.apertium.org/wiki/Wikipedia_Extractor)