---
title: VidPN オブジェクトおよびインターフェイス
description: VidPN オブジェクトおよびインターフェイス
ms.assetid: 5dedac8c-9a99-4b3a-81be-39819135cd97
keywords:
- ビデオの現在のネットワーク WDK 表示、オブジェクト
- VidPN WDK display、objects
- オブジェクト WDK ビデオの現在のネットワーク
- インターフェイス WDK ビデオの現在のネットワーク
- ビデオの現在のネットワーク WDK ディスプレイ、インターフェイス
- VidPN WDK ディスプレイ、インターフェイス
- サブオブジェクト WDK ビデオの現在のネットワーク
ms.date: 10/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: c1d7cc0564a849b04b1a37ba9ebfa15a1ceb0765
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829187"
---
# <a name="vidpn-objects-and-interfaces"></a>VidPN オブジェクトおよびインターフェイス


ビデオの present (VidPN) マネージャーは、VidPN オブジェクトを使用して、ビデオの現在のソース、ビデオの現在のターゲット、および表示モード間のアソシエーションに関する情報を保持します。 詳細については、「[ビデオの紹介」を](introduction-to-video-present-networks.md)参照してください。

## <a name="vidpn-object"></a>VidPN オブジェクト

VidPN オブジェクトには、次のサブオブジェクトが含まれています。

-   トポロジ

-   ソースモードセット

-   ターゲットモードセット

-   ソースモードセットの監視

-   モニターの頻度の範囲セット

-   モニター記述子セット

-   Path

-   Source (ソース)

-   対象

-   ソースモード

-   ターゲットモード

-   ソースモードの監視

次の図は、VidPN オブジェクトとそのサブオブジェクトを示しています。

![vidpn オブジェクトとそのサブオブジェクトを示す図](images/vidpnobject.png)

上の図は、特定のアソシエーションが一対一、一対多、多対一、多対多のいずれであるかを示しています。 たとえば、1つのソースが複数のパスに属することはできますが、ターゲットは1つのパスにしか属することができません。

図の青のオブジェクトにはハンドルとインターフェイスを使用してアクセスし、灰色のオブジェクトには構造体のポインターを介してアクセスします。 このコンテキストのインターフェイスは、関数ポインターを格納する構造体です。 たとえば、 [**DXGK\_VIDPNTOPOLOGY\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface)構造体には、topology manager によって実装される関数へのポインターが含まれています。これは、表示ミニポートドライバーが、トポロジオブジェクトを検査および変更するために呼び出します。 表示ミニポートドライバーは、これらの関数のいずれかを呼び出すときに、トポロジオブジェクトへのハンドルを提供する必要があります。 次の表は、VidPN オブジェクトとそのサブオブジェクトへのアクセスに使用されるハンドル、インターフェイス、およびポインターのデータ型を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オブジェクト</th>
<th align="left">アクセスメソッドとデータ型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>VidPN (VidPN インターフェイス)</p></td>
<td align="left"><p>ハンドルとインターフェイスを介してアクセスされます。</p>
<p>D3DKMDT_HVIDPN</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface" data-raw-source="[&lt;strong&gt;DXGK_VIDPN_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface)"><strong>DXGK_VIDPN_INTERFACE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>トポロジ (VidPN トポロジインターフェイス)</p></td>
<td align="left"><p>ハンドルとインターフェイスを介してアクセスされます。</p>
<p>D3DKMDT_HVIDPNTOPOLOGY</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface" data-raw-source="[&lt;strong&gt;DXGK_VIDPNTOPOLOGY_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface)"><strong>DXGK_VIDPNTOPOLOGY_INTERFACE</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>ソースモードセット (VidPN ソースモードセットインターフェイス)</p></td>
<td align="left"><p>ハンドルとインターフェイスを介してアクセスされます。</p>
<p>D3DKMDT_HVIDPNSOURCEMODESET</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpnsourcemodeset_interface" data-raw-source="[&lt;strong&gt;DXGK_VIDPNSOURCEMODESET_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpnsourcemodeset_interface)"><strong>DXGK_VIDPNSOURCEMODESET_INTERFACE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>ターゲットモードセット (VidPN ターゲットモードセットインターフェイス)</p></td>
<td align="left"><p>ハンドルとインターフェイスを介してアクセスされます。</p>
<p>D3DKMDT_HVIDPNTARGETMODESET</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntargetmodeset_interface" data-raw-source="[&lt;strong&gt;DXGK_VIDPNTARGETMODESET_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntargetmodeset_interface)"><strong>DXGK_VIDPNTARGETMODESET_INTERFACE</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>ソースモードセットの監視</p></td>
<td align="left"><p>ハンドルとインターフェイスを介してアクセスされます。</p>
<p>D3DKMDT_HMONITORSOURCEMODESET</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_monitorsourcemodeset_interface" data-raw-source="[&lt;strong&gt;DXGK_MONITORSOURCEMODESET_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_monitorsourcemodeset_interface)"><strong>DXGK_MONITORSOURCEMODESET_INTERFACE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>Path</p></td>
<td align="left"><p>構造体ポインターを介してアクセスされます。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path" data-raw-source="[&lt;strong&gt;D3DKMDT_VIDPN_PRESENT_PATH&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path)"><strong>D3DKMDT_VIDPN_PRESENT_PATH</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Source (ソース)</p></td>
<td align="left"><p>構造体ポインターを介してアクセスされます。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_present_source" data-raw-source="[&lt;strong&gt;D3DKMDT_VIDEO_PRESENT_SOURCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_present_source)"><strong>D3DKMDT_VIDEO_PRESENT_SOURCE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>対象</p></td>
<td align="left"><p>構造体ポインターを介してアクセスされます。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_present_target" data-raw-source="[&lt;strong&gt;D3DKMDT_VIDEO_PRESENT_TARGET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_present_target)"><strong>D3DKMDT_VIDEO_PRESENT_TARGET</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>ソースモード</p></td>
<td align="left"><p>構造体ポインターを介してアクセスされます。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_source_mode" data-raw-source="[&lt;strong&gt;D3DKMDT_VIDPN_SOURCE_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_source_mode)"><strong>D3DKMDT_VIDPN_SOURCE_MODE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>ターゲットモード</p></td>
<td align="left"><p>構造体ポインターを介してアクセスされます。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_target_mode" data-raw-source="[&lt;strong&gt;D3DKMDT_VIDPN_TARGET_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_target_mode)"><strong>D3DKMDT_VIDPN_TARGET_MODE</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>ソースモードの監視</p></td>
<td align="left"><p>構造体ポインターを介してアクセスされます。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_monitor_source_mode" data-raw-source="[&lt;strong&gt;D3DKMDT_MONITOR_SOURCE_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_monitor_source_mode)"><strong>D3DKMDT_MONITOR_SOURCE_MODE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>モニターの頻度の範囲セット</p></td>
<td align="left"><p>構造体ポインターを介してアクセスされます。</p>
<p>[<strong>DXGK_MONITORFREQUENCYRANGESET_INTERFACE</strong> ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_monitorfrequencyrangeset_interface)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>モニター記述子セット</p></td>
<td align="left"><p>構造体ポインターを介してアクセスされます。</p>
<p>[<strong>DXGK_MONITORDESCRIPTORSET_INTERFACE</strong>](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_monitordescriptorset_interface)</p></td>
</tr>
</tbody>
</table>

