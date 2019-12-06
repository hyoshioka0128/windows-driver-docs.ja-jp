---
title: WDDM 2.1 の機能
description: このセクションでは、Windows Display Driver Model (WDDM) バージョン2.1 の新機能と強化された機能について詳しく説明します。
ms.assetid: 7dc0d0ad-98da-4bd6-bed9-f70525b682bc
ms.date: 01/10/2019
ms.localizationpriority: medium
ms.openlocfilehash: 4c579c6bfc9a3ded30a9212a828827b26adb3ef0
ms.sourcegitcommit: ba3199328ea5d80119eafc399dc989e11e7ae1d6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74862973"
---
# <a name="wddm-21-features"></a>WDDM 2.1 の機能


このトピックでは、windows Display Driver Model (WDDM) バージョン2.1 の新機能と強化された機能について詳しく説明します。このバージョンは、Windows 10 周年版から入手できます。

WDDM 2.1 自体は省略可能です。 実装されている場合は、必須およびオプションのドライバー機能のコレクションです。 これらの機能のいずれかをサポートするドライバーは、すべての必須の機能をサポートしている必要があります。  サポートは HLK テストで検証できますが、Dxgkrnl では、機能と DDIs の一貫性がチェックされます。

**WDDM 2.1 要件の表**

| 機能 | 適用条件 |
| --- | --- |
| オファーと回収の改善 | Mandatory |
| ビデオメモリの管理 | オプション |
| HW 保護されたコンテンツの信頼性の向上 | ハードウェアの選択 |
| Windows のサポートを使用したアプリケーションのサポート | Mandatory |
| 間接表示 | ハードウェアの選択 |
| ドライバーストアとサイドバイサイドインストール | Mandatory |
| カメラ/キャプチャシナリオ用の DirectX メモリ表面共有 | Mandatory|

WDDM 2.1 では、D3D9、D3D10、D3D 10.1、D3D11、D3D11、D3D12 の各 D3D バージョンがサポートされています。

## <a name="offer-and-reclaim-improvements"></a>オファーと回収の改善

新しい DDI の[PFND3DDDI_RECLAIMALLOCATIONS3CB](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_reclaimallocations3cb)が作成され、バックグラウンドモードで実行されるアプリケーションのメモリフットプリントが減少します。 このインターフェイスを使用すると、アプリケーションはバックグラウンドで完全にコミット解除できるリソースを提供できます。 その結果、プロセス有効期間マネージャーは、DirectX を使用するバックグラウンドアプリからより多くのメモリを再利用できるようになります。これにより、メモリ不足時にバックグラウンドアプリケーションの終了が少なくなります。

その他の DDI の変更:

* [PFND3DDDI_UPDATEALLOCATIONPROPERTYCB コールバック](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_updateallocationpropertycb)
* [PFND3DDDI_OFFERALLOCATIONS2CB コールバック](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_offerallocations2cb)
* [D3DDDICB_OFFERALLOCATIONS2 構造体](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-d3dddicb_offerallocations2)
* [D3DDDICB_RECLAIMALLOCATIONS3 構造体](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddicb_reclaimallocations3)

リソースの提供と再利用の詳細については、「[変更の提供と再利用](offer-and-reclaim-changes.md)」を参照してください。

## <a name="application-support-with-windows-gamedvr"></a>Windows のサポートを使用したアプリケーションのサポート

Windows 10 の記念版には、Windows ゲームバーとゲームの全画面ゲームでのゲームを利用する機能が強化されています。

WDDM 2.1 ドライバーは、"*現在のバッチ*処理" と呼ばれるパフォーマンス機能をサポートするために必要です。これにより、フリップモデルのスワップチェーンに対するマルチスレッドサポートが追加されます。 これは、ゲームバーを含む全画面ゲームが、以前のバージョンの Windows と同じパフォーマンスレベルで実行されることを保証するための重要な機能です。

この機能を有効にするために作成された新しい DDIs を次に示します。

* [PFND3DDDI_SYNCTOKENCB コールバック](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_synctokencb)
* [D3DDDIARG_SYNCTOKEN 構造体](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_synctoken)
* [PFND3DDDI_SYNCTOKEN コールバック](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_synctoken)


