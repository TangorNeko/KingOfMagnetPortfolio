# **磁界之王**
### 河原電子ビジネス専門学校
### ゲームクリエイター科3年　錦織隼王

# **目次**
### 1. [作品概要](#overview)
### 2. [操作説明](#operation)
### 3. [担当ソースコード](#responsible)
### 4. [改造したエンジンのコード](#enginecode)
### 5. [画面分割](#splitview)
### 6. [ブルーム](#bloom)
### 7. [カスケードシャドウ](#shadow)
### 8. [ディファードレンダリング](#deferred)
### 9. [カプセルコライダー](#capsule)
### 10. [弾の発射先の決定](#bullet)
### 11. [リングゲージ](#ringgauge)
### 12. [ゲームでこだわった部分](#commitment)

<a id="overview"></a>

# **1. 作品概要**
* ## 磁界之王(じかいのおう)
    三人称視点の二人対戦シューティングゲームで、  
    各プレイヤーにかかる磁力を考えた攻撃・行動をしながら  
    もう一人のプレイヤーを倒すゲームです。
    <iframe width="640" height="365" src="https://www.youtube.com/embed/kX87_XVBVlo" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>  

    **紹介動画**
* ## 使用ゲームエンジン
    学校内製エンジンを改造して使用
* ## 使用ツール
    Visual Studio 2019  
    Visual Studio Code  
    3ds Max 2021  
    Adobe Photoshop Elements 2020  
    Git
* ## 使用言語
    C++  
    HLSL
* ## 開発環境
    Windows10  
    DirectX12
* ## 制作人数
    4人
* ## 開発期間
    2021年2月～2021年8月

<a id="operation"></a>

# **2. 操作説明**
<img src="Pictures/Control1.png" width="720">   

<a id="responsible"></a>

# **3. 担当ソースコード**  

<details open>
<summary>担当ソースコード</summary>

* BackGround.cpp  
* BackGround.h  
* Bomb.cpp(一部)  
移動処理以外を担当  
* Bomb.h  
* CascadeShadow.cpp
* CascadeShadow.h
* CDirectionLight.cpp  
* CDirectionLight.h  
* CEffect2D.cpp  
* CEffect2D.h  
* CFontRender.cpp  
* CFontRender.h  
* CLevel.cpp  
* CLevel.h  
* CLevelRender2D.cpp  
* CLevelRender2D.h  
* CLightManager.cpp  
* CLightManager.h  
* CMapChipRender.cpp  
* CMapChipRender.h  
* CPointLight.cpp  
* CPointLight.h  
* CSkinModelRender.cpp  
* CSkinModelRender.h  
* CSpotLight.cpp  
* CSpotLight.h  
* CSpriteRender.cpp  
* CSpriteRender.h  
* DamageDisplay.cpp  
* DamageDisplay.h  
* Debris.cpp  
* Debris.h  
* DebrisBlock.cpp  
* DebrisBlock.h  
* DeferredRendering.cpp  
* DeferredRendering.h  
* GameOption.cpp  
* GameOption.h  
* GameScene.cpp(一部)  
ゲームシーンの初期化処理、シーンの移行関係の処理を担当  
* GameScene.h(一部)  
ゲームシーンの初期化処理、シーンの移行関係の処理を担当  
* GravityBullet.cpp(一部)  
弾の見た目以外の処理を担当  
* GravityBullet.h(一部)  
弾の見た目以外の処理を担当  
* MobiusGauge.cpp  
* MobiusGauge.h  
* MyCapsuleCollider.cpp  
* MyCapsuleCollider.h  
* OptionValue.cpp  
* OptionValue.h  
* Player.cpp(一部)  
移動、弾の保持、発射、必殺技、当たり判定、カメラの移動を担当  
* Player.h(一部)  
移動、弾の保持、発射、必殺技、当たり判定、カメラの移動を担当  
* PostEffectManager.cpp  
* PostEffectManager.h  
* RoundCounter.cpp  
* RoundCounter.h  
* SkyBoard.cpp  
* SkyBoard.h  
* TitleScene.cpp(一部)  
ゲームオプションの展開処理、背景の処理を担当  
* TitleScsne.h(一部)  
ゲームオプションの展開処理、背景の処理を担当  
* TriangleCollider.cpp  
* TriangleCollider.h  
* cascadeShadow.fx  
* deferredModel.fx
* DeferredSprite.fx
* model.fx
* PBR.fx
* postEffect.fx
* ringUI.fx
* shadow.fx
* shadowReceiver.fx
* SkyBoard.fx

