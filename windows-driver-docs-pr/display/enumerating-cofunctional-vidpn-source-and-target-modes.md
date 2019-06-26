---
title: Cofunctional VidPN ソースおよびターゲット モードの列挙
description: Cofunctional VidPN ソースおよびターゲット モードの列挙
ms.assetid: f1aa6277-7af6-4ba0-8ff1-d562f7029540
keywords:
- ビデオは、WDK の表示をネットワークに存在、ターゲットとソースのモードの列挙
- VidPN WDK の表示は、ターゲットを列挙し、ソースのモード
- 制約の VidPN WDK
- WDK ビデオ存在するネットワークのモードがターゲットとソースを列挙します。
- ソース モード WDK ビデオ存在するネットワーク
- ターゲット モード WDK ビデオ存在するネットワーク
- WDK ビデオ存在するネットワークの拡大縮小の変換をピン留め
- 回転変換 WDK ビデオ存在するネットワークをピン留め
- WDK ビデオ存在するネットワークのマルチ サンプリング メソッド
- モードは、WDK ビデオ存在するネットワークを設定します。
- 制約の VidPN WDK の検査
- WDK ビデオ存在するネットワークをフラグ スケーリングをサポート
- WDK 存在するネットワークのビデオの回転をサポートするフラグ
- 列挙体 pivot WDK ビデオ存在するネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: faac0a2042c7091eacbc5ef61bc1d663ad4c26a3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355548"
---
# <a name="enumerating-cofunctional-vidpn-source-and-target-modes"></a>Cofunctional VidPN ソースおよびターゲット モードの列挙


このトピックでは、ビデオの存在するネットワーク (VidPN) マネージャーとディスプレイのミニポート ドライバーが存在するビデオのソースとターゲットで販売されているモードを列挙するために共同作業方法について説明します。 このガイドを読む前に次のトピックの内容に精通する必要があります。

-   [ビデオの存在するネットワークの概要](introduction-to-video-present-networks.md)

-   [VidPN オブジェクトとインターフェイス](vidpn-objects-and-interfaces.md)

ときどき、VidPN マネージャーは、ディスプレイ アダプターのビデオの存在するソースとターゲットで販売されているモードを列挙するためにディスプレイのミニポート ドライバーを確認します。 通常、要求では、次のパターンがあります。

1.  VidPN マネージャーを作成またはをそのソースとターゲットのすべてではありませんが、一部は、ピン留めされたモードを持つ VidPN を取得します。

2.  VidPN manager 呼び出し[ **DxgkDdiIsSupportedVidPn** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_issupportedvidpn)をディスプレイ アダプターでサポートされている機能 VidPN を形成する、VidPN を拡張できるかどうかを判断します。 つまり、既存の固定モードを変更することがなく、残りのソースとターゲットのモードを固定することができるかどうかを確認します。

3.  VidPN manager 呼び出し[ **DxgkDdiEnumVidPnCofuncModality** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)しないモードに固定するターゲット、ソースで利用できるモードを取得します。

渡される引数の 1 つ*DxgkDdiEnumVidPnCofuncModality*制約 VidPN と呼ばれる VidPN オブジェクトへのハンドルします。

*DxgkDdiEnumVidPnCofuncModality*次を実行する必要があります。

-   制約の VidPN を検査します。

-   各ソースおよびターゲット固定モードがない cofunctional の制約には、最大の可能なモードのセットになるよう設定されて、モードを調整します。

-   固定のスケーリング変換がないパスごとに、制約を持つ cofunctional ように、スケーリングをサポートするフラグを調整します。

-   各パスはない、ピン留めされた回転変換がある、回転角度を調整するには、cofunctional 制約を持つようにフラグをサポートします。

-   ピン留めされたモードになっているソースごとに、そのソースで利用可能なマルチ サンプリング メソッドを報告します。

次の段落では、前の箇条書きリスト内の各タスクを実行する方法の詳細を付与します。

### <a name="span-idinspectingtheconstrainingvidpnspanspan-idinspectingtheconstrainingvidpnspaninspecting-the-constraining-vidpn"></a><span id="inspecting_the_constraining_vidpn"></span><span id="INSPECTING_THE_CONSTRAINING_VIDPN"></span>制約の VidPN の検査

制約の VidPN の次のプロパティは、制約によって優先順位を付ける必要があります*DxgkDdiEnumVidPnCofuncModality*します。

-   トポロジ (ソースとターゲット間の関連付けのセット)

