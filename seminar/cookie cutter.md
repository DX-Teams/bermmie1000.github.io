---
sort: 5
---
# ![cookiecutter](https://raw.githubusercontent.com/cookiecutter/cookiecutter/3ac078356adf5a1a72042dfe72ebfa4a9cd5ef38/logo/cookiecutter_medium.png)

```note
# Cookiecutter - Data Science
_데이터 과학 작업을 수행하고 공유하기 위해 논리적이고 합리적으로 표준화되었지만 유연한 __프로젝트 구조__ 입니다._
```


## 이 프로젝트 구조를 사용하는 이유는 무엇입니까?
데이터 분석을 수행할 때 우리는 종종 결과 보고서나 인사이트 또는 시각화에만 치중합니다.그래서 메인 이벤트인 최종 결과물을 멋지게 만드는 데에 너무 집중한 나머지, 그 결과물을 생성하는 코드의 품질을 무시하기 쉽상입니다.하지만 코드의 품질은 매우 중요합니다! 왜냐하면 그 최종 결과물은 모두 개발을 통해 생성되기 때문입니다.여기서 우리는 들여쓰기 같은 코딩 컨벤션을 얘기하고자 하는 것이 아닙니다.결국 데이터 분석 코드의 품질은 정확성과 재현성에 달려있습니다.

좋은 분석은 종종 매우 산발적이고 우연한 탐험의 결과입니다.잘 풀리지 않을 수 있는 주먹구구식 실험과 신속하게 테스트하는 접근 방식은 모두 좋은 것을 얻기 위한 프로세스의 일부이며, 데이터 탐색을 단순하고 선형적인 진행으로 바꾸는 마법은 없습니다.

즉, 일단 시작되면 코드 또는 프로젝트 레이아웃의 구조를 변경하기 어렵기 때문에 깨끗하고 논리적인 구조로 시작하여 고수하는 것이 가장 좋습니다. 우리는 이와 같이 상당히 표준화된 설정을 사용하는 것이 모든 면에서 상당히 큰 이득이라고 생각합니다. 그 이유는 다음과 같습니다.

### 다른 사람들이 감사할 것입니다. 🙏
- `cookiecutter`를 사용해 만든 표준 프로젝트 구조 덕분에
    - 초보자가 광범위한 문서를 파헤치지 않고도 분석을 이해하기 시작할 수 있습니다.
    - 또한 매우 구체적인 항목을 찾기 위해 코드를 100 % 읽을 필요는 없습니다.

깨끗하게 정리된 코드는 맥락을 제공한다는 점에서 자체 문서화되는 경향이 있습니다. 덕분에 조직에서 많은 투자를 하지 않으면서 코드를 내재화할 수 있습니다. 사람들은 다음 항목들을 수행할 수 있기 때문에 이에 대해 감사할 것입니다.
- 이 분석에 대해 당신과 더 쉽게 협업 할 수 있기 때문에
- 프로세스와 도메인에 대해 분석을 통해 배울 수 있기 때문에
- 분석 결과에 대한 결론에 자신감을 가질 수 있기 때문에

이에 대한 좋은 예는 `Django` 또는 `Ruby on Rails`와 같은 주요 웹 개발 프레임 워크에서 찾을 수 있습니다.
- 새로운 `Rails` 프로젝트를 만들기 위해 아무도 프로젝트 구조에 대해 고민하지 않습니다. 
- 그저 다른 사람들과 마찬가지로 표준 프로젝트 골격을 얻기 위해 새로운 레일을 실행할 뿐입니다. 
- 기본 프로젝트 구조는 대부분의 프로젝트에서 논리적이고 합리적인 표준이기 때문에 특정 프로젝트를 본 적이 없는 사람이 다양하고 움직이는 부분을 찾을 수 있는 위치를 파악하는 것이 훨씬 쉽습니다.

