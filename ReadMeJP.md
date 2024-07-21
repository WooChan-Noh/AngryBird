# AngryBird
Unityゲームスクール1期のポートフォリオ : アングリーバード (制作期間 : 4日間)
## デモ映像
[![Video Label](https://img.youtube.com/vi/Cj3ggTdfJUs/0.jpg)](https://www.youtube.com/watch?v=Cj3ggTdfJUs)
## ポートフォリオ作成時に立てた目標
- Unityに再び慣れる
- 授業で学んだことを適用する
  - HashValueをstatic readonlyで管理して使う
  - Listでオブジェクトを管理する
  - UI構造管理(transform.Find, onClick.AddListenerを使って管理)
  - 最適化(rigidbody.velocitiy.sqrMagnitude)
- C#高級文法を使う
  - Delegateでロジック管理
  - ラムダ式を使う
- シネマシンを使う
## 修正及び補完する点
- Birdに関連したデータを[Dictionary](https://assetstore.unity.com/packages/tools/utilities/serialized-dictionary-243052?locale=ko-KR)に統合してインスペクタで管理する
  - Enumを使うSwitch文を削除
## 使用アセット
### BGM
- AIVAで直接制作
- 使用プロンプト : not heavy, fun, old west
- 使用テーマ : heavy rock ensemble
- その後、自然なLoopのために一部直接修正
### 3D モデル (鳥、豚)
- [外部リンク](https://www.models-resource.com/mobile/angrybirdsgo/)
- 右下のボタンUIに使用された2Dアングリーバードは、Unityゲームスクール受講生が直接作って共有してくれたものを使用。
### サウンド(BGMを除く)  
- [外部リンク](https://www.sounds-resource.com/mobile/angrybirdsepic/sound/3940/)
### エフェクト(スキル、火)
- Cartton FX Remaster Free [アセットストア(無料)](https://assetstore.unity.com/packages/vfx/particles/cartoon-fx-remaster-free-109565)
- Low Poly Fire [アセットストア(無料)](https://assetstore.unity.com/packages/vfx/particles/fire-explosions/low-poly-fire-244190)
### マップ
- Low Poly Atmospheric Locations Pack [アセットストア(無料)](https://assetstore.unity.com/packages/3d/environments/landscapes/low-poly-atmospheric-locations-pack-278928)
- FREE Skybox Extended Shader [アセットストア(無料)](https://assetstore.unity.com/packages/vfx/shaders/free-skybox-extended-shader-107400)
- マップステージは直接配置
### UI
- UI Ultimate Clean GUI Pack [アセットストア(有料)](https://assetstore.unity.com/packages/2d/gui/ultimate-clean-gui-pack-154574)
## 説明
- ユーザーが右下のUIを押すと、その鳥が生成リスト(左上のトグル)に追加されます。
- 順番に鳥が生成され、飛んだ後に消えると次の鳥が生成されます。
- 黄色い鳥、黒い鳥、青い鳥はそれぞれスキルを持っており、飛んでいる途中でマウスを左クリックするとスキルを使用します。
### BirdManager.cs
- 鳥を動的に生成するので、これに必要なデータを持っています。
- 鳥のプリファブをResources.Loadを利用してstatic構造で持ってきて生成に活用します。
- BirdColorクラスとBirdTypeは生成した鳥オブジェクトのインタラクションに使います。(サウンド、エフェクトなど)
- Queue構造を使って鳥の生成を管理します。
### BirdsUI.cs
- Queue構造を使ってトグル(生成する鳥のリスト)を管理します。
- AddListenerに渡す関数にパラメータが必要なので、ラムダ式で一回括ってから追加しています。
- バードが生成されるたびに左にトグルを1つずつ移動します。
### BirdThrow.cs
- 各鳥のプリファブに付いている基本スクリプト。鳥を飛ばす動作に関わる機能を担当する。(飛行前、飛行中、飛行後)
- 鳥のタグを使って鳥の状態を確認して飛ばす。
- 予想される経路を事前にユーザーに表示する。この時、経路として表示されるオブジェクトはInstantiateで作成し、Listで管理する。
