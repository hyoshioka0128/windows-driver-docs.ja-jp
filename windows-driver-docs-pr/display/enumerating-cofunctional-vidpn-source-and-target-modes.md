---
title: Cofunctional VidPN ソースおよびターゲット モードの列挙
description: Cofunctional VidPN ソースおよびターゲット モードの列挙
ms.assetid: f1aa6277-7af6-4ba0-8ff1-d562f7029540
keywords:
- ビデオの現在のネットワーク WDK ディスプレイ、列挙ターゲットモードとソースモード
- VidPN WDK ディスプレイ、列挙ターゲットモードとソースモード
- VidPN WDK の制約
- ターゲットモードとソースモードの列挙 WDK ビデオの現在のネットワーク
- ソースモード WDK ビデオの現在のネットワーク
- ターゲットモード WDK ビデオの現在のネットワーク
- 固定スケーリング変換 WDK ビデオの現在のネットワーク
- 固定回転変換 WDK ビデオの現在のネットワーク
- マルチサンプリング方法 WDK ビデオの現在のネットワーク
- モードは、WDK ビデオの現在のネットワークを設定します
- 制約のある VidPN WDK を検査しています
- スケーリングサポートフラグ WDK ビデオの現在のネットワーク
- ローテーションサポートフラグ WDK ビデオの現在のネットワーク
- 列挙ピボット WDK ビデオの現在のネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1de28fc19878e8ebd114fb34cbbd976c2a711b5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839705"
---
# <a name="enumerating-cofunctional-vidpn-source-and-target-modes"></a>Cofunctional VidPN ソースおよびターゲット モードの列挙


このトピックでは、video present network (VidPN) マネージャーと表示ミニポートドライバーが連携して、ビデオの現在のソースとターゲットで使用可能なモードを列挙する方法について説明します。 この資料を読む前に、次のトピックで説明されている内容について理解しておく必要があります。

-   [ビデオの現在のネットワークの概要](introduction-to-video-present-networks.md)

-   [VidPN オブジェクトとインターフェイス](vidpn-objects-and-interfaces.md)

場合によっては、VidPN マネージャーがディスプレイミニポートドライバーに対して、ディスプレイアダプターのビデオに表示されるソースとターゲットで使用可能なモードを列挙するように要求します。 通常、要求には次のパターンがあります。

1.  VidPN マネージャーは、ソースとターゲットの一部ではなく一部にピン留めされたモードを持つ VidPN を作成または取得します。

2.  VidPN マネージャーは、 [**DxgkDdiIsSupportedVidPn**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_issupportedvidpn)を呼び出して、表示アダプターでサポートされている機能的な vidpn を形成するために、vidpn を拡張できるかどうかを判断します。 つまり、既存の固定モードを変更せずに、残りのソースとターゲットに対してモードを固定できるかどうかを確認します。

3.  VidPN マネージャーは、 [**DxgkDdiEnumVidPnCofuncModality**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)を呼び出して、まだピン留めされたモードがないソースとターゲットで使用できるモードを取得します。

*DxgkDdiEnumVidPnCofuncModality*に渡される引数の1つは、制約を持つ vidpn と呼ばれる vidpn オブジェクトへのハンドルです。

*DxgkDdiEnumVidPnCofuncModality*は次の操作を行う必要があります。

-   制約のある VidPN を調べます。

-   固定モードが設定されていない各ソースとターゲットについて、制約と連携する最大のモードセットになるようにモードを調整します。

-   固定スケーリング変換が設定されていない各パスに対して、スケーリングのサポートフラグを調整して、制約と連携するようにします。

-   固定された回転変換がない各パスに対して、回転のサポートフラグを調整して、制約と連携するようにします。

-   ピン留めされたモードのソースごとに、そのソースで使用可能なマルチサンプリングメソッドを報告します。

次の段落では、前の箇条書きリストの各タスクを実行する方法の詳細について説明します。

### <a name="span-idinspecting_the_constraining_vidpnspanspan-idinspecting_the_constraining_vidpnspaninspecting-the-constraining-vidpn"></a><span id="inspecting_the_constraining_vidpn"></span><span id="INSPECTING_THE_CONSTRAINING_VIDPN"></span>制約のある VidPN を検査しています

制約のある VidPN の次のプロパティは、 *DxgkDdiEnumVidPnCofuncModality*が受け入れる必要がある制約です。

-   トポロジ (ソースとターゲットの間の関連付けのセット)