## <a name="indirect-display"></a>間接表示

WDDM 2.1 では、間接ディスプレイにより、USB 接続ディスプレイが、他のすべてのモニターと同じユーザーエクスペリエンスに参加できるようになります。 また、間接ディスプレイドライバーは、カーネルモードドライバーよりも簡単に開発できるユーザーモードドライバーであり、その結果、システム全体の信頼性が向上します。

WDDM 2.1 では、次の USB 表示機能/エクスペリエンスが有効になっています。

* USB ディスプレイを Windows プラットフォームに接続する場合、またはオペレーティングシステムをアップグレードする場合は、Windows update から適切なドライバーがダウンロードされ、インストールされます。

* モニターを USB ディスプレイハードウェアに接続すると、適切なモニタートポロジ、解決策、および DPI が検出され、設定されます。

* モニターの解像度と拡大/縮小はユーザーが変更できます。

* ユーザーは、予期しない副作用を生じることなく、USB ディスプレイを切断し、再接続することができます。

* モニタートポロジは、切断して、同じモニターに再接続することによって保持されます。

* USB は、スリープや休止状態などのさまざまな電源状態で、機能を適切に表示します。

間接表示の詳細については、「[間接ディスプレイドライバーモデルの概要](indirect-display-driver-model-overview.md)」を参照してください。

## <a name="driver-store-and-side-by-side-driver-installation"></a>ドライバーストアとサイドバイサイドドライバーのインストール

WDDM 2.1 では、*ドライバーストア*を使用したグラフィックスドライバーのインストールについて説明します。 グラフィックドライバーをインストールするこのメカニズムによって、Windows Update からのドライバーの更新の回復性が向上し、ドライバーファイルのバージョンの不一致が解消され、システムが不安定になり、ユーザーが開始した再起動が発生します。 その後の各ドライバーの更新は、ドライバーストア内の一意の場所 (つまり `System32\DriverStore\FileRepository\[…]`) から直接実行されるため、ドライバーファイルの上書きと不一致を回避できます。