-   固定モード

-   スケーリング、スケーリングの各パスのサポート、回転、および回転のサポート

-   各パスのターゲットの色の基礎

-   各パスのターゲット色係数の動的範囲

-   各パスのコンテンツの種類 (グラフィックスまたはビデオ)

-   各パスのガンマごとの傾斜増加

制約 VidPN から制約を抽出するには、次の手順を実行します。

-   呼び出して開始、 [ **pfnGetTopology** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_gettopology)へのポインターを取得する関数を[VidPN トポロジ インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface)制約 VidPN トポロジを表します。

-   呼び出す、 [ **pfnAcquireFirstPathInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpntopology_acquirefirstpathinfo)と[ **pfnAcquireNextPathInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpntopology_acquirenextpathinfo)関数内の各パスに関する情報を取得します制約 VidPN トポロジ。 特定のパス (ソース ID、ターゲットの ID、スケール、変換、回転変換、ターゲットの色の基準など) に関する情報が含まれている、 [ **D3DKMDT\_VIDPN\_存在\_パス** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path)構造体。

-   パスごとにパスのソースの ID を渡す、 [ **pfnAcquireSourceModeSet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_acquiresourcemodeset)パスのソースを取得します。

-   呼び出す、 [ **pfnAcquirePinnedModeInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_acquirepinnedmodeinfo)モード (存在する場合) は、ソースのモードのセットに固定するかを判断する関数。 ソースのモードのセットに固定モードがある場合は、セット内の残りのモードを確認する必要はおそらくありません。 モードのセットが固定モードを持たない場合は、セット内の残りのモードを呼び出すことによって調べる[ **pfnAcquireFirstModeInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_acquirefirstmodeinfo)と[ **pfnAcquireNextModeInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_acquirenextmodeinfo).

    同様の手順を使用して、ターゲット モードの設定を確認し、ターゲット モードを確認する、セットのモードがピン留めします。

### <a name="span-idadjustingmodesetsspanspan-idadjustingmodesetsspanadjusting-mode-sets"></a><span id="adjusting_mode_sets"></span><span id="ADJUSTING_MODE_SETS"></span>調整モードの設定

ソースとターゲットを制約する VidPN トポロジに関連付けられているモード設定を検査するには、セットにはどちらのモードのモードがピン留めをメモしてをおきます。 モードを設定する場合は、固定モードになっているため、調整する必要があるかどうかを判断することはありません。 Cofunctional 制約ではないモードが含まれている場合、または制約を持つ cofunctional は使用可能なモードがない場合、モード設定を調整する必要があります。

モニターが接続されているビデオの存在ターゲットも、モニターでサポートされるモードのセットを検討する必要があります。 ビデオの存在ターゲット ディスプレイ アダプターでは、(制約を考慮した) 特定のモードをサポートする場合でものみで、ターゲットのモードが接続されているモニターには、モードもサポートしている場合に設定するには、そのモードを一覧表示する必要があります。 接続されているモニターがサポートするモードを確認するのには、次の手順を実行します。

-   [DXGK\_モニター インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_monitor_interface)

    呼び出す[ **pfnAcquireMonitorSourceModeSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_monitor_acquiremonitorsourcemodeset)します。 モードを設定が必要ないない場合の調整、単独で省略できます。 コード型のモード設定を調整する必要がある場合新しいモードのセットを作成する新しい設定の既存のモードを置き換えますする必要があります。

-   [DXGK_VIDPN_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface)

    新しいソース モードのセットを作成し、呼び出す[ **pfnCreateNewSourceModeSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_createnewsourcemodeset)します。

-   [_DXGK_VIDPNSOURCEMODESET_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpnsourcemodeset_interface)

    呼び出して[ **pfnCreateNewModeInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_createnewmodeinfo)と[ **pfnAddMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_addmode)します。

-   [DXGK_VIDPN_INTERFACE](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface)

    最後に呼び出す[ **pfnAssignSourceModeSet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_assignsourcemodeset)を既存のソース モードの新しい設定を置き換えます。

### <a name="adjusting-scaling-support-flags"></a>スケーリングをサポートするフラグを調整します。

