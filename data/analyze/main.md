## 목차

1. Python 기초
2. 라이브러리 이해하기
3. Jupyter Notebook 사용법
4. 데이터 포맷 이해하기
5. Pandas 기초
6. Pandas 데이터 전처리
7. 데이터 병합과 결합
8. 실전 프로젝트: Brazilian E-commerce 분석

---

## 1. Python 기초 문법

### 1.1 데이터 타입과 변수

**출력 (print)**

```python
print('hello python!')
print(3 + 7)

```

**변수 (Variable)**

```python
str_data = "hello"        # 문자열 (string)
int_data = 1             # 정수 (integer)
float_data = 1.1         # 부동소숫점 (float)
bool_data = True         # Boolean (True/False)

```

**기본 연산자**

```python
# 산술 연산
print(15 / 7)    # 나누기
print(15 // 5)   # 몫
print(7 % 3)     # 나머지
print(15 ** 3)   # 거듭제곱

# 비교 연산
print(3 < 7)     # True
print(34 == 100) # False
print(34 != 100) # True

```

**Type Casting**

```python
float(3)      # int to float
int(3.6)      # float to int
str(1)        # int to string
int("12")     # string to int

```

### 1.2 문자열 다루기

**인덱싱과 슬라이싱**

```python
some_string = "python"
len(some_string)      # 6

some_string[0]        # 'p' (인덱싱)
some_string[-1]       # 'n'
some_string[3:5]      # 'ho' (슬라이싱)
some_string[1:5]      # 'ytho'

```

**문자열 주요 함수**

```python
func = "python is easy programming language"
func.count('p')                              # 'p' 개수 세기
func.find('p')                               # 'p' 첫 위치 찾기
func.replace("python", "golang")             # 문자열 치환

some_string = "   computer     "
some_string.strip()                          # 양쪽 공백 제거

```

### 1.3 리스트 (List)

```python
lang = ["python", "c", "java", "golang"]

lang.append("javascript")     # 끝에 추가
lang.insert(1, "c++")         # 특정 위치에 추가
lang.remove("golang")         # 값으로 삭제
del lang[2]                  # 인덱스로 삭제

numbers = [2, 1, 4, 3]
numbers.sort()               # 오름차순 정렬

```

---

## 2. 라이브러리 이해하기

* **정의**: 미리 만들어놓은 함수 집합
* **설치**: `!pip install 라이브러리명`

**사용법 예시**

```python
import pandas as pd
import statistics as s

data = [1, 2, 3, 4]
print(s.mean(data))

```

---

## 3. Jupyter Notebook

### 3.1 주요 단축키

* **a**: 위에 셀 추가 (Above)
* **b**: 아래에 셀 추가 (Below)
* **Shift + Enter**: 셀 실행 후 다음 셀로 이동
* **Ctrl + Enter**: 현재 셀 실행

---

## 4. 데이터 포맷 이해하기

### 4.1 Plain Text (파일 읽고 쓰기)

| 모드 | 설명 |
| --- | --- |
| **r** | 읽기 모드 |
| **w** | 쓰기 모드 (기존 파일 삭제) |
| **a** | 추가 모드 (기존 파일 끝에 추가) |

**With 문 사용 (권장)**

```python
with open('text_data.txt', 'r', encoding='utf-8-sig') as f:
    data = f.read()

```

### 4.2 CSV & JSON

**Pandas로 CSV 읽기**

```python
import pandas as pd
doc = pd.read_csv("data.csv", encoding='utf-8-sig')
# 쓰기
doc.to_csv("result.csv", index=False)

```

**JSON 다루기**

```python
import json
# 문자열 -> 딕셔너리
jsondata = json.loads(json_string)
# 딕셔너리 -> JSON 문자열
json_string = json.dumps(data, indent=2)

```

---

## 5. Pandas 기초

### 5.1 Series & DataFrame

* **Series**: 1차원 데이터 (Index + Value)
* **DataFrame**: 2차원 테이블 구조

### 5.2 데이터 접근 (loc vs iloc)

* **loc**: 인덱스 **이름**으로 접근
* **iloc**: 인덱스 **번호**(0, 1, 2...)로 접근

```python
df.loc[2020]
df.iloc[0]

```

---

## 6. Pandas 데이터 전처리

### 6.1 결측치(NaN) 처리

```python
doc.isnull().sum()             # 결측치 확인
doc = doc.dropna()             # 삭제
doc = doc.fillna(0)            # 0으로 채우기

```

### 6.2 그룹화 (Groupby)

```python
# 국가별 합계 계산
doc_group = doc.groupby('Country_Region').sum()

```

---

## 7. 데이터 병합과 결합

### 7.1 merge (SQL Join 방식)

```python
# Inner Join (기본값)
pd.merge(df1, df2, on='id', how='inner')

# Left Join
pd.merge(df1, df2, on='id', how='left')

```

---

## 8. Brazilian E-commerce 분석

### 8.1 분석 프로세스

1. **데이터 로드**: `pd.read_csv()`
2. **전처리**: 결측치 제거 및 `to_datetime()` 변환
3. **병합**: 주문(`orders`) + 고객(`customers`) 데이터 병합
4. **EDA**: 지역별 고객 분포, 월별 판매 트렌드 분석
5. **시각화**: `Plotly` 또는 `Matplotlib` 활용

```python
# 예시: 월별 판매 추이 추출
df['month'] = df['order_purchase_timestamp'].dt.month
monthly_sales = df.groupby('month')['price'].sum()

```
