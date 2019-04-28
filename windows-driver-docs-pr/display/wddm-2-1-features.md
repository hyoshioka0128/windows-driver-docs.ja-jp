---
title: WDDM 2.1 の機能
description: このセクションでは、新機能と Windows Display Driver Model (WDDM) バージョン 2.1 の機能強化について説明します。
ms.assetid: 7dc0d0ad-98da-4bd6-bed9-f70525b682bc
ms.date: 01/10/2019
ms.localizationpriority: medium
ms.openlocfilehash: 9299bf0a565c4765c1cfe506c6e4fdc513cd0a08
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378416"
---
# <a name="wddm-21-features"></a>WDDM 2.1 の機能


このトピックでは、以降、Windows 10 Anniversary Edition で利用できるある新機能と Windows Display Driver Model (WDDM) バージョン 2.1 では、機能強化の詳細についてを説明します。

WDDM 2.1 自体は省略可能です。 実装されている場合は、必須およびオプションのドライバーの機能のコレクションです。 これらの機能のいずれかをサポートする任意のドライバーには、すべての必須のものをサポートする必要があります。  サポートは HLK テストを検証できますが、Dxgkrnl 機能および Ddi の一貫性が確認されます。

**WDDM 2.1 の要件の表**

| 機能 | 適用条件 |
| --- | --- |
| 提供し、改善を再利用 | 必須 |
| ビデオ メモリ管理 | 省略可能 |
| ハードウェア保護コンテンツの信頼性に関する機能強化 | ハードウェアを選択します。 |
| Windows GameDVR でアプリケーションのサポート | 必須 |
| 間接的な表示 | ハードウェアを選択します。 |
| ドライバー ストアとサイド バイ サイドのインストール | 必須 |
| 共有/カメラ キャプチャ シナリオを DirectX メモリ画面 | 必須|

WDDM 2.1 には、次の D3D バージョンがサポートされています。D3D9, D3D10, D3D10.1, D3D11, D3D11.x, D3D12

## <a name="offer-and-reclaim-improvements"></a>提供し、改善を再利用

新しい DDI, [PFND3DDDI_RECLAIMALLOCATIONS3CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimallocations3cb)バック グラウンド モードで実行されているアプリケーションのメモリ使用量を減らすために作成されました。 このインターフェイスは、完全にコミット解除、バック グラウンドに移行するときに使用可能なリソースを提供するアプリケーションを有効になります。 その結果、プロセスの有効期間マネージャーはメモリの負荷がかかったときに少ないバック グラウンド アプリケーションの終了につながる、DirectX を使用するバック グラウンド アプリからより多くのメモリを解放することになります。

その他の DDI 変更:

* [PFND3DDDI_UPDATEALLOCATIONPROPERTYCB コールバック](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_updateallocationpropertycb)
* [PFND3DDDI_OFFERALLOCATIONS2CB コールバック](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_offerallocations2cb)
* [D3DDDICB_OFFERALLOCATIONS2 構造体](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-d3dddicb_offerallocations2)
* [D3DDDICB_RECLAIMALLOCATIONS3 構造体](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddicb_reclaimallocations3)

プランし、リソースを解放の詳細についてを参照してください。[変更のプランと回収](offer-and-reclaim-changes.md)します。

## <a name="application-support-with-windows-gamedvr"></a>Windows GameDVR でアプリケーションのサポート

Windows 10 Anniversary edition には、全画面表示のゲームを使用して Windows ゲーム バーと GameDVR 機能強化にはが含まれています。

WDDM 2.1 ドライバーと呼ばれるパフォーマンス機能をサポートするために必要な*バッチ処理を提示*、フリップ モデル スワップのマルチ スレッドのサポートを追加します。 これは、Windows の以前のバージョンの同じレベルのパフォーマンスで実行するゲームのバーでその全画面表示をゲームにより不可欠な機能です。

この機能を有効にするために作成する新しい Ddi を次に示します。

* [PFND3DDDI_SYNCTOKENCB コールバック](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_synctokencb)
* [D3DDDIARG_SYNCTOKEN 構造体](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_synctoken)
* [PFND3DDDI_SYNCTOKEN コールバック](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_synctoken)


