# Town Pack — 마을·집·바 배경과 바 환경음

Town Pack은 작은 마을을 무대로 한 이야기를 위한 바로 쓸 수 있는 배경 모음입니다. 그려진 배경 세 장 — 마을 입구의 길모퉁이, 집 현관, 저녁의 바 — 과 바 환경음 루프를 담고 있습니다. 스토리나 장면, 캐릭터는 들어 있지 않으므로 그림을 어디에 보여줄지는 게임이 정합니다.

내장된 두 게임이 이미 이 팩을 함께 씁니다. **Cthangover**는 마을 입구와 현관을, **My Novel** 템플릿은 배경 세 장과 바 환경음을 모두 사용합니다. 두 게임이 이 모드의 같은 파일을 가져다 쓰기 때문에, Town Pack의 수정이나 개선된 그림은 양쪽 모두에 반영됩니다.

## 안에 무엇이 있나

마을 입구 `town/town_entry`: 줄무늬 차양을 단 가게들 사이 자갈길 모퉁이입니다.

![마을 입구 배경: 자갈길 모퉁이에 초록과 흰 차양을 단 모퉁이 건물.](assets/town_entry.jpg)

집 현관 `home/vestibule`: 계단과 안락의자, 그림이 있는 홀입니다.

![현관 배경: 따뜻한 조명의 홀에 나무 계단, 안락의자, 벤치, 액자 속 그림.](assets/vestibule.jpg)

바 `bar/bar`: 랜턴이 놓인 테이블, 카운터, 술병 선반입니다.

![바 배경: 랜턴 불빛 아래 테이블과 카운터, 들보 천장 아래 술병 선반.](assets/bar.jpg)

바 환경음 `bar/bar_ambient`: Ambience 사운드 채널용, 바 분위기를 담은 Ogg Vorbis 루프입니다.

세 그림은 모두 1920 × 1024입니다. 각 그림에는 같은 이름에 `_depth` 접미사를 붙인 회색조 파일이 짝으로 있습니다:

![마을 입구의 뎁스 이미지: 같은 구도의 회색조 버전.](assets/town_entry_depth.jpg)

뎁스 이미지는 직접 보이지 않습니다. 배경을 표시할 때 게임은 `<name>_depth`도 함께 읽어 조명 시스템에 넘기고, 시스템은 이를 바탕으로 장면 위에 놓인 빛을 계산합니다. 뎁스 짝이 없는 배경도 평소처럼 표시됩니다.

## 어디에서 보이나

- **Cthangover:** `town_entry` 장면(마을 입구)과 `home_vestibule` 장면.
- **My Novel 템플릿:** `my_novel_town`, `my_novel_home`, `my_novel_bar`. 바 장면에서는 `bar/bar_ambient`도 재생합니다.

같은 마을 입구가 My Novel 템플릿에서는 한 줄의 해설과 함께 게임을 엽니다:

![My Novel의 첫 장면: 마을 입구 배경 위에 "저녁의 마을. 가로등은 벌써 켜졌고, 시원한 바람이 자갈길을 따라 분다" 한 줄.](assets/reuse-my-novel.jpg)

그리고 Cthangover에서는 같은 그림 위를 다른 이야기가 자기 선택지로 덮습니다:

![Cthangover의 마을 입구: 같은 배경 위에 "집으로 돌아간다"와 "골목을 살펴본다" 선택지.](assets/reuse-cthangover.jpg)

Town Pack은 두 게임의 컬렉션에 모두 들어 있어 함께 로드됩니다. 설치만으로 다른 게임에 이 장소들이 생기지는 않습니다. 배경을 쓰는 것은 게임 자신의 장면입니다.

## 내 게임에서 배경 쓰기

1. 콘텐츠 모드의 `depends` 목록에 `town_pack>=1`을 추가합니다.
2. 게임의 컬렉션에 `town_pack>=1`을 추가합니다. My Novel 템플릿이 **Assets** 블록에서 하는 일이 그 예입니다.
3. 리소스는 아래 이름으로 참조합니다. 이름은 `backgrounds/`와 `sounds/` 기준 상대경로이며 확장자는 붙이지 않습니다.

```jsonc
// mods/my_game/manifest.json — 기존 목록에 추가
"depends": ["town_pack>=1"]
```

템플릿의 `my_novel_bar` 장면에서 가져온, 바를 보여주고 환경음을 트는 장면입니다:

```json
{
  "name": "my_bar",
  "defaultBackground": "bar/bar",
  "defaultAmbient": "bar/bar_ambient"
}
```

시나리오는 대화 도중에 그림을 바꿀 수도 있습니다:

```scenario
background town/town_entry
text "이 시간에 길은 텅 비어 있었다."
```

사용할 수 있는 이름은 다음과 같습니다:

```text
town/town_entry     backgrounds/town/town_entry.png
home/vestibule      backgrounds/home/vestibule.png
bar/bar             backgrounds/bar/bar.png
bar/bar_ambient     sounds/bar/bar_ambient.ogg
```

## 내 게임용으로 그림 바꾸기

Town Pack을 고치지 않고 그림을 바꾸려면, 같은 상대경로 이름의 파일(예: `backgrounds/bar/bar.png`)을 자신의 모드에 넣고 그 모드의 `depends`에 `town_pack>=1`을 선언하세요. 소유자에게 의존하는 모드가 나중에 로드되어 이깁니다. 배경을 바꿀 때는 같은 이름의 `_depth` 파일도 함께 넣으세요. 그렇지 않으면 Town Pack의 원래 뎁스 이미지가 그대로 발견되어 빛이 옛 그림의 구도를 따라갑니다.

의존성이 없으면 같은 이름을 놓은 두 모드의 순서는 정의되지 않으며, 리소스 맵 도구가 이를 오류로 보고합니다.

## 뭔가 빠졌을 때

1. 배경이 검게 나오거나 사라졌다면 대개 이름을 잘못 쓴 것입니다. 이름은 대소문자를 구분하며 `/`를 씁니다.
2. Town Pack이 설치만 된 것이 아니라 실행한 게임에 포함되어 있는지 확인하세요.
3. 바 소리가 안 들리면: 장면의 `defaultAmbient`가 `bar/bar_ambient`인지, **Settings → Sound**에서 **Ambience**가 켜져 있는지 확인하세요. 소리 재생은 Audio Engine 모드가 맡습니다.