-   固定モード

-   各パスのスケーリング、スケーリングのサポート、回転、回転のサポート

-   各パスの目標の色

-   各パスのターゲットの色係数の動的な範囲

-   各パスのコンテンツの種類 (グラフィックスまたはビデオ)

-   各パスのガンマランプ

制約された VidPN から制約を抽出するには、次の手順を実行します。

-   まず、 [**Pfngettopology**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_gettopology)関数を呼び出して、制約のある vidpn のトポロジを表す、 [vidpn トポロジインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface)へのポインターを取得します。

-   [**PfnAcquireFirstPathInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpntopology_acquirefirstpathinfo)関数と[**pfnAcquireNextPathInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpntopology_acquirenextpathinfo)関数を呼び出して、制約された VidPN のトポロジ内の各パスに関する情報を取得します。 特定のパス (ソース ID、ターゲット ID、スケーリング変換、回転変換、ターゲット色など) に関する情報は、 [**D3DKMDT\_VIDPN\_存在\_パス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path)構造に含まれています。

-   パスごとに、パスのソース ID を[**pfnAcquireSourceModeSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_acquiresourcemodeset)関数に渡して、パスのソースを取得します。

-   [**PfnAcquirePinnedModeInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_acquirepinnedmodeinfo)関数を呼び出して、ソースのモードセットに固定されているモード (存在する場合) を確認します。 ソースのモードセットに固定モードが設定されている場合、セット内の残りのモードを調べる必要がない可能性があります。 モードセットに固定モードが設定されていない場合は、 [**pfnAcquireFirstModeInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_acquirefirstmodeinfo)と[**pfnAcquireNextModeInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_acquirenextmodeinfo)を呼び出して、セット内の残りのモードを確認します。

    同様の手順を使用して、ターゲットモードセットを確認し、固定モードに設定されているターゲットモードを判別します。

### <a name="span-idadjusting_mode_setsspanspan-idadjusting_mode_setsspanadjusting-mode-sets"></a><span id="adjusting_mode_sets"></span><span id="ADJUSTING_MODE_SETS"></span>モードセットの調整

制約付きの VidPN のトポロジでソースとターゲットに関連付けられているモードセットを検査する際には、固定モードに設定されているモードを確認してください。 モードセットに固定モードが指定されていない場合は、調整する必要があるかどうかを判断します。 制約に準拠していないモードが含まれている場合、または制約と連携する使用可能なモードが不足している場合は、モードセットを調整する必要があります。

モニターが接続されているビデオの現在のターゲットについては、モニターでサポートされているモードのセットも考慮する必要があります。 ディスプレイアダプター上のビデオの存在するターゲットが特定のモード (制約を指定) をサポートしている場合でも、接続されているモニターがモードもサポートしている場合は、ターゲットのモードでそのモードのみを一覧表示する必要があります。 接続モニターでサポートされているモードを確認するには、次の手順を実行します。

-   [DXGK\_MONITOR インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_monitor_interface)

    [**PfnAcquireMonitorSourceModeSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_monitor_acquiremonitorsourcemodeset)を呼び出します。 モードセットが調整を必要としない場合は、そのままにすることができます。 モードセットを調整する必要がある場合は、新しいモードセットを作成し、既存のモードセットを新しいモードに置き換える必要があります。

-   [DXGK_VIDPN_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface)

    新しいソースモードセットを作成して設定するには、 [**pfnCreateNewSourceModeSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_createnewsourcemodeset)を呼び出します。

-   [_DXGK_VIDPNSOURCEMODESET_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpnsourcemodeset_interface)

    次に、 [**pfnCreateNewModeInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_createnewmodeinfo)と[**Pfnaddmode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_addmode)を呼び出します。

-   [DXGK_VIDPN_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface)

    最後に、 [**Pfn割り当て Sourcemodeset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_assignsourcemodeset)を呼び出して、既存のソースモードセットを新しいものに置き換えます。

### <a name="adjusting-scaling-support-flags"></a>スケーリングのサポートフラグの調整

制約を行う VidPN のトポロジ内の各パスに対して、パスに固定されたスケーリング変換があるかどうかを確認します。 この判断を行うには、 *Vpnpath*を検査します。**Contenttransformation。このスケーリング**では、 *Vpnpath*は[**D3DKMDT\_VIDPN\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path) 、パスを表す\_パス構造を提供します。 *Vpnpath*の場合。**Contenttransformation。スケーリング**は、 **D3DKMDT\_VPPS\_IDENTITY**、 **D3DKMDT\_vpps\_中央揃え**、または**D3DKMDT\_vpps\_stretch**に設定され、その後、パスがピン留めされています。 それ以外の場合、スケーリング変換は固定されません。