## <a name="indirect-display"></a>間接的な表示

WDDM 2.1 では、間接的な表示を USB 接続の表示に参加するすべての同じユーザー エクスペリエンスの他のいずれかのモニターとして使用できます。 さらに、間接的なディスプレイ ドライバーは、カーネル モード ドライバーより簡単に開発し、システムの全体的な信頼性の向上に貢献してその結果、ユーザー モード ドライバーです。

WDDM 2.1 では、以下 USB 表示機能/のエクスペリエンスが有効にします。

* Windows プラットフォームまたはオペレーティング システムをアップグレードする USB ディスプレイを接続するときに、適切なドライバーがダウンロードされ、Windows update からインストールされています。

* USB ディスプレイ ハードウェアにモニターを接続する、検出し、トポロジ、解像度と DPI に適切なモニターを設定します。

* ユーザーは、モニターの解像度とモニターのスケーリングを変更できます。

* ユーザーは、USB の表示を切断し、予期しない副作用なしの表示を再接続します。

* モニターのトポロジの保持を切断し、同じのモニターに再接続します。

* USB は、スリープ、休止状態など、さまざまな電源状態で正しく関数を表示します。

間接的な表示の詳細については、次を参照してください[間接ドライバー モデルの概要の表示。](indirect-display-driver-model-overview.md)

## <a name="driver-store-and-side-by-side-driver-installation"></a>ドライバー ストアとサイド バイ サイドでドライバーのインストール

WDDM 2.1 からグラフィックス ドライバーのインストールが導入されています、*ドライバー ストア*します。 グラフィック ドライバーをインストールするには、このメカニズムは、システムが不安定にドライバー ファイル バージョンの不一致を排除すること、Windows Update からドライバーの更新プログラムの回復性を向上し、ユーザーが開始した再起動されます。 各後続のドライバーの更新がドライバー ストア内の一意の場所から直接実行されます (つまり`System32\DriverStore\FileRepository\[…]`)、避けるドライバー ファイルが上書きされと一致しません。