또 다른 좋은 예는 유닉스 계열 시스템을 위한 파일 시스템 계층 표준입니다. 
- `/etc` 디렉터리는 `/tmp` 폴더와 마찬가지로 매우 특정한 목적을 가지고 있으며 대부분의 사람들은 해당 사회적 약속을 준수하는 데 동의합니다. 
- 즉, `Red Hat` 사용자와 `Ubuntu` 사용자는 서로의 시스템 또는 기타 표준 호환 시스템을 사용할 때에도 특정 유형의 파일을 찾을 위치를 대략적으로 알고 있습니다.

이상적으로는 동료가 데이터 과학 프로젝트를 시작할 때 그렇게 해야 합니다.

### 스스로에게 감사할 것입니다. 🐸
몇 달 전 또는 몇 년 전에 수행한 분석을 재현하려고 시도한 적이 있나요?
내가 작성한 코드지만 다시 찾아보면 어느 파일을 사용하여 작업을 수행해야하는지 헷갈립니다.
여기에 우리가 공포감을 가지고 물어볼 수있는 몇 가지 질문이 있습니다.

- 시작하기 전에 X 열을 데이터에 조인해야합니까?
    아니면 notebook 중 하나에서 가져온 것입니까?
- 시각화 코드를 실행하기 전에 먼저 어떤 파일을 실행해야합니까?
    "process data"입니까, "clean data"입니까?
- 지도 그래프의 shapefile은 어디서 다운로드 했습니까?
- 등등, 무한대...