</details>

<a id="enginecode"></a>

# **4. 改造したエンジンのコード**
<details open>
<summary>改造したエンジンのコード</summary>

* GameObjectManager.cpp  
ディファードレンダリングやポストエフェクト、シャドウの描画  
画面分割の描画に対応  
* CharacterController.cpp  
即座に降りられる段差の高さを変更  
* Camera.cpp  
画面分割に応じてカメラのアスペクト比をセットできるように変更  
* GraphicsEngine.cpp  
FPSの固定ができるように変更  
* GraphicsEngine.h  
画面分割するかどうかのフラグを追加  
* IGameObject.h  
レンダリングモードによって描画する関数を変えられるように変更
* Material.cpp  
使用するカラーバッファのフォーマットを指定できるように変更  
FlyWeightパターンを利用したシェーダーファイルの読み込みの高速化  
* MeshParts.cpp、MeshParts.h  
使用できる定数バッファの数を増加させた  
* Model.cpp、Model.h  
初期化の際のモデルの読み込みをFlyWeightパターンを利用し高速化  
線分とモデルとの交差判定関数の追加  
ビュー行列とプロジェクション行列を直接指定して描画できるように変更  
* RenderContext.h  
描画する画面を指定できるように変更  
* Sprite.cpp  
乗算カラーを指定できるように変更  
使用するカラーバッファのフォーマットを指定できるように変更  
ブルーム時に画面端から周囲のピクセルをサンプリングした際に反対側の端にループしないようTEXTURE_ADDRESS_MODEを変更  
使用できる定数バッファの数を増加させた  
* Texture.h  
テクスチャの幅と高さを取得する関数を追加


</details>

<a id="splitview"></a>

# **5. 画面分割**
<img src="Pictures/Viewport1.png" width="540">    

2人のプレイヤーがそれぞれの視点を持つため、2つの画面が必要ですが、  
複数のVIEWPORTを用意することで画面分割を実装しています。  
分割せず画面全体に表示したいスプライト等のため、  
画面全体を覆うVIEWPORTも用意し、そちらでスプライト等の描画を行っています。  
<img src="Pictures/Viewport2.png" width="540">

<a id="bloom"></a>

# **6. ブルーム**
川瀬式ブルームを実装。  
通常シーンをオフスクリーンレンダリング後、輝度が高いピクセルを抽出し、  
ブラーとダウンサンプリングをかけながら複数枚のテクスチャを作成し、  
複数枚のテクスチャの平均を取って加算合成しています。  
<img src="Pictures/Bloom1.png" width="540">  
**通常シーン**  
<img src="Pictures/Bloom2.png" width="540">  
**輝度抽出したテクスチャ**  
<img src="Pictures/Bloom3.png" width="540">  
**ブラーをかけながらダウンサンプリングしたテクスチャ**  
**(さらにダウンサンプリングしながら複数枚作成)**  
<img src="Pictures/Bloom4.png" width="540">  
**加算合成後**  

<a id="shadow"></a>

# **7. カスケードシャドウ**
影の描画には、カメラからの距離に応じて解像度の違う複数のシャドウマップを使い分ける  
カスケードシャドウを使用しています。  
そのため、近くの影は高品質に、遠くの影は低品質に(遠いので影響が殆どない)なっています。  
画面が2つあるゲームなので、2(左画面、右画面) ✕ 3(近距離、中距離、遠距離)  
の6つのシャドウマップに描画しています。  
<img src="Pictures/Shadow1.png" width="540">  
**作成されたシャドウマップ**    
<img src="Pictures/Shadow2.png" width="540">  
**近距離と中距離用のシャドウマップで描かれた影**    