ドライバー ストアの機能の実装では、固有のドライバー リポジトリにドライバー ファイルをコピーすることを確認するには、グラフィックス ドライバーの INF ファイルに変更が必要です。 INF 変更については、詳細で、 [INF 要件](#graphics-inf-requirements)このドキュメントの「します。

## <a name="dxil"></a>DXIL

WDDM 2.1 により、GPU シェーダー コンパイラ スタックの遷移が DirectX バイト コード (DXBC) からに DirectX 中間言語 (DXIL)、GPU にシェーダーの命令を送信するための新しい形式について説明します。 DXIL への移行は、開発者に、次の利点をもたらします。

* プログラミングの開発の容易さが向上し、GPU プログラミング構文と開発者が慣れ親しんでいる CPU 言語間の違いを最小限に抑えることによって開発者のため、シェーダーの作成プロセスの複雑さが減ります。

* コンパイラの高パフォーマンスの向上: 

    * *実行時のシェーダー パフォーマンス*を有効にすると、優れたパフォーマンスを提供します。 
    * DXIL では、Gpu で SIMD プロセッサのレーンの間でデータを共有できるようにする、組み込みの新しいセットを提供します。

* ワークフローの柔軟性 - DXIL により、独自のカスタム ツールの制御するために開発者と最適化渡し、コンパイル手順が実行時とビルド時に適用されるかを選択します。

* 言語の機能 - 高度な進化の言語は、GPU と CPU のコード間の相違点を排除し、GPU プログラマのための学習曲線を平坦化する主な機能を提供します。

これらの機能を開発者向けの特典を提供することに重点を置いて、エンドユーザーはも、既存のハードウェアで実行と新しいまたは更新されたゲームのパフォーマンスの向上のメリットが表示されます。

## <a name="directx-memory-surface-sharing-for-cameracapture-scenarios"></a>共有/カメラ キャプチャ シナリオを DirectX メモリ画面

WDDM 2.1 では、共有、カメラまたはデバイスを同時に複数のプロセスでキャプチャするフレームのサーバー コンポーネントが登場しました。 これにより、複数のアプリケーションを複数回のプロセスと子プロセスのイメージ データのコピーではなくから読み取ることができます、1 つのメモリの場所にキャプチャされたフレームを保存します。 この機能によりキャプチャした画像の管理をより効率的な複数のプロセス、省電力、帯域幅の削減、および WDDM 2.1 準拠のハードウェアとドライバーの待機時間の削減の間でパフォーマンスが向上する結果アプリケーションとユーザーの。

フレーム サーバーでは、プロセス間の共有可能なメモリとしてキャプチャしたイメージを割り当て、アクセスを要求するプロセスをこのメモリを共有します。 フレームのサーバーでは、複数のクライアント プロセスにテクスチャをブロードキャスト、ため、テクスチャは同時読み取りをサポートする必要があることに注意することになります。 現在 NV12 テクスチャは、この目的のためサポートされます。

## <a name="pipeline-state-object-pso-caching-and-library"></a>パイプライン状態オブジェクト (PSO) のキャッシュとライブラリ

D3D12 で導入された、パイプライン状態オブジェクト (PSO) は、グラフィックス パイプラインの説明、およびリソースを表すインターフェイス (状態とも呼ばれます) として D3D とドライバーの分解の状態の不一致を減らすには、統一されたオブジェクト。 視覚的に厳しいアプリケーションやゲーム Pso の膨大な数を作成する必要が実行されています。 

WDDM 2.1 PSO のライブラリとキャッシュは、物理記憶域、初期の実行中に作成した後、PSO を格納するゲーム アプリケーションを使用できます。 これは、D3D ランタイムに、インスタンスを減らす PSO の抽出に将来のライブラリから事前に作成した Pso を取得する機能を提供します。 たとえば、または PC を再起動した後、2 回目以降後は、ゲームを実行中、コンテンツはから読み込む物理ライブラリとして保存された Pso。


## <a name="start-of-pipeline-gpu-timestamps"></a>GPU のタイムスタンプをパイプラインの開始

WDDM 2.1 では、GPU パイプラインでグラフィックス イベントのタイムスタンプの開始を取得する機能が導入されました。 パイプラインのタイムスタンプの末尾と組み合わせて使用して、新機能として、開発者は、並列処理の明確で詳細な視覚エフェクトをパイプライン処理、およびタイミングの GPU 上で発生している、アプリケーションのアクティビティ。 指定の各イベントの実行時間を開発者がさらに、コードを最適化し、非効率性やその他のパフォーマンスの問題を調査できます。

この機能は、'リアルタイム、低オーバーヘッド' の有効化に貢献 GPU パフォーマンス データ収集と同時を視覚化し、Gpu でワークロードを測定するのに十分な情報を提供します。 機能の目的は、正確な順序を再構築するための十分な情報を提供して、ツールは、並列処理と、エンジンとパイプライン処理を視覚化できるように、GPU で実行される操作の継続時間は、GPU ワークロードを測定し、可能性を識別します。同期の問題。

## <a name="viewing-gpu-microcode"></a>GPU マイクロ コードを表示します。

WDDM 2.1 では、GPU マイクロ コードの表示を提示してそのシェーダーがさらに最適化できます。 開発者は、GPU ドライバーの中間言語にコンパイルされたもので、HLSL シェーダーを作成、グラフィックス パイプラインをプログラムします。 ドライバーは、追加のコンパイルと開発者に不透明なまま GPU に固有の手順を次のコードを変換するための最適化を実行します。 この機能により、開発者には、シェーダーの最適化と速度のエクステントを評価する読み取り可能な GPU に固有のコードが表示されます。

この機能により、グラフィックス パイプラインのプログラミング可能な各ステージに (とも呼ばれますコメント UMD。 シェーダー) プログラマの使用やこれらのシェーダーの誤用の実用的な情報を返すとします。 GPU 固有マイクロ コードが逆アセンブルし、UMD コメントと共にが判読できる文字列形式で表示されます。 開発者は、読み取り可能な GPU コードにサイド バイ サイドを動的に、コードを変更し、GPU コード側のコンパイラ最適化の結果を確認できるように、HLSL コードのマッピングを表示できます。

## <a name="determining-wddm-version"></a>WDDM バージョンを確認します。

### <a name="wddm-21-caps"></a>WDDM 2.1 キャップ

ドライバーを通じて WDDM 2.1 のサポートが報告されます[DXGK_DRIVERCAPS::WDDMVersion](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)と新しいバージョンの定数。

`DXGK_WDDMVERSION::DXGKDDI_WDDMv2_1 = 0x2100`

Dxgkrnl は使用しません、 **WDDMVersion**キャップがサポートされている新しい機能を決定する方法として、そのタスクは、他の cap または DDI プレゼンスに委ねられます。 ただし、ドライバーが報告 WDDM 2.1 サポートを通じて、 **WDDMVersion**キャップを dxgkrnl は cap または WDDM 2.1 で必要な Ddi が存在し、それ以外の場合、アダプターの作成に失敗することが検証されます。 一貫性のない cap アダプターまたはセグメントの作成に失敗が発生します。

> [!NOTE]
> 既存または新しいアプリケーションは、ここで説明しているなどのプラットフォームの機能強化を有効になっている任意の Windows 10 Anniversary Edition 機能を活用するために、ドライバー モデルのクエリを実行することはできません。 すべての機能の変更は、それぞれランタイムを通じて表示される必要があります。

新しい定数が KMT_DRIVERVERSION_WDDM_2_1 を一致するように追加されています。

```cpp
typedef enum _DXGIDRIVERMODELVERSION
{
    DXGIDMVERSION_1_0            = 1000,
    DXGIDMVERSION_1_1_PRERELEASE = 1102,
    DXGIDMVERSION_1_1            = 1105, 
    DXGIDMVERSION_1_2            = 1200,
    DXGIDMVERSION_1_3            = 1300,
    DXGIDMVERSION_2_0            = 2000,
    DXGIDMVERSION_2_1            = 2100,

} DXGIDRIVERMODELVERSION;
```

KMD DDI インターフェイス バージョンは次のとおりです。 

```cpp
#define DXGKDDI_INTERFACE_VERSION_VISTA      0x1052
#define DXGKDDI_INTERFACE_VERSION_VISTA_SP1  0x1053
#define DXGKDDI_INTERFACE_VERSION_WIN7       0x2005
#define DXGKDDI_INTERFACE_VERSION_WIN8       0x300E
#define DXGKDDI_INTERFACE_VERSION_WDDM1_3    0x4002
#define DXGKDDI_INTERFACE_VERSION_WDDM1_3_PATH_INDEPENDENT_ROTATION  0x4003
#define DXGKDDI_INTERFACE_VERSION_WDDM2_0    0x5023
#define DXGKDDI_INTERFACE_VERSION_WDDM2_1    0x6002
```

## <a name="graphics-inf-requirements"></a>グラフィックス INF の要件

WDDM 2.1 グラフィック ドライバーには、WDDM 2.0 または以前のドライバーと比較して異なる INF 要件があります。 それらを次に示します。

1. WDDM 2.1 には、WDDM 2.0 グラフィックス ドライバー (D1) の場合と同じの特徴のスコアが必要です。

2. WDDM 2.1 グラフィック ドライバーは、さまざまな OS INF インストール セクションを使用する必要があります。

3. WDDM 2.1 グラフィックス ドライバーの INF は、"Store"がドライバーのインストールを変更します。

詳細については、次を参照してください。 [INF ファイルのセクションとディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)します。

ドライバー ファイル、32 ビットと 64 ビットに保持され、ドライバー ストアから読み込まれます。 WoW64 ファイル システムのリダイレクトは、ドライバー ストアには適用されません。 Ihv は、必要な場合は、一意のドライバー ストアのフォルダーの下の WoW64 フォルダーなどを作成する標準の INF 構文を使用して、サブフォルダーを指定できます。

次は、以前の動作の実行をドライバー ストアから INF サポートの相違の例です。

```inf
WINDOWS 10 ANNIVERSARY EDITION APPROACH: RUNNING DRIVERS FROM THE DRIVER STORE
[DestinationDirs]
KMDCopyFiles = 13
UMDCopyFiles = 13
UMDWoW64CopyFiles = 13

[DDInstall]
CopyFiles=KMDCopyFiles
CopyFiles=UMDCopyFiles
CopyFiles=UMDWoW64CopyFile

[KMDCopyFiles]
myKMD.sys

[UMDCopyFiles]
myUMD64.dll
myOpenCL64.dll
myOpenGL64.dll

[UMDWow64CopyFiles]
myUMD32.dll
myOpenCL32.dll
myOpenGL32.dll

[DDInstall.Services]
AddService = serviceName, 0x00000002, serviceName_Service_Inst

[serviceName_Service_Inst]
ServiceBinary = %13%\serviceName.sys

[regAdd]
HKR,,UserModeDriverName,%REG_MULTI_SZ%,%13%\myUMD64.dll, %13%\myUMD64.dll, %13%\myUMD64.dll, %13%\myUMD64.dll
HKR,,UserModeDriverNameWoW,%REG_MULTI_SZ%, %13%\myUMD32.dll, %13%\myUMD32.dll, %13%\myUMD32.dll, %13%\myUMD32.dll
HKLM,"Software\Khronos\OpenCL\Vendors",%13%\myOpenCL64.dll,%REG_DWORD%,0x00000000
HKLM,"Software\Wow6432Node\Khronos\OpenCL\Vendors",%13%\ myOpenCL32.dll,%REG_DWORD%,0x00000000
HKR,,OpenGLDriverName,%REG_MULTI_SZ%,%13%\myOpenGL64.dll
HKR,,OpenGLDriverNameWoW,%REG_MULTI_SZ%,%13%\myOpenGL32.dll
```

サブフォルダーを指定するには、次の例に示すように、ドライバーは構文を使用する可能性があります。

```inf
...
[DestinationDirs]
...
UMDWoW64CopyFiles = 13,WoW64
...
[regAdd]
...
HRK,, UserModeDriverNameWoW,%REG_MULTI_SZ%, %13%\WoW64\myUMD.dll, %13%\WoW64\myUMD.dll, %13%\

The new manufacturer install section decoration for Windows 10 Anniversary edition WDDM 2.1 drivers is as follows: 
...
[Manufacturer]
%Grfx_Manf% =  IHVGfx, NTamd64.10.0…14310
...
[IHVGfx.NTamd64.10.0…14310]
; HW ID list
[list of HW IDs]
```

## <a name="driver-versioning"></a>ドライバーのバージョン管理

グラフィックス アダプターまたはチップセット ドライバー DLL と SYS ファイルを正しく書式設定されたファイルのバージョンが必要です。

ドライバー情報ファイル (.inf)、カーネル モード ドライバー (.sys) とユーザー モード ドライバー (.dll) ファイルのバージョン情報が一致する必要があります。 さらに、すべてのファイル バージョン情報が識別される、`[SignatureAttributes]`バイナリが一致する必要があります PETrust として .inf のセクション、。 inf します。 そのファイルのバージョン情報を一致するドライバー パッケージに追加のバイナリをお勧めします。 inf。

従来のオペレーティング システムの優勢のファイルのバージョン管理の要件と一致するファイルのバージョンの書式設定従う必要があります、 `AA.BB.CCCCC.DDDDD` where のパターンします。

* AA を .inf で表示されている最も対応のデバイスのドライバー モデルのバージョンを示します
* BB (WDDM 1.2 ドライバー以降)
    * .Inf で表示されている最も対応のデバイスの使用可能な D3D 機能の最高レベルを示します
* BB (WDDM 1.1 ドライバーおよび下)
    * .Inf で表示されている最も対応のデバイスでサポートされている使用可能な最高の DDI バージョンを示します
* としては、0 から 65535 までのベンダーによって選択された 5 桁の数字までの数
* DDDDD は最大で 0 から 65535 までのベンダーによって選択された 5 桁の数字の数

AA フィールドの値:

|ドライバー モデル |AA 値|
| --- | --- |
|WDDM v2.1 |21|
|WDDM v2.0 |20|
|WDDM v1.3 |10|
|WDDM v1.2 |9|
|WDDM v1.1|8|
|WDDM v1.0|7|
|XDDM|6|

BB フィールド (WDDM 1.2 以降) の値:

|DirectX の機能レベル|BB 値|
|---|---|
12_x|21
12_1|20
12_0|19
11_1|18
11_0|17
10_1|16
10_0|15
9_3|14
9_2|14
9_1|14

BB フィールド (WDDM 1.1 またはそれ以前) の値:

|DDI バージョン|BB 値
---|---
機能レベル 11_0 D3D11-DDI|17
D3D11-DDI 10 の機能レベル|16
D3D10-DDI|15
D3D9 DDI|14

#### <a name="examples"></a>例

> [!NOTE]
> 数値に先行するゼロを埋め込む必要はありません、つまり 123 を 00123 としてまたは DDDDD のフィールドとして表す必要はありません。 以前のバージョンの Windows OS では、最後の 2 つのフィールドは、4 桁、つまり CCCC をいました。DDDD します。 そのため、Windows 10 および WDDM 2.0 より前のバージョンのドライバーの例では、4 桁の数字のみがあります。

* Windows Vista WDDM 1.0:

    * D3D9 DDI ドライバー 7.14.0000.0000 に 7.14.9999.9999 を使用できます。
    * D3D10 DDI ドライバー 7.15.0000.0000 に 7.15.9999.9999 を使用できます。

* Windows 7 WDDM 1.1。

    * D3D9 DDI ドライバー 8.14.0000.0000 に 8.14.9999.9999 を使用できます。
    * D3D10 DDI ドライバー 8.15.0000.0000 に 8.15.9999.9999 を使用できます。
    * D3D11 DDI FL_10_0 ドライバーでは、8.16.0000.0000 に 8.16.9999.9999 を使用できます。
    * D3D11 DDI FL_11_0 ドライバーでは、8.17.0000.0000 に 8.17.9999.9999 を使用できます。

* Windows 8 WDDM 1.2。

    * FL_10_0 HW 9.15.0000.0000 に 9.15.9999.9999 を使用できます。
    * FL_10_1 HW 9.16.0000.0000 に 9.16.9999.9999 を使用できます。
    * FL_11_0 HW 9.17.0000.0000 に 9.17.9999.9999 を使用できます。
    * FL_11_1 HW 9.18.0000.0000 に 9.18.9999.9999 を使用できます。

* Windows 8.1 WDDM 1.3。

    * FL_10_0 HW 10.15.0000.0000 に 10.15.9999.9999 を使用できます。
    * FL_10_1 HW 10.16.0000.0000 に 10.16.9999.9999 を使用できます。
    * FL_11_0 HW 10.17.0000.0000 に 10.17.9999.9999 を使用できます。
    * FL_11_1 HW 10.18.0000.0000 に 10.18.9999.9999 を使用できます。

* Windows 10 WDDM 2.0。

    * FL_11_1 HW 20.18.0000.0000 に 20.18.65535.65535 を使用できます。
    * FL_12_0 HW 20.19.0000.0000 に 20.19.65535.65535 を使用できます。
    * FL_12_1 HW 20.20.0000.0000 に 20.20.65535.65535 を使用できます。

* Windows 10 WDDM 2.1。

    * FL_11_1 HW 20.18.0000.0000 に 21.18.65535.65535 を使用できます。
    * FL_12_0 HW 20.19.0000.0000 に 21.19.65535.65535 を使用できます。
    * FL_12_1 HW 20.20.0000.0000 に 21.20.65535.65535 を使用できます。


#### <a name="enforcement"></a>強制

HLK 証明再生リストの Windows 10 用の必須のテストをビルド 10586 が上記のルールを適用するよりも高くします。 テストは、古い OS バージョンでは省略可能になります。 Windows 10 ビルド 10586 後 WDDM バージョンは 2.1 に更新されました。 このファイルを表示することもできますが、必須の要件は、WDDM 2.1 以降に組み込まれているドライバーにのみ適用されます。