## <a name="vidpn-manager"></a>VidPN マネージャー

DirectX グラフィックスカーネルサブシステムのコンポーネントの1つである VidPN マネージャーは、VidPNs をビルドして維持するためのディスプレイミニポートドライバーを使用して共同で動作します。 次の手順では、表示ミニポートドライバーが、VidPN オブジェクトへのハンドルとインターフェイスを取得する方法について説明します。

1.  初期化中に、DirectX graphics カーネルサブシステムは、ディスプレイミニポートドライバーの[*DxgkDdiStartDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_start_device)関数を呼び出します。 この呼び出しでは、DirectX グラフィックスカーネルサブシステムによって実装されている関数へのポインターを含む、 [**DXGKRNL\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)構造を持つミニポートドライバーが表示されます。 これらの関数の1つは[*DxgkCbQueryVidPnInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_queryvidpninterface)です。

2.  ある時点で、VidPN マネージャーは、表示ミニポートドライバーのヘルプを必要とします。そのため、次の関数のいずれかを呼び出すことによって、表示ミニポートドライバーに、VidPN オブジェクトへのハンドルを提供します。
    -   [*DxgkDdiIsSupportedVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_issupportedvidpn)
    -   [*DxgkDdiRecommendFunctionalVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)
    -   [*DxgkDdiEnumVidPnCofuncModality*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)

3.  表示ミニポートドライバーは、手順 2. で取得したハンドルを[*DxgkCbQueryVidPnInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkcb_queryvidpninterface)に渡します。これにより、 [**DXGK\_VIDPN\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface)構造へのポインターが返されます。

表示ミニポートドライバーには、VidPN オブジェクトへのハンドルとインターフェイスがあり、プライマリサブオブジェクト (トポロジ、ソースモードセット、ターゲットモードセット、監視ソースモードセット) へのハンドルとインターフェイス (必要に応じて) を取得できます。 たとえば、表示ミニポートドライバーは、 [*Pfngettopology*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_gettopology) (vidpn インターフェイス内の関数の1つ) を呼び出して、vidpn トポロジオブジェクトへのハンドルと、 [**DXGK\_VIDPNTOPOLOGY\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface)構造へのポインターを取得できます。

次の関数 (VidPN インターフェイス内) は、VidPN オブジェクトのプライマリサブオブジェクトに対するハンドルとインターフェイスを提供します。

