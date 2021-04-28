# 
# Make_vocab-Kor-
- 각 언어마다 학습시키기 위한 데이터 전처리 과정이 다르다.
- 따라서, 한국어에 맞는 vocab을 사전에 만들어 두고 여러 프로젝트에 사용할 수 있도록 준비해야 한다.

# 개요
## - character level
Character 단위로 vocab을 만드는 방법.

한국어 기준으로 자음[‘ㄱ’, ‘ㄴ’, …, ‘ㅎ’], 모음[‘ㅏ’, ‘ㅑ’, …, ‘ㅣ’] 단위로 vocab을 나누거나,
글자[‘가’, ‘갸’, …, ‘힣’]와 같이 가능한 모든 글자 단위로 vocab을 나누는 것.

이 경우는 가능한 모든 글자를 전부 vocab으로 표현이 가능하지만 
각 단어의 고유한 의미를 표현하고 있는것은 아니기 때문에 좋은 성능을 내지 못하는 경우가 많다.

## - space level
띄어쓰기 단위로 vocab를 만드는 방법. 

띄어쓰기로 할 경우 한국어의 경우는 조사/어미 등으로 인해서 중복단어 문제가 발생하는데 
가령 ‘책’이라는 단어는 문장 내에서는 [‘책이’, ‘책을’, ‘책에’, ‘책은’, …]같이 나타난다.

이 모든 단어를 전부 vocab으로 만들경우 vocab이 매우 커지게 되고 빈도수가 낮은 단어들은 잘 학습이 되지 않는다.

대안으로 vocab을 줄이기 위해서 일정 빈도 이상이 단어만 vocab으로 만들 경우에 
vocab에 없는 단어는 unknown으로 처리 해야 하는 문제가 발생하기도 한다.

## - subword level
많은 단어를 처리하면서도 unknown이 발생할 확률을 줄이는 방법.
단어의 빈도수를 계산해서 subword 단위로 쪼개는 방법입니다. 

이 기능을 쉽게 처리할 수 있도록 구글에서 sentencepiece라는 툴을 제공하고 있다.

# 환경
- python = 3.x
- pytorch = 1.18

# 준비물
## 한국어 위키 말뭉치
(https://ko.wikipedia.org/wiki/%EC%9C%84%ED%82%A4%EB%B0%B1%EA%B3%BC:%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4_%EB%8B%A4%EC%9A%B4%EB%A1%9C%EB%93%9C)
- 위 링크에서 pages-articles.xml.bz2 파일을 다운로드
- wikiextractor(https://github.com/attardi/wikiextractor)를 이용해 처리된 결과 파일을 텍스트로 변환.
- 위 과정을 웹 크롤러로 자동화 해놓은 프로그램이 있음.

git clone https://github.com/paul-hyun/web-crawler.git

cd web-crawler

pip install tqdm

pip install pandas

pip install bs4

pip install wget

pip install pymongo

python kowiki.py

## google SentencePiece 설치
- pip install sentencepiece
(사용법 - https://github.com/google/sentencepiece)

# 목표
- 한국어 학습을 위한 말뭉치(vocab)을 만들어 보고 이를 학습에 이용해본다.