이런 질문들은 고통스럽고 체계적이지 않은 프로젝트의 증상입니다. 좋은 프로젝트 구조는 예를 들어 관심사 분리, [DAG](https://ko.wikipedia.org/wiki/%EC%9C%A0%ED%96%A5_%EB%B9%84%EC%88%9C%ED%99%98_%EA%B7%B8%EB%9E%98%ED%94%84)로 분석 추상화, 버전 제어와 같은 엔지니어링 모범 사례와 같이 이전 작업으로 쉽게 돌아갈 수있는 방법을 권장합니다.

### 기본 구조에 얽매이지 않아도 됩니다.
> "어리석은 일관성은 작은 마음의 홉 고블린입니다."— Ralph Waldo Emerson(1803)
>- 미국 시인
>- __홉 고블린__ 이란 영국 민담에서 나오는 요정의 일종으로 어리석은 고집(일관성, 걱정)은 소인배(에게 들러붙는) 말썽쟁이를 뜻함

- 기본 폴더 이름이 맘에 들지 않나요?
- 지금 진행하고 있는 프로젝트가 약간 비표준적이고 기본 구조에 맞지 않나요?
- 기본값 중 하나가 아닌 다른 패키지를 사용하고 싶나요?

```note
# 수정 하세요!
__프로젝트 내의 일관성이 더 중요합니다.__
하나의 모듈 또는 기능 내에서 일관성이 가장 중요합니다.... 그러나 일관성이 없어야 할 때를 아십시오. 때로는 스타일 가이드 권장 사항이 적용되지 않는 경우도 있습니다. 의심스러우면 최선의 판단을 내리십시오. 다른 예를 보고 가장 잘 보이는 것을 결정하십시오. 그리고 주저하지 말고 물어보세요!
```
---

## 시작하기 🎯
### 요구사항
- Python 2.7 or 3.5
- [cookiecutter Python package](https://cookiecutter.readthedocs.io/en/latest/installation.html) >= 1.4.0
```console
$ pip install cookiecutter
```


### 새 프로젝트 시작
새 프로젝트를 시작하는 것은 매우 쉽습니다.
먼저 디렉토리를 만들 필요가 없습니다. cookiecutter가 대신 만들어드립니다.

```console
$ cookiecutter https://github.com/drivendata/cookiecutter-data-science
```
## Directory structure
``` console
root
├── LICENSE
├── Makefile           <- Makefile with commands like `make data` or `make train`
├── README.md          <- The top-level README for developers using this project.
├── data
│   ├── external       <- Data from third party sources.
│   ├── interim        <- Intermediate data that has been transformed.
│   ├── processed      <- The final, canonical data sets for modeling.
│   └── raw            <- The original, immutable data dump.
│
├── docs               <- A default Sphinx project; see sphinx-doc.org for details
│
├── models             <- Trained and serialized models, model predictions, or model summaries
│
├── notebooks          <- Jupyter notebooks. Naming convention is a number (for ordering),
│                         the creator's initials, and a short `-` delimited description, e.g.
│                         `1.0-jqp-initial-data-exploration`.
│
├── references         <- Data dictionaries, manuals, and all other explanatory materials.
│
├── reports            <- Generated analysis as HTML, PDF, LaTeX, etc.
│   └── figures        <- Generated graphics and figures to be used in reporting
│
├── requirements.txt   <- The requirements file for reproducing the analysis environment, e.g.
│                         generated with `pip freeze > requirements.txt`
│
├── setup.py           <- Make this project pip installable with `pip install -e`
├── src                <- Source code for use in this project.
│   ├── __init__.py    <- Makes src a Python module
│   │
│   ├── data           <- Scripts to download or generate data
│   │   └── make_dataset.py
│   │
│   ├── features       <- Scripts to turn raw data into features for modeling
│   │   └── build_features.py
│   │
│   ├── models         <- Scripts to train models and then use trained models to make
│   │   │                 predictions
│   │   ├── predict_model.py
│   │   └── train_model.py
│   │
│   └── visualization  <- Scripts to create exploratory and results oriented visualizations
│       └── visualize.py
│
└── tox.ini            <- tox file with settings for running tox; see tox.testrun.org
```

### 데이터는 불변입니다.
- 원시 데이터를 편집하지 마십시오. 
- 특히 수동으로 편집하지 마십시오. 
- 특히 Excel에서는 편집하지 마십시오. 
- 원시 데이터를 덮어쓰지 마십시오. 
- 여러 버전의 원시 데이터를 저장하지 마십시오. 
- 데이터 (및 해당 형식)를 변경 불가능한 것으로 취급하십시오. 
- 작성하는 코드는 파이프 라인을 통해 원시 데이터를 최종 분석으로 이동해야 합니다. 
- 새 그림을 만들고 싶을 때마다 모든 단계를 실행할 필요는 없지만 (분석은 DAG 참조) 누구나 `src`의 코드와 `data/raw`의 데이터만으로 최종 제품을 재현할 수 있어야 합니다.

또한 데이터가 변경 불가능한 경우 코드와 동일한 방식으로 소스 제어가 필요하지 않습니다. 따라서 기본적으로 데이터 폴더는. `.gitignore` 파일에 포함됩니다. 거의 변경되지 않는 소량의 데이터가 있는 경우 해당 데이터를 저장소에 포함할 수 있습니다. Github는 현재 파일이 50MB를 초과하면 경고하고 100MB를 초과하는 파일은 거부합니다. 대용량 데이터를 저장 / 동기화하기 위한 다른 옵션으로는 동기화 도구 (예 : `s3 cmd`)가 있는 AWS S3, Git 대용량 파일 스토리지, Git Annex 및 dat가 있습니다. 현재 기본적으로 S3 버킷을 요청하고 AWS CLI를 사용하여 `data` 폴더의 데이터를 서버와 동기화합니다.

### EDA와 커뮤니케이션을 위한 `notebook`
Jupyter notebook, Beaker notebook, Zeppelin 및 기타 유능한 프로그래밍 도구와 같은 notebook 패키지는 EDA에 매우 효과적입니다. 그러나 이러한 도구는 분석 재현에 덜 효과적 일 수 있습니다.
- 작업에서 notebook을 사용할 때 종종 `notebooks` 폴더를 세분화합니다.
    - 예를 들어 `notebooks/exploratory`에는 초기 탐색이 포함되어있는 반면 `notebooks/reports`는 `reports` 디렉터리에 html로 내보낼 수 있는 보다 세련된 작업입니다.

notebook은 소스 제어를 위한 까다로운 개체이기 때문에 (예 : `json`의 diff는 사람이 읽을 수없는 경우가 많고 병합이 거의 불가능함) Jupyter notebook에서 다른 사람과 직접 협업하지 않는 것이 좋습니다. notebook을 효과적으로 사용하기 위해 권장하는 두 단계가 있습니다.

1. 소유자와 분석이 수행된 순서를 보여주는 명명 규칙을 따릅니다. `<step>-<ghuser>-<description>.ipynb` 형식을 사용합니다. (예 : `0.3-bull-visualize-distributions.ipynb`).

2. 좋은 부분을 리팩터링 하십시오. 여러 notebook에서 동일한 작업을 수행하는 코드를 작성하지 마십시오. 데이터 전처리 작업인 경우 `src/data/make_dataset.py`의 파이프 라인에 넣고 `data/interim`에서 데이터를 로드합니다. 유용한 유틸리티 코드라면 `src`로 리팩터링 하십시오.

이제 기본적으로 프로젝트를 Python 패키지로 변환합니다 (`setup.py` 파일 참조). 코드를 가져와서 다음과 같은 셀이 있는 notebook에서 사용할 수 있습니다.

``` python
# OPTIONAL: Load the "autoreload" extension so that code can change
%load_ext autoreload

# OPTIONAL: always reload modules so that as you change code in src, it gets loaded
%autoreload 2

from src.data import make_dataset
```

### 분석은 DAG입니다
종종 분석에는 데이터를 전 처리하거나 모델을 훈련시키는 장기 실행 단계가 있습니다. 이러한 단계가 이미 실행된 경우 (`data/interim` 디렉터리와 같은 위치에 출력을 저장한 경우) 매번 다시 실행하기를 기다리지 않아도 됩니다. 우리는 `make`을 통해 서로 의존하는 단계, 특히 장기 실행 단계를 관리하는 것을 선호합니다. Make는 Unix 기반 플랫폼의 일반적인 도구입니다 (Windows에서 사용 가능). `make` 문서, Makefile 규약 및 이식성 가이드를 따르면 Makefile이 시스템 전반에서 효과적으로 작동하는지 확인할 수 있습니다. 다음은 시작하기 위한 몇 가지 예입니다. Mike Bostock을 비롯한 많은 데이터 사용자가 `make`를 선택한 도구로 사용합니다.

DSL 대신 Python으로 작성된 DAG를 관리하기 위한 다른 도구가 있습니다 (예 : Paver, Luigi, Airflow, Snakemake, Ruffus 또는 Joblib). 분석에 더 적합한 경우 자유롭게 사용하십시오.

### 환경에서 위로 구축
분석을 재현하는 첫 번째 단계는 항상 실행된 계산 환경을 재현하는 것입니다. 모든 것이 잘 작동하도록 하려면 동일한 도구, 동일한 라이브러리 및 동일한 버전이 필요합니다.

이에 대한 효과적인 접근 방법 중 하나는 virtualenv를 사용하는 것입니다 (virtualenv를 관리하려면 virtualenvwrapper를 권장합니다). 모든 요구 사항을 리포지토리 (Requirements.txt 파일 포함)에 나열하면 분석을 다시 만드는 데 필요한 패키지를 쉽게 추적할 수 있습니다. 다음은 좋은 워크 플로입니다.

1. 새 프로젝트를 만들 때 `mkvirtualenv` 실행
2. `pip install` 분석에 필요한 패키지
3. `pip freeze > requirements.txt`를 실행하여 분석을 다시 생성하는 데 사용된 정확한 패키지 버전을 고정합니다.
4. 다른 패키지를 설치해야 하는 경우 `pip freeze > requirements.txt`를 다시 실행하고 변경 사항을 버전 제어에 커밋합니다.

환경을 다시 만들기 위한 더 복잡한 요구 사항이 있는 경우 Docker 또는 Vagrant와 같은 가상 머신 기반 접근 방식을 고려하십시오. 이 두 도구는 모두 텍스트 기반 형식 (각각 Dockerfile 및 Vagrantfile)을 사용하여 소스 제어에 쉽게 추가하여 필요한 요구 사항으로 가상 머신을 생성하는 방법을 설명할 수 있습니다.

### 버전 제어에서 비밀 및 구성 유지
Github에서 AWS 비밀 키 또는 Postgres 사용자 이름과 암호를 유출하고 싶지는 않습니다. 충분히 말씀하셨습니다. 이 점에 대한 12 가지 요소 앱 원칙을 참조하세요. 이를 수행하는 한 가지 방법은 다음과 같습니다.

_비밀 및 구성 변수를 특수 파일에 저장_
프로젝트 루트 폴더에 `.env` 파일을 만듭니다. `.gitignore` 덕분에 이 파일은 버전 관리 저장소에 커밋되지 않아야 합니다. 예를 들면 다음과 같습니다.
```
# example .env file
DATABASE_URL=postgres://username:password@localhost:5432/dbname
AWS_ACCESS_KEY=myaccesskey
AWS_SECRET_ACCESS_KEY=mysecretkey
OTHER_VARIABLE=something
```

_패키지를 사용하여 이러한 변수를 자동으로 로드하십시오._
`src/data/make_dataset.py`에서 `stub`스크립트를 보면 python-dotenv라는 패키지를 사용하여이 파일의 모든 항목을 환경 변수로 로드하여 `os.environ.get`으로 액세스 할 수 있습니다. 다음은 `python-dotenv` 문서에서 수정된 예제 스 니펫입니다.
```python
# src/data/dotenv_example.py
import os
from dotenv import load_dotenv, find_dotenv

# find .env automagically by walking up directories until it's found
dotenv_path = find_dotenv()

# load up the entries as environment variables
load_dotenv(dotenv_path)

database_url = os.environ.get("DATABASE_URL")
other_variable = os.environ.get("OTHER_VARIABLE")
```

_AWS CLI 구성_
Amazon S3를 사용하여 데이터를 저장할 때 AWS 액세스를 관리하는 간단한 방법은 액세스 키를 환경 변수에 설정하는 것입니다. 그러나 단일 시스템에서 여러 키 세트를 관리하는 경우 (예 : 여러 프로젝트에서 작업하는 경우) 일반적으로 `~/.aws/credentials`에 있는 자격 증명 파일을 사용하는 것이 가장 좋습니다. 일반적인 파일은 다음과 같습니다.
```
[default]
aws_access_key_id=myaccesskey
aws_secret_access_key=mysecretkey

[another_project]
aws_access_key_id=myprojectaccesskey
aws_secret_access_key=myprojectsecretkey
```
프로젝트를 초기화 할 때 프로필 이름을 추가 할 수 있습니다. 적용 가능한 환경 변수가 설정되어 있지 않다고 가정하면 프로필 자격 증명이 기본값으로 사용됩니다.

### 기본 폴더 구조 변경 시 신중해야 합니다.
이 구조를 다양한 종류의 프로젝트에 광범위하게 적용하려면 프로젝트의 폴더를 자유롭게 변경하고 모든 프로젝트의 기본 구조를 보수적으로 변경하는 것이 가장 좋은 방법이라고 생각합니다.

폴더 추가, 빼기, 이름 바꾸기 또는 이동을 제안하는 문제를 위해 특별히 폴더 __레이아웃 레이블__ 을 만들었습니다. 보다 일반적으로 구현하기 전에 신중한 논의와 광범위한 지원이 필요한 문제에 대한 __필요 논의 레이블__ 도 만들었습니다.


[원본링크](https://drivendata.github.io/cookiecutter-data-science/#example)