# [ARCODA 표준 트리거 개발 가이드](https://github.com/escaco95/warcraft-iii-project-template)

이 문서에서는 프로젝트의 구조, 개발 규칙 및 유지 보수 정책을 소개합니다.

프로젝트의 구조에 대한 세부적인 설명을 통해, 개발자들이 프로젝트의 전반적인 흐름을 이해하고, 각각의 스크립트가 어떻게 상호작용하는지 파악할 수 있도록 돕습니다. 또한, 유지 보수 정책에 대한 안내를 통해, 프로젝트가 지속적으로 안정적이고 효율적으로 운영될 수 있도록 지원합니다.

이 가이드는 프로젝트에 참여하는 모든 개발자들에게 필수적인 정보를 제공하며, 새로운 기능을 추가하거나 기존 코드를 수정할 때 참조할 수 있는 기준을 제시합니다. 따라서 이 문서를 숙지하고 이해하는 것은 프로젝트에 성공적으로 참여하기 위한 첫걸음입니다.

각 섹션은 다음과 같습니다:

- **[개발 환경 설정](#environment-configuration)** <br/>
`해당 개발 가이드를 실천하기에 최적화된 개발 환경 설정을 소개합니다.`
- **[프로젝트 구조](#project-structure)** <br/>
`프로젝트의 주요 컴포넌트와 그들이 어떻게 상호작용하는지에 대한 설명입니다.`
- **[코딩 규칙](#code-style)** <br/>
`프로젝트에서 사용되는 코딩 스타일과 규칙에 대한 안내입니다.`
- **[유지 보수 정책](#sustaining-guide)** <br/>
`버그 수정, 새로운 기능 추가, 코드 리팩토링 등 프로젝트 유지 보수에 관한 정책을 설명합니다.`
- **[문제 해결 가이드](#solving-issues)** <br/>
`자주 발생하는 문제와 그 해결 방법에 대한 안내입니다.`

이 가이드를 통해 개발자들은 프로젝트에 더욱 효과적으로 참여하고, 고품질의 코드를 작성하며, 프로젝트의 성공에 기여할 수 있습니다.

<br/>
<br/>

## 개발 환경 설정 <span id="environment-configuration"><span>

본 가이드는 아래의 개발 환경 설정에 최적화되어 있습니다.

| 요소 | 이름 | 비고 |
| -- | -- | -- |
| 스크립트 편집기 | [VSCode](https://code.visualstudio.com/) | [언어 패키지](https://marketplace.visualstudio.com/items?itemName=MS-CEINTL.vscode-language-pack-ko), [vJass 확장](https://marketplace.visualstudio.com/items?itemName=jass.jass), [색상코드 미리보기 확장](https://marketplace.visualstudio.com/items?itemName=PhoenixZeng.color4wc3text) 설치 추천 |
| 지도 편집기 | World Editor(리포지드) | [워크래프트 III: 리포지드](https://warcraft3.blizzard.com/) 구매 및 설치 필요 |
| 지도 편집기 | JN Editor | [다운로드 링크 1](https://cafe.naver.com/w3umf/129002) 또는 [다운로드 링크 2](https://cafe.naver.com/w3umf/133212) |

<br/>
<br/>

## 프로젝트 구조 <span id="project-structure"><span>

### 개요

> [main.j](main.j) <br/>
> [📁 lib](lib) <br/>
> └ [📜 (listfile).j](lib/(listfile).j) <br/>
> [📁 sys](sys) <br/>
> └ [📜 (listfile).j](sys/(listfile).j) <br/>
> [📁 trigger](trigger) <br/>
> └ [📜 (listfile).j](trigger/(listfile).j) <br/>
> [📁 validation](validation) <br/>
> └ [📜 (listfile).j](validation/(listfile).j) <br/>

<br/>

### 상세

> [main.j](main.j) <br/>
> `이 파일은 프로젝트의 모든 소스 코드를 포함하는 핵심 파일입니다.` <br/>
> `트리거 에디터에서 main.j 파일을 import 하는 것으로 모든 코드를 지도에 적용할 수 있습니다.`
>
> [📁 lib](lib) <br/>
> └ [📜 (listfile).j](lib/(listfile).j) <br/>
> `이 디렉토리는 모든 범용 독립 라이브러리를 보관하는 곳입니다.` <br/>
> `지도와 장르에 구애받지 않는 라이브러리를 이 곳에 위치시키면, 필요에 따라 쉽게 사용할 수 있습니다.`
>
> [📁 sys](sys) <br/>
> └ [📜 (listfile).j](sys/(listfile).j) <br/>
> `이 디렉토리는 해당 지도에 의존성을 갖고 있는 라이브러리를 보관하는 곳입니다.` <br/>
> `게임 시스템과 관련되어 있는 라이브러리들이 이에 해당합니다.`
>
> <span id="rule-trigger"><span>
> [📁 trigger](trigger) <br/>
> └ [📜 (listfile).j](trigger/(listfile).j) <br/>
> `이 디렉토리는 실제 사용자와 상호 작용하는 콘텐츠를 작성하는 곳입니다.` <br/>
> `기능의 스파게티화를 막기 위해, 해당 디렉토리에 전역 변수와 라이브러리를 작성해서는 안 됩니다.`
>
> [📁 validation](validation) <br/>
> └ [📜 (listfile).j](validation/(listfile).j) <br/>
> `이 디렉토리는 디버그용 명령어(예:치트) 또는 기타 테스트용 기능을 작성하는 곳입니다.` <br/>
> `이 외의 기본적인 규칙은` [📁 trigger](#rule-trigger) `와 공유합니다.`

<br/>
<br/>

## 코딩 규칙 <span id="code-style"><span>

### 작명법

- 완성 버전의 코드에서는 축약된 이름이 최대한 등장하지 않도록 의미를 명확하게 합니다. <br/> *(u, p, i, btn, pid, int, str)* --> (unit, player, index, button, playerIndex, integer, string)

<br/>

### 식별자 표기법

| 분류 | 규칙 | 예시 |
| -- | -- | -- |
| constants | [blizzard.j](https://jass.sourceforge.net/doc/api/Blizzard_j-variables.shtml) 상수 표기법 | (blizzard.j) bj_PI, bj_MAX_PLAYERS <br/> (custom) rpg_MAX_PLAYERS, rpg_MAP_KEY |
| private constants | 스네이크 표기법(대문자) | MY_CONSTANT, SAMPLE_CONSTANT |
| library | 파스칼 표기법 | MyLibrary, SampleLibrary, SomeRandomLibraryName |
| scope | 파스칼 표기법 | MyScope, SampleScope, SomeRandomScopeName |
| function | 파스칼 표기법 | MyFunction, SamplePrivateFunction, SomeRandomPrivateFunction |
| private function | 카멜 표기법 | myFunction, samplePrivateFunction, someRandomPrivateFunction |
| global variable | 파스칼 표기법 | MyVariable, SampleVariable, SomeRandomVariableName |
| local variable | 카멜 표기법 | triggerUnit, playerIndex, data, someRandomInteger |

<br/>

### 주석

- 줄마다 주석을 붙이는 행위는 지양합니다. 우리는 이해할 수 있는 코드로 이야기합니다.
```cs
// [잘못된 예]
call AddSpecialEffectTarget( "E\\Onekill", u, "overhead" ) // 즉사 이펙트 표시
call KillUnit( u ) // 능력의 대상이 된 유닛을 죽입니다.
set u = null // null 처리
```
- 코드 블럭 또는 특정 구간을 설명하기 위해 한 줄 주석을 붙일 수 있습니다.
```cs
// 즉사 이펙트를 표시하고 유닛을 죽임
/* 즉사 이펙트를 표시하고 유닛을 죽임 (지도 파일에 기록되지 않는 주석) */
call AddSpecialEffectTarget( "E\\Onekill", spellTargetUnit, "overhead" )
call KillUnit( spellTargetUnit )

set spellTargetUnit = null
```
- 주석 블록(`/* */`)으로 함수 또는 라이브러리를 설명하지 않습니다. <br/> 대신, [VSCode vJass 확장](#environment-configuration)에서 제공하는 [마크다운 주석](https://github.com/escaco95/warcraft-iii-project-template/wiki/VSCode-%EB%A7%88%ED%81%AC%EB%8B%A4%EC%9A%B4-%EC%A3%BC%EC%84%9D-%ED%99%9C%EC%9A%A9%ED%95%98%EA%B8%B0)을 최대한 활용합니다.
```cs
// ---
// ### ⚙️ 유닛 - 유닛이 생존함
// > ([유닛](<unit whichUnit>)) 이 생존해있는지 확인합니다.
// ##### ℹ️ 이 함수는 제거된, 소멸한 유닛을 사망 상태로 판정합니다.
// ##### ℹ️ 이 함수는 부활 중인 유닛을 사망 상태로 판정합니다.
// ##### ℹ️ 이 함수는 쓰러진 영웅을 사망 상태로 판정합니다.
// ---
// **함수 형태**
// > ##### - ***whichUnit*** : 생존 여부를 확인할 유닛
function IsUnitAlive takes unit whichUnit returns boolean
    return not IsUnitType(whichUnit, UNIT_TYPE_DEAD) and GetUnitTypeId(whichUnit) != 0 
endfunction
```

<br/>
<br/>

## 유지 보수 정책 <span id="sustaining-guide"><span>

<br/>
<br/>

## 문제 해결 가이드 <span id="solving-issues"><span>