制約 VidPN トポロジ内の各パスのパスが固定のスケーリング変換を持つかどうかを決定します。 この決定をするためには、検査*vpnPath*.**ContentTransformation.Scaling**ここで、 *vpnPath*は、 [ **D3DKMDT\_VIDPN\_存在\_パス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path)パスを表す構造体です。 場合*vpnPath*.**ContentTransformation.Scaling**に設定されている**D3DKMDT\_VPPS\_IDENTITY**、 **D3DKMDT\_VPPS\_中央揃え**、または**D3DKMDT\_VPPS\_STRETCHED**パスのスケーリング変換がピン留めします。 それ以外の場合、スケール変換はピン留めされていません。

パスが固定のスケーリング変換を持たない場合は、パスのスケーリングをサポートするフラグを調整する必要があるかどうかを決定します。 スケーリングの型のサポートは、cofunctional の制約がないか、スケーリングの型のサポートに失敗する場合は、制約 cofunctional を表示する場合は、サポートのフラグを調整する必要があります。 メンバーを設定、スケーリングをサポートするフラグを変更する、 [ **D3DKMDT\_VIDPN\_存在\_パス\_スケーリング\_サポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path_scaling_support)フラグを保持する構造体。

### <a name="adjusting-rotation-support-flags"></a>回転をサポートするフラグを調整します。

パスの回転をサポートするフラグを調整することは、パスのスケーリングをサポートするフラグを調整することに似ています。 *VpnPath*は、D3DKMDT\_VIDPN\_存在\_パス構造。 場合*vpnPath*.**ContentTransformation.Rotation**に設定されている**D3DKMDT\_VPPR\_IDENTITY**、 **D3DKMDT\_VPPR\_ROTATE90**、**D3DKMDT\_VPPR\_ROTATE180**、または**D3DKMDT\_VPPR\_ROTATE270**パスの回転の変換にはピン留めします。 それ以外の場合、回転変換はピン留めされていません。 回転をサポートするフラグ*vpnPath*.**ContentTransformation.RotationSupport**します。

### <a name="span-idreportingmultisamplingmethodsspanspan-idreportingmultisamplingmethodsspanreporting-multisampling-methods"></a><span id="reporting_multisampling_methods"></span><span id="REPORTING_MULTISAMPLING_METHODS"></span>レポートのマルチ サンプリング メソッド

ディスプレイ アダプターでのマルチ サンプリング アンチエイリアシングの対応する 1 つまたは複数の出力ビデオ コーデックにされている場合は、固定モードになっているソースごとに (制約を考慮) 利用できるマルチ サンプリング メソッドを報告する必要があります。 使用可能なマルチ サンプリング メソッドを報告するには、次の手順を実行します。

-   配列を作成する[D3DDDI\_MULTISAMPLINGMETHOD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_multisamplingmethod)構造体
-   先の配列を渡す、 [ **pfnAssignMultisamplingMethodSet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_assignmultisamplingmethodset)の関数、 [VidPN インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface)します。

[D3DDDI\_MULTISAMPLINGMETHOD](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddi_multisamplingmethod)構造体が 2 つのメンバー、これは次のように設定する必要があります、マルチ サンプリング メソッドの特性を示す。 **NumSamples**メンバーは、サンプリングされた subpixels の数を示します。 **NumQualityLevels**メンバーは、メソッドを行える品質レベルの数を示します。 各レベルの増加が大幅に表示されるイメージの品質を改善する限り、任意の数の品質レベルを指定できます。

### <a name="span-idenumerationpivotsspanspan-idenumerationpivotsspanenumeration-pivots"></a><span id="enumeration_pivots"></span><span id="ENUMERATION_PIVOTS"></span>列挙型のピボット

前述のよう*DxgkDdiEnumVidPnCofuncModality*に渡された VidPN cofunctional いるモードのセットを作成する必要があります、 *hConstrainingVidPn*パラメーター。 場合によっては、 *DxgkDdiEnumVidPnCofuncModality*で渡される追加情報 (列挙体 pivot、) に応じて動作を拡張する必要があります、 *EnumPivotType*と*EnumPivot*パラメーター。

列挙型のピボットには、次のいずれかを指定できます。

-   ビデオ存在するソースを特定のモード設定

-   特定のビデオの存在ターゲットのモード設定

-   特定の VidPN 存在するパスのスケーリング変換

-   特定の VidPN 存在するパスの回転変換

モード設定は、列挙型のピボット*DxgkDdkEnumVidPnCofuncModality*そのモードが変更されていない設定のままにする必要があります。 列挙型のピボットが transformation の場合、スケーリング (回転)、パスの*DxgkDdiEnumVidPnCofuncModality*そのパスのスケーリング (回転) サポート フラグを変更する必要があります。

 

 