<a id="deferred"></a>

# **8. ディファードレンダリング**
ディファードレンダリングを行い、ライティングの計算が呼ばれる回数を減らしています。  
DirectXのマルチレンダーターゲット描画を利用し、アルベド、法線、ワールド座標のG-Bufferを出力しています。 
その後、G-Bufferを使用してライティングを行う事で、  
画面に描画されるピクセルのみにライティングの計算を行います。  
また、今回はUVスクロールする空のみ特殊なライティングを行うので  
ディファードレンダリングの後、空のみフォワードレンダリングで描画しています。  
<img src="Pictures/Deferred1.png" width="540">  
**アルベドG-Buffer**  
<img src="Pictures/Deferred2.png" width="540">  
**法線G-Buffer**  
<img src="Pictures/Deferred3.png" width="540">  
**ワールド座標G-Buffer**  
<img src="Pictures/Deferred4.png" width="540">  
**ディファードライティング+空のみフォワードレンダリング**  

<a id="capsule"></a>

# **9. カプセルコライダー**
プレイヤーと弾との当たり判定のため、カプセルコライダーを作成し、使用しています。  
移動処理によって移動する前の弾の座標と、移動した後の弾の座標を  
カプセルの端点にすることで、スピードの速い弾でもプレイヤーをすり抜けることなく  
判定する事ができます。  
<img src="Pictures/CapsuleCollider1.png" width="540">  

<a id="bullet"></a>

# **10. 弾の発射先の決定**
三人称視点のゲームのため、どうしても照準で狙う方向とプレイヤーが弾を発射する方向が  
ずれてしまいます。
そこで、カメラから照準の方向にレイを飛ばし、  
最初にレイがステージのモデルに当たった座標に向かって弾を発射するようにしています。

<img src="Pictures/ShotRay1.png" width="540">  

しかし、これだけでは相手プレイヤーを狙ったとしてもその奥にあるステージを狙う事になり、  
相手プレイヤーに向かって弾を飛ばす事が困難です。

<img src="Pictures/ShotRay2.png" width="540">  

そこで、各プレイヤーに常に相手のプレイヤー方向を向く平面の当たり判定を用意し、  
そこに照準の方向へのレイが交差した場合も交差地点に弾を発射するようにしました。  
<img src="Pictures/ShotRay3.png" width="300">  
**プレイヤーの向きに関係なく常に相手方向に向く**
<img src="Pictures/ShotRay4.png" width="540">  

<a id="ringgauge"></a>

# **11. リングゲージ**
プレイヤーの磁力の状態を表すゲージとして、8の字の形のゲージを用意しています。  
<img src="Pictures/RingGauge1.png" width="540">  
内積を利用して描画ピクセルの角度を計算し、指定した角度以上なら描画する  
といったリングゲージを作成し、それを2つ並べて配置することで  
8の字に減少するようにしました。  
<img src="Pictures/RingGauge2.png" width="540">  
<img src="Pictures/RingGauge3.png" width="300">  

<a id="commitment"></a>

# **12. ゲームでこだわった部分**
## 1.決着時のカメラ

バトルに決着がついた際、2画面分割の対戦画面から演出用の1画面に切り替わり、  
勝者を映す演出を流しています。  
<img src="Pictures/FinalHit1.png" width="540">  
**倒れる敗者を映し**  
<img src="Pictures/FinalHit2.png" width="540">  
**敗者からゆっくりと勝者にカメラが移動する**  
<img src="Pictures/FinalHit3.png" width="540">  
**最後は勝者プレイヤーを映す**  


## 2.磁力の状態によるプレイヤーの行動のメリハリ
磁界之王では、引力状態では通常の攻撃は一切できず、バーストでも敵の弾を引き寄せてしまう完全なデメリット状態です。  
しかし、攻撃に必要な弾は引力状態でしか集める事ができません。  
斥力状態では通常の攻撃の他、バーストによって相手の攻撃を弾く事ができます。  
このように、磁力の状態によってはっきりとした有利、不利を作る事で、  
プレイヤーが今できる行動を明確にし、次に何をするか選択しやすいようにしています。