ドライバーストアの機能を実装するには、ドライバーファイルが一意のドライバーリポジトリに確実にコピーされるように、グラフィックスドライバーの INF ファイルを変更する必要があります。 INF の変更については、このドキュメントの「 [inf の要件](#graphics-inf-requirements)」セクションで詳しく説明されています。

## <a name="dxil"></a>DXIL

WDDM 2.1 では、GPU シェーダーコンパイラスタックを DirectX バイトコード (DXBC) から DirectX 中間言語 (DXBC) に移行することが導入されました。これは、GPU 命令を GPU に送信するための新しい形式です。 DXIL への移行では、開発者に次の利点が提供されます。

* プログラミングの容易さが向上し、開発者が理解している GPU プログラミング構文と CPU 言語の違いを最小限に抑えることで、開発者にとってシェーダー作成プロセスの複雑さが軽減されます。

* 高パフォーマンスコンパイラ: 

    * パフォーマンスの向上を実現するために、*ランタイムシェーダーのパフォーマンス*が有効になっています。 
    * DXIL は、Gpu の SIMD プロセッサのレーン間でデータを共有できるようにする、組み込みの新しいセットを提供します。

* ワークフローの柔軟性-DXIL を使用すると、開発者は独自のカスタムツールと最適化パスを制御し、ビルド時と実行時に適用されるコンパイルステップを選択できます。

* 高度な言語機能-進化した言語では、GPU コードと CPU コードの違いをなくし、GPU プログラマの学習曲線を平坦化する主な機能が提供されます。

開発者にとっての利点に重点を置いたこれらの機能により、エンドユーザーは、既存のハードウェアで実行した場合でも、新規または更新されたゲームのパフォーマンスが向上するというメリットを得ることができます。

## <a name="directx-memory-surface-sharing-for-cameracapture-scenarios"></a>カメラ/キャプチャシナリオ用の DirectX メモリ表面共有

WDDM 2.1 では、複数のプロセスで同時にカメラまたはキャプチャデバイスを共有するためにフレームサーバーコンポーネントが導入されました。 これにより、複数のアプリケーションが複数回のプロセス間でイメージデータをコピーするのではなく、複数のアプリケーションから読み取ることができる1つのメモリ位置に、キャプチャされたフレームを保存できます。 この機能を使用すると、複数のプロセス間でのキャプチャされた画像の効率的な管理、省電力、帯域幅の削減、および WDDM 2.1 準拠のハードウェアとドライバーの待機時間の削減を実現し、アプリケーションとユーザーのパフォーマンスが向上します。

フレームサーバーは、キャプチャされたイメージをプロセス間で共有可能なメモリとして割り当て、アクセスを要求するプロセスにこのメモリを共有します。 フレームサーバーはテクスチャを複数のクライアントプロセスにブロードキャストするため、テクスチャは同時読み取りをサポートする必要があることに注意してください。 現在、この目的では NV12 テクスチャがサポートされています。

## <a name="pipeline-state-object-pso-caching-and-library"></a>パイプライン状態オブジェクト (PSO) のキャッシュとライブラリ

D3D12 で導入された、パイプライン状態オブジェクト (PSO) は、グラフィックスパイプライン命令とリソース (状態) を統合オブジェクトとして表すインターフェイスであり、状態の D3D とドライバー decompositions の不一致を軽減します。 グラフィカルに要求の厳しいアプリケーションやゲームを実行するには、膨大な数の Pso を作成する必要があります。 

WDDM 2.1 PSO ライブラリとキャッシュを使用すると、ゲームアプリケーションは、最初の実行時に作成された後、物理ストレージに PSO を格納できます。 これにより、後のインスタンスで事前に作成された Pso をライブラリから取得できるため、PSO 抽出時間が短縮されます。 たとえば、ゲームを初めて実行したとき、または PC を再起動した後、コンテンツは保存された Pso として物理ライブラリから読み込まれます。


## <a name="start-of-pipeline-gpu-timestamps"></a>パイプライン GPU のタイムスタンプの開始

WDDM 2.1 では、GPU パイプラインでグラフィックスイベントのタイムスタンプの開始を取得する機能が導入されました。 この新機能は、パイプラインのタイムスタンプの末尾と組み合わせて使用されるもので、開発者は、GPU で発生するアプリケーションのアクティビティの並列化、パイプライン処理、およびタイミングを明確かつ詳細に視覚化できます。 各イベントの実行時間によって、開発者はコードをさらに最適化し、非効率性やその他のパフォーマンスの問題を調査できます。

この機能により、"リアルタイムで低オーバーヘッド" GPU パフォーマンスデータ収集が可能になり、同時に、Gpu 上のワークロードを視覚化して測定するための十分な情報が得られます。 この機能の目的は、GPU によって実行される操作の正確な順序と期間を再構築するための十分な情報を提供することです。これにより、ツールがエンジンとの並列化とパイプライン処理を視覚化したり、GPU ワークロードを測定したり、可能性を特定したりできるようになります。同期の問題。

## <a name="viewing-gpu-microcode"></a>GPU マイクロコードの表示

WDDM 2.1 を使用すると、開発者は GPU マイクロコードを表示して、シェーダーをさらに最適化できます。 開発者は HLSL でシェーダーを作成することによってグラフィックスパイプラインをプログラミングします。これは、GPU ドライバーの中間言語にコンパイルされます。 ドライバーは、追加のコンパイルと最適化を実行して、このコードを、開発者に対して不透明な GPU 固有の命令に変換します。 この機能により、開発者には、シェーダーの最適化と速度の範囲を評価するための読み取り可能な GPU 固有のコードが表示されます。

この機能によって、UMD は、グラフィックスパイプラインの各プログラム可能なステージ ( シェーダー) を使用すると、これらのシェーダーの使用や誤用に関する実用的な情報を返すことができます。 GPU 固有のマイクロコードは逆アセンブルされ、UMD コメントと共に読み取り可能な文字列形式で表示されます。 開発者は、読み取ることができる GPU コードの HLSL コードマッピングをサイドバイサイドで表示できます。これにより、コードを動的に変更し、GPU コード側でコンパイラの最適化の結果を確認できます。

## <a name="determining-wddm-version"></a>WDDM バージョンの確認

### <a name="wddm-21-caps"></a>WDDM 2.1 キャップ

ドライバーは、新しいバージョン定数を使用して[DXGK_DRIVERCAPS:: WDDMVersion](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_drivercaps)で WDDM 2.1 サポートを報告します。

`DXGK_WDDMVERSION::DXGKDDI_WDDMv2_1 = 0x2100`

Dxgkrnl は、サポートされている新しい機能を判別する手段として**Wddmversion** cap を使用しません。そのタスクは他の cap または DDI の有無に対して残されます。 ただし、ドライバーが**Wddmversion** cap を通じて wddm 2.1 サポートを報告する場合、dxgkrnl は、wddm 2.1 で必要とされるキャップまたは DDIs が存在することを検証し、アダプターがない場合はアダプターを作成できません。 キャップが矛盾すると、アダプターまたはセグメントの作成に失敗します。

> [!NOTE]
> アプリケーション、既存またはそれ以降のバージョンでは、ドライバーモデルを照会して、ここで説明するようなプラットフォームの機能強化によって有効になっている Windows 10 記念版の機能を利用する必要はありません。 機能の変更は、それぞれのランタイムを通じて公開する必要があります。

KMT_DRIVERVERSION_WDDM_2_1 に一致するように新しい定数が追加されました。

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

KMD の DDI インターフェイスのバージョンは次のとおりです。 

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

Wddm 2.1 グラフィックスドライバーには、WDDM 2.0 以前のドライバーと比較した場合とは異なる INF 要件があります。 それらを次に示します。

1. WDDM 2.1 では、WDDM 2.0 グラフィックスドライバー (D1) と同一の特徴スコアを持っている必要があります。

2. WDDM 2.1 グラフィックスドライバーでは、別の OS INF インストールセクションを使用する必要があります。

3. "ドライバーストア" インストールの WDDM 2.1 グラフィックスドライバー INF の変更。

詳細については、「 [INF ファイルのセクションとディレクティブ](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)」を参照してください。

ドライバーファイル32と64ビットは、に残り、ドライバーストアから読み込まれます。 WoW64 ファイルシステムのリダイレクトは、ドライバーストアには適用されません。 Ihv は、標準的な INF 構文を使用してサブフォルダーを指定し、たとえば、必要に応じて一意のドライバーストアフォルダーの下に WoW64 フォルダーを作成することができます。

次に、ドライバーストアからの実行をサポートする INF が以前の動作とどのように異なるかを示します。

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

サブフォルダーを指定するには、次の例に示すように、ドライバーで構文を使用することができます。

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

グラフィックスアダプターまたはチップセットのドライバー DLL および SYS ファイルには、適切にフォーマットされたファイルバージョンが必要です。

ドライバー情報ファイル (.inf)、カーネルモードドライバー (.sys)、およびユーザーモードドライバー (.dll) ファイルのバージョン情報が一致している必要があります。 また、.inf の `[SignatureAttributes]` セクションで指定されているすべてのファイルのバージョン情報は、.inf と一致している必要があります。 ドライバーパッケージ内の追加バイナリのファイルバージョン情報は、.inf と一致することをお勧めします。

レガシオペレーティングシステムのファイルバージョン管理の優先要件と一致させるには、ファイルのバージョンの書式設定が、次のような `AA.BB.CCCCC.DDDDD` パターンに従う必要があります。

* AA は、.inf に記載されている最も機能の高いデバイスのドライバーモデルバージョンを示します。
* BB (WDDM 1.2 ドライバー以上の場合)
    * .Inf に一覧表示されている最も使用可能なデバイスの最大の D3D 機能レベルを示します。
* BB (WDDM 1.1 ドライバーおよびそれ以降)
    * .Inf に記載されている最も機能の高いデバイスでサポートされている、使用可能な最大の DDI バージョンを示します。
* CCCCC は、ベンダーによって選択された 0 ~ 65535 の最大5桁の数字です。
* DDDDD は、ベンダーによって選択された 0 ~ 65535 の最大5桁の数字です

AA フィールドの値:

|ドライバーモデル |AA 値|
| --- | --- |
|WDDM version 2.1 |21|
|WDDM バージョン2.0 |20|
|WDDM (1.3) |10|
|WDDM version 1.2 |9|
|WDDM v1.1|8|
|WDDM v1.0|7|
|XDDM|6|

BB フィールドの値 (WDDM 1.2 以降):

|DirectX の機能レベル|BB 値|
|---|---|
12_x|21
12_1|20
120|19
11_1|18
110|17
10_1|16
100 (_s)|15
93|14
9_2|14
9_1|14

BB フィールドの値 (WDDM 1.1 以前):

|DDI バージョン|BB 値
---|---
D3D11 機能レベル110|17
機能レベル10の D3D11-DDI|16
D3D10-DDI|15
D3D9 DDI|14

#### <a name="examples"></a>例

> [!NOTE]
> 数値に先行ゼロを埋め込む必要はありません。つまり、123を CCCCC フィールドまたは DDDDD フィールドに対して00123として表す必要はありません。 以前のバージョンの Windows OS では、最後の2つのフィールドは、CCCC の4桁でした。DDDD. そのため、Windows 10 および WDDM 2.0 より前のドライバーバージョンの例では、4桁しか使用できません。

* Windows Vista WDDM 1.0:

    * D3D9 DDI ドライバーは7.14.0000.0000 を使用できます。
    * D3D10 DDI ドライバーは7.15.0000.0000 を使用できます。

* Windows 7 WDDM 1.1:

    * D3D9 DDI ドライバーは8.14.0000.0000 を使用できます。
    * D3D10 DDI ドライバーは8.15.0000.0000 を使用できます。
    * FL_10_0 ドライバーを使用した D3D11 DDI では、8.16.0000.0000 を8.16.9999.9999 に使用できます。
    * FL_11_0 ドライバーを使用した D3D11 DDI では、8.17.0000.0000 を8.17.9999.9999 に使用できます。

* Windows 8 WDDM 1.2:

    * FL_10_0 HW では、9.15.0000.0000 を9.15.9999.9999 に使用できます。
    * FL_10_1 HW では、9.16.0000.0000 を9.16.9999.9999 に使用できます。
    * FL_11_0 HW では、9.17.0000.0000 を9.17.9999.9999 に使用できます。
    * FL_11_1 HW では、9.18.0000.0000 を9.18.9999.9999 に使用できます。

* Windows 8.1 WDDM 1.3:

    * FL_10_0 HW では、10.15.0000.0000 を10.15.9999.9999 に使用できます。
    * FL_10_1 HW では、10.16.0000.0000 を10.16.9999.9999 に使用できます。
    * FL_11_0 HW では、10.17.0000.0000 を10.17.9999.9999 に使用できます。
    * FL_11_1 HW では、10.18.0000.0000 を10.18.9999.9999 に使用できます。

* Windows 10 WDDM 2.0:

    * FL_11_1 HW では、20.18.0000.0000 を20.18.65535.65535 に使用できます。
    * FL_12_0 HW では、20.19.0000.0000 を20.19.65535.65535 に使用できます。
    * FL_12_1 HW では、20.20.0000.0000 を20.20.65535.65535 に使用できます。

* Windows 10 WDDM 2.1:

    * FL_11_1 HW では、20.18.0000.0000 を21.18.65535.65535 に使用できます。
    * FL_12_0 HW では、20.19.0000.0000 を21.19.65535.65535 に使用できます。
    * FL_12_1 HW では、20.20.0000.0000 を21.20.65535.65535 に使用できます。


#### <a name="enforcement"></a>強制

10586より高い Windows 10 ビルドの HLK 証明書再生リストの必須テストでは、上記の規則が適用されます。 以前のバージョンの OS では、テストは省略可能です。 10586より後の Windows 10 ビルドでは、WDDM バージョンが2.1 に更新されました。 これを確認するもう1つの方法として、必須要件は WDDM 2.1 以上用にビルドされたドライバーにのみ適用されます。