# AngryBird
멋쟁이사자처럼 유니티 게임스쿨 1기 첫 번째 포트폴리오 : 앵그리버드 (제작 기간 : 4일)
## 시연 영상
[![Video Label](https://img.youtube.com/vi/Cj3ggTdfJUs/0.jpg)](https://youtube.be/'Cj3ggTdfJUs')
## 포트폴리오 제작 시 세운 목표
- 유니티에 다시 익숙해지기
- 수업 시 배운 것 적용
  - Hash값을 static readonly로 관리하여 사용
  - List로 오브젝트 관리
  - UI 구조 관리 (transform.Find, onClick.AddListener 사용하여 관리)
  - 최적화 (rigidbody.velocitiy.sqrMagnitude)
- 고급 문법 사용
  - Delegate으로 로직 관리
  - 람다식 사용
- 시네머신 사용
## 수정 및 보완할 점
- Bird에 관련된 데이터를 [Dictionary](https://assetstore.unity.com/packages/tools/utilities/serialized-dictionary-243052?locale=ko-KR)로 통합하여 인스펙터에서 관리
  - Enum을 사용한 Switch문 제거
## 사용 에셋
### 배경음악
- AIVA로 직접 제작
- 사용 프롬프트 : not heavy, fun, old west
- 사용테마 : heavy rock ensemble
- 이후 자연스러운 Loop를 위해 일부 직접 수정
### 3D 모델 (새, 돼지)
- [외부 링크](https://www.models-resource.com/mobile/angrybirdsgo/)
- 오른쪽 하단의 버튼 UI에 사용된 2D 앵그리버드 도트는 유니티 게임 스쿨 수강생이 직접 찍어 공유해준 것을 사용함
### 사운드 (배경음악 제외)  
- [외부 링크](https://www.sounds-resource.com/mobile/angrybirdsepic/sound/3940/)
### 이펙트 (스킬, 불)
- Cartton FX Remaster Free [에셋 스토어(무료)](https://assetstore.unity.com/packages/vfx/particles/cartoon-fx-remaster-free-109565)
- Low Poly Fire [에셋 스토어(무료)](https://assetstore.unity.com/packages/vfx/particles/fire-explosions/low-poly-fire-244190)
### 맵
- Low Poly Atmospheric Locations Pack [에셋 스토어(무료)](https://assetstore.unity.com/packages/3d/environments/landscapes/low-poly-atmospheric-locations-pack-278928)
- FREE Skybox Extended Shader [에셋 스토어(무료)](https://assetstore.unity.com/packages/vfx/shaders/free-skybox-extended-shader-107400)
- 맵 스테이지는 직접 배치함
### UI
- UI Ultimate Clean GUI Pack [에셋 스토어(유료)](https://assetstore.unity.com/packages/2d/gui/ultimate-clean-gui-pack-154574)
## 설명
- 사용자가 오른쪽 하단의 UI를 누르면 해당 새가 생성 목록(왼쪽 상단 토글)에 추가됨
- 순서에 맞게 새가 생성되고, 날아간 뒤 사라지면 다음 새가 생성된다.
- 노란 새, 검은 새, 파란 새는 각각 스킬을 가지고 있으며 날아가는 도중 마우스 왼클릭을 하면 스킬을 사용한다.
### BirdManager.cs
- 새를 동적으로 생성하므로 이에 필요한 데이터들을 가지고 있다.
- 새 프리팹을 Resources.Load를 활용해 static 구조로 가지고 생성에 활용한다.
- BirdColor 클래스와 BirdType 열거형은 생성한 새 오브젝트의 상호작용에 사용한다. (사운드, 이펙트 등)
- Queue 구조를 사용하여 새 생성을 관리한다.
### BirdsUI.cs
- Queue 구조를 사용하여 토글(생성할 새 목록)을 관리한다.
- AddListener에 넘길 함수에 파라미터가 필요하여 람다식으로 한 번 묶은 다음에 추가하였다.
- 새가 생성될 때마다 왼쪽으로 토글을 한 칸씩 옮겨준다. 
### BirdThrow.cs
- 각 새의 프리팹에 붙어있는 기본 스크립트. 새를 날리는 행동에 관련된 기능을 담당한다. (날리기 전, 날아가는 도중, 날아간 후)
- 새의 태그를 사용하여 새의 상태를 확인하고 날린다.
- 예상 경로를 미리 사용자에게 보여준다. 이 때 경로로 표시되는 오브젝트는 Instantiate로 생성하고 List로 관리한다.
