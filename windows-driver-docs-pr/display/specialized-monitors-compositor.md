---
title: HMD と特殊なモニター用のカスタム Compositor アプリの構築
description: HMD と特殊なモニター用のカスタム Compositor アプリの構築
keywords:
- デバイスの WDK を表示する
- ドライバーの監視 WDK
- ドライバーの表示 WDK、ドライバーの監視
- monitors
- HMD
- 仮想現実
ms.author: windowsdriverdev
ms.date: 7/8/2020
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
ms.openlocfilehash: 2bc9410394c29501a528a1cfdeb78fad4be52154
ms.sourcegitcommit: f788aa204a3923f9023d8690488459a4d9bc2495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86141239"
---
# <a name="building-a-custom-compositor-app-for-hmds-and-specialized-monitors"></a>HMD と特殊なモニター用のカスタム Compositor アプリの構築

コンポジター [API](https://docs.microsoft.com/uwp/api/windows.devices.display.core)は、サードパーティ製の api であり、他のすべてのパブリック api の下に配置され、windows でのディスプレイアダプターの列挙、構成、および表示に使用される、低レベルの WinRT api です。 これは、GPU 上の3D エンジンやメディアエンジンと同様に、表示コントローラーを別の "エンジン" として扱うことです。 この API の役割は次のとおりです。

* ディスプレイハードウェアに関するクエリへの応答 (機能や使用可能な表示モードなど)
* 現在の構成に関するクエリへの応答
* ディスプレイハードウェア (表示モードなど) のプロパティの設定
* ディスプレイハードウェア (接続されたモニターの解像度、ワイヤ形式など) の構成
* "プライマリ" と呼ばれる特殊な GPU サーフェスの割り当てとスキャン
* Direct3D と Windows... Core Api の間の相互運用を許可する (例: サーフェイスの共有、フェンス)

次のようなものを呼び出すことはでき**ません**。

* アプリがウィンドウにコンテンツを表示するために使用する API ではありません。 アプリでは、引き続き DXGI、XAML、DirectComposition、GDI などを使用します。
* コンテンツを全画面表示するためにゲームで使用される API ではありません。 アプリアプリでは引き続き DXGI を使用します。 Win32 アプリでは引き続き Hwnd を使用し、UWP アプリは常に CoreWindow でコンテンツを表示します。

この API は、専用のハードウェアを運転するコンポジターアプリ用です。

![API アーキテクチャレイヤー](images/specialized-displays-layers.png)


## <a name="scenarios-for-building-custom-compositors"></a>カスタムコンポジターを構築するシナリオ

Windows... Core Api は、次のシナリオで使用するのに適しています。
* 仮想および拡張された現実の表示では、独自のコンポジターを必要として、ディスプレイコントローラーを直接駆動し、Windows デスクトップとは別のタイミングとモードの構成をきめ細かく制御できます。
* 特化されたディスプレイハードウェアシナリオで、商用設定の表示に対する専用の制御が必要です。 たとえば、ハードウェアのワープによって、このようなディスプレイで Windows デスクトップが正しくレンダリングされない場合は、グレースケールが表示されます。
* 特定の "アプライアンス" シナリオ。 Windows デスクトップエクスペリエンスを長時間にわたって干渉することなく、アプリ専用のモニターを使用できます (専用のビデオモニターなど)。

API は次の方法でこれを実現します。
* ワイヤ形式や HDR など、全画面表示モード情報をきめ細かく制御できます。
* フェンスを使用してプレゼンテーションを同期させることで、コンポジターはプロセスやサブコンポーネント間でプレゼンテーションをチェーン化し、パフォーマンスのオーバーヘッドをほぼゼロにすることができます。
* 基になるビデオの現在のネットワーク (VidPN) に対してクエリや構成を行う機能を向上させることにより、システムコンポーネントと低レベルの合成コンポーネントの両方でより複雑な操作を実行できるようになります。

この API は、特殊なハードウェアを使用したサードパーティのユースケースの*ごく*一部に対してのみ使用されます。 その使用は、この API の機能が必要であることを宣言するハードウェアに対して非常に制限されています。 そのため、開発者はハードウェアの概念を理解している程度の知識があれば、問題を解決するために Microsoft に直接問い合わせる必要があります。

## <a name="hardware-requirements"></a>ハードウェア要件

サードパーティのカスタムコンポジターは、HMDs または "特殊化された" 表示として事前に指定されているディスプレイのみを取得できます。 この指定は、次の2つの方法のいずれかで指定する必要があります。
* **EDID 拡張機能**-Hmds、X レイモニター、ビデオ壁面、またはその他の特殊なシナリオとして永続的に使用するように設計されたカスタムディスプレイデバイスでは、 [Hmds 用の Microsoft EDID 拡張機能と特殊な表示](specialized-monitors-edid-extension.md)を実装する必要があります。
* **ユーザー**による上書き-既製のモニターを使用したカスタムハードウェアインストールの場合、Windows には、モニターを "特殊化" として指定するための UI の切り替えが用意されています。

ソフトウェアの EDID を上書きすることによって、表示を HMDs または特殊化された表示として指定することはでき**ません**。

## <a name="roadmap-for-implementing-a-custom-compositor"></a>カスタムコンポジターを実装するためのロードマップ

カスタムコンポジターの実装は、いくつかの段階に分けることができます。

1. 関連する HMDs または特殊化された表示を列挙して検出する
2. 選択した表示の所有権を取得する
2. 選択したすべての表示のモードを構成する
4. ディスプレイにフレームを表示するためのリソースを作成する
5. コンテンツをレンダリングし、フレームのプレゼンテーションをスケジュールする

## <a name="comparison-of-display-related-apis"></a>表示関連 Api の比較

| API | 目的と対象ユーザー |
|-----|-----------------------------|
| `Windows.Graphics.Display.DisplayInformation` | CoreWindow のレンダリングプロパティとレイアウトプロパティを取得するために使用します。 |
| `Windows.Graphics.Display.Core.HdmiDisplayInformation` | 制約されたモードのセットを列挙して設定するための Xbox 専用 API です。 Xbox メディアアプリのシナリオに特化しています。 |
| `Windows.Devices.Display.DisplayMonitor` | 物理モニターデバイスのプロパティを照会するために使用されます。 では、モニターの構成方法や OS による現在の使用方法に関するランタイム情報は公開されません。 |
| `EnumDisplayDevices`, `EnumDisplayMonitors`, `EnumDisplaySettings` | HMONITORs、GDI デバイス、および物理モニターのマッピングに対してクエリを実行するための従来の Win32 Api。 ここで返される情報は、高度に仮想化され、アプリケーションの互換性のために維持されます。 |
| Direct3D | Gpu サーフェイスにピクセルコンテンツをレンダリングし、GPU で計算を実行するために使用されます。 |
| DXGI スワップチェーン | ウィンドウ表示および "縁なしウィンドウ表示" プレゼンテーションで使用されます。 アプリケーションスワップチェーンのコンテンツフローは、システムコンポジター、DWM を経由します。 |
| DXGI 出力列挙型 | HMONITORs には、DXGI ラッパーが用意されています。 |
| `QueryDisplayConfig`, `SetDisplayConfig`, `DisplayConfigGetDeviceInfo`, `DisplayConfigSetDeviceInfo` | ディスプレイトポロジを構成するための Win32 Api。 では、複数のモードを列挙するメカニズムはありませんが、現在の構成と設定に関する豊富な情報が用意されています。 ただし、モードのすべての新しいプロパティがこれらの Api によって公開されるわけではありません。 |
| `Windows.Devices.Display.Core`**(このドキュメント)** | ターゲットの列挙、モードの列挙、モードの構成、プレゼンテーション用の GPU サーフェイスの割り当て、および表示するコンテンツの提示に使用されます。 |

## <a name="display-configuration-overview"></a>構成の概要の表示

### <a name="physical-hardware-enumeration"></a>物理ハードウェアの列挙

Windows... Core API には、物理ハードウェアオブジェクトを表すためのさまざまなオブジェクトがあります。 は、 `DisplayAdapter` 通常、PCI Express に接続された gpu や CPU 上の統合 gpu などの物理ハードウェアデバイスです。 DisplayTargets は、GPU から接続できる物理コネクタ (たとえば、HDMI、VGA、DisplayPort など) を表します。 これには、内部モニター (ラップトップ、タブレットなど) を搭載したデバイスに対して、ユーザーに表示されない内部接続が含まれる場合があります。 ユーザーが一度に物理的に接続できるよりも、ソフトウェアで表現されている DisplayTargets が多くなる可能性があります。 たとえば、DisplayPort 接続の標準ではデイジーチェーンが許可されるため、GPU ドライバーは通常、チェーンされたモニターを考慮するために、物理ポートごとに複数の DisplayPort ターゲットを列挙します。

![ハードウェアトポロジの図](images/specialized-displays-hardware.png)

### <a name="objects-for-setting-modes"></a>モードを設定するためのオブジェクト

DisplayTargets を列挙するためのモードなどの設定とクエリを実行するために、DisplayTargets を DisplayPaths で表現します。 複製グループは DisplayViews によって表され、Displayviews に集計されます。 そのため、1つの DisplayState オブジェクトは、複数のモニターのドライバーに送信できるモード状態の完全なセットを表すことができます。

![モードトポロジの図](images/specialized-displays-state-objects.png)

### <a name="atomic-state-for-mode-configuration-and-enumeration"></a>モードの構成と列挙のアトミック状態

コンポジター API は、さまざまなシステム表示状態へのアクセスを、明確に定義された "staleness" 動作で確実に取得できるように設計されています。 これが重要なのは、Gpu は共有リソースであり、非常に厳しい帯域幅と電源の制約があるためです。 最新のシステムでは、デバイスはいつでも到着または停止できます。また、使用可能な表示モード (ドッキング/ドッキング解除、スリープ状態、別のパス上の別のコンポーネントの変更モードなど) の一覧に影響を与える可能性があります。 したがって、コンポジターは、Windows. Core API を使用してシステム構成の変更に対して回復性を備え、状態を構成するために推奨されるパターンに従うことが重要です。

このため、Windows では、データベースと同様に、単純なトランザクションの読み取り/変更コミットモデルが提供されます。 クライアントは、システム内の表示デバイスの DisplayState オブジェクトをアトミックに読み取ることができます。 すべてのオブジェクトは変更不可であるか、またはシステムへの状態を更新/コミットするための適切に定義された Api を提供します。 DisplayState が行われるまで変更は行われません。 TryApply が呼び出され、システムへの変更が "コミット" されます。 DisplayState に対する変更のコミット/適用は、影響を与えずに失敗するか、適用された完全な変更に成功します。

API の原子性機能を利用するには、次のようにします。

* 再試行**可能な**ループで、任意のモード構成ロジックを記述します。
* 各ループ内のモード構成の開始時に新しい DisplayState**を作成し**ます。
* DisplayState を呼び出すとき**は、フラグを使用** [`FailIfStateChanged`](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaystateapplyoptions) します。 tryapply を使用して、システム状態が displaystate が作成されたときと同じではなくなったことを検出します。 これにより、操作を再試行することができます。 操作がで失敗した場合は `SystemStateChanged` 、ループ全体を再試行します。
* 同じ原子性が保証されない可能性があるため、状態の読み取りまたは変更を行う他の Api (DXGI、GDI など) を、Windows の Api を使用し**て混在させないで**ください。

```C++
#include <winrt\Windows.Devices.Display.Core.h>
using namespace winrt::Windows::Devices::Display::Core;
...

// Create a DisplayManager
DisplayManager manager = DisplayManager::Create(DisplayManagerOptions::EnforceSourceOwnership);

// Loop around trying to acquire a target and set a mode
bool shouldRetry;
do
{
    shouldRetry = false;

    // ... Find the target that you want to use
    auto targets = manager.GetCurrentTargets();
    DisplayTarget selectedTarget = ...;

    auto stateCreationResult = manager.TryAcquireTargetsAndCreateEmptyState(
        winrt::single_threaded_vector<DisplayTarget>({ selectedTarget }));

    if (stateCreationResult.ErrorCode() != DisplayManagerResult::Success)
    {
        winrt::check_hresult(stateCreationResult.ExtendedErrorCode());
    }

    auto state = stateCreationResult.State();
    DisplayPath newPath = state.ConnectTarget(selectedTarget);

    // ... Configure the path

    auto applyResult = state.TryApply(DisplayStateApplyOptions::FailIfStateChanged);

    if (applyResult.Status() == DisplayStateOperationStatus::SystemStateChanged)
    {
        shouldRetry = true;
    }
    else if (applyResult.Status() != DisplayStateOperationStatus::Success)
    {
        winrt::check_hresult(applyResult.ExtendedErrorCode());
    }

} while (shouldRetry);
```

次の Api は、システムからアトミックに状態を読み取ります。

* **DisplayManager**
    * [GetCurrentTargets](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaymanager.getcurrenttargets)
    * [GetCurrentAdapters](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaymanager.getcurrentadapters)
    * [Tryreadcurrentstateforalltargets](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaymanager.tryreadcurrentstateforalltargets) /[TryAcquireTargetsAndReadCurrentState](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaymanager.tryacquiretargetsandreadcurrentstate)
* **DisplayState**
    * [IsStale](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaystate.isstale)
    * [TryFunctionalize](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaystate.tryfunctionalize)
* **DisplayPath**
    * [FindAllModes](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaypath.findmodes)
* **DisplayTarget**
    * [DisplayTarget.IsStale](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaytarget.isstale)

次の Api は、状態をシステムにコミットします。

* **DisplayManager**
    * [TryAcquireTarget](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaymanager.tryacquiretarget) /[ReleaseTarget](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaymanager.releasetarget) (およびメソッドを使用したターゲット `TryAcquireTargetsAnd*` の取得) –システムから displaytargets の所有権を取得します。
* **DisplayState**
    * [Tryapply](https://docs.microsoft.com/uwp/api/windows.devices.display.core.displaystate.tryapply) –ディスプレイドライバーを使用して、システム内のすべての所有対象ターゲットのモードを設定またはクリアして、現在のシステムの表示状態を更新します。

## <a name="known-limitations"></a>既知の制限事項

Windows... Core API には、いくつかの既知の制限があります (Windows 10 バージョン2004以降)。

* 現在、間接ディスプレイドライバー (Miracast、USB ディスプレイアダプター、ソフトウェアドライバーなど) に対応することはできません。 `DisplayManager.CreateDisplayDevice`間接ディスプレイアダプターが渡されると、は失敗します。

## <a name="sample-code"></a>サンプル コード

サンプルアプリケーションについては、「 [Windows. デバイス. Core カスタムコンポジターサンプル](https://github.com/microsoft/Windows-classic-samples/tree/master/Samples/DisplayCoreCustomCompositor)」を参照してください。