-   [*pfnGetTopology*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_gettopology)
-   [*pfnAcquireSourceModeSet*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_acquiresourcemodeset)
-   [*pfnAcquireTargetModeSet*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_acquiretargetmodeset)

前の一覧の2つの関数には、VidPN サブオブジェクトをリリースする対応する関数が含まれていることに注意してください。

-   [*pfnReleaseSourceModeSet*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_releasesourcemodeset)

-   [*pfnReleaseTargetModeSet*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_releasetargetmodeset)

表示ミニポートドライバーは、VidPNs のいずれかのプライマリサブオブジェクトへのハンドルとインターフェイスを取得した後、そのサブオブジェクトに関連するオブジェクトの記述子を取得するためにインターフェイス関数を呼び出すことができます。 たとえば、トポロジオブジェクトへのハンドルとインターフェイスを指定した場合、ディスプレイミニポートドライバーは、次の手順を実行してトポロジ内のすべてのパスの記述子を取得することができます。

1.  [VidPN トポロジインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface)

    VidPN トポロジインターフェイスの[*pfnAcquireFirstPathInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpntopology_acquirefirstpathinfo)関数を呼び出して、トポロジ内の最初のパスを記述する[ **\_パス構造の D3DKMDT\_vidpn\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path)へのポインターを取得します。

2.  [VidPN トポロジインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface)

    [*PfnAcquireNextPathInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpntopology_acquirenextpathinfo)関数を繰り返し呼び出して、トポロジ内の残りのパスを記述する\_パス構造の D3DKMDT\_VIDPN\_へのポインターを取得します。

同様に、表示ミニポートドライバーは、次のいずれかのモード設定インターフェイスの*pfnAcquireFirstModeInfo*関数と*pfnAcquireNextModeInfo*関数を呼び出すことによって、モードセットのモードの記述子を取得できます。

-   [**DXGK\_VIDPNSOURCEMODESET\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpnsourcemodeset_interface)

-   [**DXGK\_VIDPNTARGETMODESET\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntargetmodeset_interface)

-   [**DXGK\_MONITORSOURCEMODESET\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_monitorsourcemodeset_interface)

[**DXGK\_VIDPNSOURCEMODESET\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpnsourcemodeset_interface)インターフェイスには、ソースモードセットからモードを削除するための機能がないことに注意してください。 表示ミニポートドライバーでソースモードセットを更新する必要がある場合、モードの追加と削除によって既存のモードが変更されることはありません。 代わりに、古いモードセットを置き換える新しいモードセットが作成されます。 モードセットを更新する必要がある関数の例としては、ディスプレイミニポートドライバーの[*DxgkDdiEnumVidPnCofuncModality*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)関数があります。 ソースモードセットの更新に必要な手順は次のとおりです。

1.  [**DXGK\_VIDPNSOURCEMODESET\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpnsourcemodeset_interface)インターフェイスの[*pfnCreateNewModeInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_createnewmodeinfo)を呼び出して、 [**D3DKMDT\_vidpn\_ソース\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_source_mode)構造体へのポインターを取得します (vidpn マネージャーによって割り当てられます)。

    [*Pfnaddmode*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_addmode)を繰り返し呼び出して、モードをソースモードセットに追加します。

2.  [**DXGK\_VIDPN\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface)の[*Pfnassign Sourcemodeset*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_assignsourcemodeset)関数を呼び出して、新しいモードセットを特定のビデオの存在するソースに割り当てます。 新しいソースモードセットによって、そのソースに現在割り当てられているソースモードセットが置き換えられます。

ターゲットモードセットの更新は、ソースモードセットの更新に似ています。 [**DXGK\_VIDPNTARGETMODESET\_interface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntargetmodeset_interface)インターフェイスには、次の関数があります。

-   [VidPN ターゲットモードセットインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_target_mode)

    新しいターゲットモードセットを作成するための[*pfnCreateNewModeInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpntargetmodeset_createnewmodeinfo)関数と、セットにモードを追加するための[*Pfnaddmode*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpntargetmodeset_addmode)関数。

特定のパスに属するソースとターゲットを取得するためのインターフェイス (関数のセット) はありません。 表示ミニポートドライバーは、特定のパスに属する**ソースとターゲット**を特定できます。そのためには、 [**D3DKMDT\_VIDPN\_存在する\_のパス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path)構造の**メンバーを調べ**ます。パスを表します。

## <a name="see-also"></a>関連項目

[表示アダプターでの VidPN がサポートされているかどうかの確認](determining-whether-a-vidpn-is-supported-on-a-display-adapter.md)

[Cofunctional な VidPN ソースモードとターゲットモードを列挙しています](enumerating-cofunctional-vidpn-source-and-target-modes.md)

[動画に関するネットワークの用語](video-present-network-terminology.md)

[追加のモニターターゲットモードの取得](obtaining-additional-monitor-target-modes.md)