パスにピン留めされたスケーリング変換がない場合は、パスのスケーリングサポートフラグを調整する必要があるかどうかを判断します。 サポートフラグを調整する必要があるのは、制約と連携していない種類のスケーリングがサポートされている場合、または制約と共存しているスケーリングの種類のサポートを表示できない場合です。 スケーリングサポートフラグを変更するには、D3DKMDT\_VIDPN\_、フラグを保持する[ **\_サポート構造\_パス\_スケーリング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling_support)のメンバーを設定します。

### <a name="adjusting-rotation-support-flags"></a>回転のサポートフラグの調整

パスの回転サポートフラグの調整は、パスのスケーリングサポートフラグの調整に似ています。 *Vpnpath*が、\_パス構造の D3DKMDT\_VIDPN\_存在すると仮定します。 *Vpnpath*の場合。**Contenttransformation. ローテーション**は、 **D3DKMDT\_VPPR\_IDENTITY**、 **D3DKMDT\_vppr\_ROTATE90**、 **D3DKMDT\_Vppr\_ROTATE180**、または**D3DKMDT\_vppr\_ROTATE270**に設定されます。その後、パスの回転変換はピン留めされます。 それ以外の場合、回転変換はピン留めされません。 ローテーションサポートフラグは、 *Vpnpath*に含まれています。**Contenttransformation. RotationSupport**。

### <a name="span-idreporting_multisampling_methodsspanspan-idreporting_multisampling_methodsspanreporting-multisampling-methods"></a><span id="reporting_multisampling_methods"></span><span id="REPORTING_MULTISAMPLING_METHODS"></span>マルチサンプリングメソッドのレポート

ディスプレイアダプターにマルチサンプリングによるアンチエイリアシングが可能なビデオ出力コーデックが1つ以上ある場合は、固定モードの各ソースについて、使用可能なマルチサンプリングメソッド (制約を指定) を報告する必要があります。 使用可能なマルチサンプリング方法を報告するには、次の手順を実行します。

-   [D3DDDI\_MULTISAMPLINGMETHOD](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_multisamplingmethod)構造体の配列を作成する
-   この配列を、 [VidPN インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface)の[**pfnAssignMultisamplingMethodSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_assignmultisamplingmethodset)関数に渡します。

[D3DDDI\_MULTISAMPLINGMETHOD](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_multisamplingmethod)構造体には、マルチサンプリング方法を特徴付ける2つのメンバーを設定する必要があります。 **Numsamples**メンバーは、サンプリングされるサブピクセルの数を示します。 **NumQualityLevels**メンバーは、メソッドが操作できる品質レベルの数を示します。 レベル noticably のそれぞれの増加によって、表示されるイメージの品質が向上する限り、任意の数の品質レベルを指定できます。

### <a name="span-idenumeration_pivotsspanspan-idenumeration_pivotsspanenumeration-pivots"></a><span id="enumeration_pivots"></span><span id="ENUMERATION_PIVOTS"></span>列挙型ピボット

前に説明したように、 *DxgkDdiEnumVidPnCofuncModality*は、 *hConstrainingVidPn*パラメーターで渡された VidPN と cofunctional するモードセットを作成する必要があります。 場合によっては、 *DxgkDdiEnumVidPnCofuncModality*は、 *enumpivottype*パラメーターおよび*enumpivot*パラメーターで渡される追加情報 (列挙ピボット) に従って動作を拡張する必要があります。

列挙ピボットには、次のいずれかを指定できます。

-   特定のビデオの存在ソースのモードセット

-   特定のビデオの現在のターゲットのモードセット

-   特定の VidPN の現在のパスのスケーリング変換

-   特定の VidPN の現在のパスの回転変換

列挙ピボットがモードに設定されている場合、 *DxgkDdkEnumVidPnCofuncModality*はそのモードを変更せずに残しておく必要があります。 列挙ピボットがパスのスケーリング (回転) 変換である場合、 *DxgkDdiEnumVidPnCofuncModality*はそのパスのスケーリング (回転) のサポートフラグを変更することはできません。

 

 





