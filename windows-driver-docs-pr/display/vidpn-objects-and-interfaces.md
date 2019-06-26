---
title: VidPN オブジェクトおよびインターフェイス
description: VidPN オブジェクトおよびインターフェイス
ms.assetid: 5dedac8c-9a99-4b3a-81be-39819135cd97
keywords:
- ビデオが存在するネットワーク オブジェクト、WDK の表示
- VidPN WDK の表示、オブジェクト
- オブジェクト WDK ビデオ存在するネットワーク
- インターフェイス WDK ビデオ存在するネットワーク
- ビデオが存在するネットワーク インターフェイス、WDK の表示
- VidPN WDK の表示、インターフェイス
- サブオブジェクト WDK ビデオ存在するネットワーク
ms.date: 10/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1d13cc87e3f5738bfd054ed339256ae8dc3d0b71
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381844"
---
# <a name="vidpn-objects-and-interfaces"></a>VidPN オブジェクトおよびインターフェイス


ビデオの存在 (VidPN) のネットワーク マネージャーでは、ビデオの存在するソース、ビデオの存在ターゲット、および表示モードの間の関連付けについての情報を保持するのに VidPN オブジェクトを使用します。 詳細については、次を参照してください。、[ビデオ存在するネットワークの概要](introduction-to-video-present-networks.md)トピック。

## <a name="vidpn-object"></a>VidPN オブジェクト

VidPN オブジェクトには、次のサブ オブジェクトが含まれています。

-   トポロジ

-   ソース モードの設定

-   ターゲット モードの設定

-   ソース モードのセットを監視します。

-   周波数の範囲のセットを監視します。

-   記述子の設定を監視します。

-   パス

-   Source

-   対象

-   ソース モード

-   ターゲット モード

-   ソース モードを監視します。

次の図は、VidPN オブジェクトとその下位のオブジェクトを示します。

![vidpn オブジェクトとその下位のオブジェクトを示す図](images/vidpnobject.png)

上記の図は、特定の関連付けが一対一、一対多、多対一または多対多であるかどうかを示します。 たとえば、図には、ソースが 1 つ以上のパスに属することができますが、ターゲットが所属できるは 1 つのみのパスを示します。

ダイアグラム内の青のオブジェクトは、ハンドルと、インターフェイスを介してアクセスし、灰色のオブジェクトは、構造体のポインターを介してアクセスします。 このコンテキストでインターフェイスは、関数ポインターを格納する構造体です。 など、 [ **DXGK\_VIDPNTOPOLOGY\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface)構造には (VidPN マネージャーによって実装される) 関数へのポインターが含まれているディスプレイのミニポート ドライバー検査し、トポロジ オブジェクトを変更するために呼び出します。 ディスプレイのミニポート ドライバーがこれらの関数のいずれかを呼び出すと、トポロジ オブジェクトを識別するハンドルを指定する必要があります。 次の表では、VidPN オブジェクトとそのサブ オブジェクトへのアクセスに使用されるハンドル、インターフェイス、およびポインターのデータ型を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">オブジェクト</th>
<th align="left">アクセス方法とデータの種類</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>VidPN (VidPN インターフェイス)</p></td>
<td align="left"><p>ハンドルおよびインターフェイスを介してアクセスします。</p>
<p>D3DKMDT_HVIDPN</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface" data-raw-source="[&lt;strong&gt;DXGK_VIDPN_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface)"><strong>DXGK_VIDPN_INTERFACE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>トポロジ (VidPN トポロジ インターフェイス)</p></td>
<td align="left"><p>ハンドルおよびインターフェイスを介してアクセスします。</p>
<p>D3DKMDT_HVIDPNTOPOLOGY</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface" data-raw-source="[&lt;strong&gt;DXGK_VIDPNTOPOLOGY_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface)"><strong>DXGK_VIDPNTOPOLOGY_INTERFACE</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>ソース モード (VidPN ソース モード設定インターフェイス) を設定します。</p></td>
<td align="left"><p>ハンドルおよびインターフェイスを介してアクセスします。</p>
<p>D3DKMDT_HVIDPNSOURCEMODESET</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpnsourcemodeset_interface" data-raw-source="[&lt;strong&gt;DXGK_VIDPNSOURCEMODESET_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpnsourcemodeset_interface)"><strong>DXGK_VIDPNSOURCEMODESET_INTERFACE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>ターゲット モード (VidPN ターゲット モード設定インターフェイス) を設定します。</p></td>
<td align="left"><p>ハンドルおよびインターフェイスを介してアクセスします。</p>
<p>D3DKMDT_HVIDPNTARGETMODESET</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntargetmodeset_interface" data-raw-source="[&lt;strong&gt;DXGK_VIDPNTARGETMODESET_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntargetmodeset_interface)"><strong>DXGK_VIDPNTARGETMODESET_INTERFACE</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>ソース モードのセットを監視します。</p></td>
<td align="left"><p>ハンドルおよびインターフェイスを介してアクセスします。</p>
<p>D3DKMDT_HMONITORSOURCEMODESET</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_monitorsourcemodeset_interface" data-raw-source="[&lt;strong&gt;DXGK_MONITORSOURCEMODESET_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_monitorsourcemodeset_interface)"><strong>DXGK_MONITORSOURCEMODESET_INTERFACE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>パス</p></td>
<td align="left"><p>構造体ポインターを通じてアクセスします。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path" data-raw-source="[&lt;strong&gt;D3DKMDT_VIDPN_PRESENT_PATH&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path)"><strong>D3DKMDT_VIDPN_PRESENT_PATH</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>Source</p></td>
<td align="left"><p>構造体ポインターを通じてアクセスします。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_present_source" data-raw-source="[&lt;strong&gt;D3DKMDT_VIDEO_PRESENT_SOURCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_present_source)"><strong>D3DKMDT_VIDEO_PRESENT_SOURCE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>対象</p></td>
<td align="left"><p>構造体ポインターを通じてアクセスします。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_present_target" data-raw-source="[&lt;strong&gt;D3DKMDT_VIDEO_PRESENT_TARGET&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_video_present_target)"><strong>D3DKMDT_VIDEO_PRESENT_TARGET</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>ソース モード</p></td>
<td align="left"><p>構造体ポインターを通じてアクセスします。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_source_mode" data-raw-source="[&lt;strong&gt;D3DKMDT_VIDPN_SOURCE_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_source_mode)"><strong>D3DKMDT_VIDPN_SOURCE_MODE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>ターゲット モード</p></td>
<td align="left"><p>構造体ポインターを通じてアクセスします。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_target_mode" data-raw-source="[&lt;strong&gt;D3DKMDT_VIDPN_TARGET_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_target_mode)"><strong>D3DKMDT_VIDPN_TARGET_MODE</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p>ソース モードを監視します。</p></td>
<td align="left"><p>構造体ポインターを通じてアクセスします。</p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_monitor_source_mode" data-raw-source="[&lt;strong&gt;D3DKMDT_MONITOR_SOURCE_MODE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_monitor_source_mode)"><strong>D3DKMDT_MONITOR_SOURCE_MODE</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>周波数の範囲のセットを監視します。</p></td>
<td align="left"><p>構造体ポインターを通じてアクセスします。</p>
<p>[<strong>DXGK_MONITORFREQUENCYRANGESET_INTERFACE</strong> ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_monitorfrequencyrangeset_interface)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>記述子の設定を監視します。</p></td>
<td align="left"><p>構造体ポインターを通じてアクセスします。</p>
<p>[<strong>DXGK_MONITORDESCRIPTORSET_INTERFACE</strong>](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_monitordescriptorset_interface)</p></td>
</tr>
</tbody>
</table>

## <a name="vidpn-manager"></a>VidPN マネージャー

構築して VidPNs を保持するディスプレイ ミニポート ドライバーを使用する DirectX グラフィックスのカーネル サブシステムのコンポーネントの 1 つは、VidPN マネージャーと連携します。 次の手順では、ディスプレイのミニポート ドライバーが、ハンドルと VidPN オブジェクトへのインターフェイスを取得する方法について説明します。

1.  初期化中に、DirectX グラフィックスのカーネルのサブシステムに呼び出すディスプレイ ミニポート ドライバーの[ *DxgkDdiStartDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/nc-dispmprt-dxgkddi_start_device)関数。 呼び出しが表示ミニポート ドライバーを提供する、 [ **DXGKRNL\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)構造体は、DirectX グラフィックスのカーネル サブシステムによって実装される関数へのポインターが含まれています。 これらの関数の 1 つは[ *DxgkCbQueryVidPnInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_queryvidpninterface)します。

2.  ある時点で VidPN マネージャーは、VidPN オブジェクトへのハンドルを次の関数の 1 つを呼び出すことによって、ディスプレイのミニポート ドライバーを提供できるように、ディスプレイのミニポート ドライバーからヘルプを必要します。
    -   [*DxgkDdiIsSupportedVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_issupportedvidpn)
    -   [*DxgkDdiRecommendFunctionalVidPn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_recommendfunctionalvidpn)
    -   [*DxgkDdiEnumVidPnCofuncModality*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)

3.  ディスプレイのミニポート ドライバーに手順 2. で取得されたハンドルを渡す[ *DxgkCbQueryVidPnInterface*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkcb_queryvidpninterface)へのポインターを返す、 [ **DXGK\_VIDPN\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface)構造体。

ディスプレイのミニポート ドライバーは、ハンドルと VidPN オブジェクトへのインターフェイスがある後、そのプライマリ サブオブジェクトへハンドルとインターフェイス (必要に応じて) を取得できます。 トポロジ、モード設定のソース、ターゲット モードのセット、およびモニター モードのセットのソース。 たとえば、ディスプレイのミニポート ドライバーを呼び出すことができます[ *pfnGetTopology* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_gettopology) (VidPN インターフェイス内の関数の 1 つ)、VidPN トポロジ オブジェクトを識別するハンドルとへのポインターを取得する、 [ **DXGK\_VIDPNTOPOLOGY\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface)構造体。

(VidPN インターフェイス) で、次の関数は、ハンドルと VidPN オブジェクトのプライマリのサブオブジェクトへのインターフェイスを提供します。

-   [*pfnGetTopology*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_gettopology)
-   [*pfnAcquireSourceModeSet*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_acquiresourcemodeset)
-   [*pfnAcquireTargetModeSet*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_acquiretargetmodeset)

VidPN サブオブジェクト リリース対応する関数がある上記のリスト内の関数の 2 つのことに注意してください。

-   [*pfnReleaseSourceModeSet*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_releasesourcemodeset)

-   [*pfnReleaseTargetModeSet*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_releasetargetmodeset)

ディスプレイのミニポート ドライバーでは、ハンドルと VidPNs プライマリのサブオブジェクトのいずれかへのインターフェイスを取得後、は、下位のオブジェクトに関連するオブジェクトの記述子を取得するインターフェイスの関数を呼び出すことができます。 たとえば、トポロジ オブジェクトを識別するハンドルとインターフェイスを指定、ディスプレイのミニポート ドライバーはトポロジ内のすべてのパスの記述子を取得する次の手順を実行可能性があります。

1.  [VidPN トポロジ インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface)

    呼び出す、 [ *pfnAcquireFirstPathInfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpntopology_acquirefirstpathinfo)へのポインターを取得するための VidPN トポロジ インターフェイスの関数を[ **D3DKMDT\_VIDPN\_存在\_パス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path)トポロジ内の最初のパスを記述する構造体。

2.  [VidPN トポロジ インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntopology_interface)

    呼び出す、 [ *pfnAcquireNextPathInfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpntopology_acquirenextpathinfo) D3DKMDT へのポインターを取得するために繰り返し関数\_VIDPN\_存在\_パス構造を記述する、トポロジ内の残りのパス。

同様に、ディスプレイのミニポート ドライバーは、呼び出すことによって設定モードでのモードの記述子を取得できます、 *pfnAcquireFirstModeInfo*と*pfnAcquireNextModeInfo*モードのセットを次のいずれかの関数インターフェイス。

-   [**DXGK\_VIDPNSOURCEMODESET\_INTERFACE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpnsourcemodeset_interface)

-   [**DXGK\_VIDPNTARGETMODESET\_INTERFACE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntargetmodeset_interface)

-   [**DXGK\_MONITORSOURCEMODESET\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_monitorsourcemodeset_interface)

なお、 [ **DXGK\_VIDPNSOURCEMODESET\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpnsourcemodeset_interface)インターフェイスには、モードをソース モードのセットから削除するための関数がありません。 ディスプレイのミニポート ドライバーでは、ソース モードのセットを更新する必要がある、設定の追加と削除モードによって、既存のモードは変更されません。 代わりに、以前のモードのセットを置換する新しいモードのセットを作成します。 モードのセットを更新する必要のある関数の例は、表示ミニポート ドライバーの[ *DxgkDdiEnumVidPnCofuncModality* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)関数。 ソース モードのセットを更新するための手順は次のとおりです。

1.  呼び出す、 [ *pfnCreateNewModeInfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_createnewmodeinfo)の[ **DXGK\_VIDPNSOURCEMODESET\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpnsourcemodeset_interface)ポインターを取得するインターフェイスを[ **D3DKMDT\_VIDPN\_ソース\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_source_mode) (VidPN マネージャーによって割り当てられた) 構造体。

    呼び出す[ *pfnAddMode* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpnsourcemodeset_addmode)モードをソース モードのセットに追加するには、繰り返し。

2.  呼び出す、 [ *pfnAssignSourceModeSet* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpn_assignsourcemodeset)の関数、 [ **DXGK\_VIDPN\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpn_interface)を割り当てる新しいモードは、特定のビデオ存在するソースに設定します。 新しいソース モードのセットには、そのソースに現在割り当てられているソース モードのセットが置き換えられます。

対象モードのセットを更新することは、ソース モードのセットの更新と同様です。 [ **DXGK\_VIDPNTARGETMODESET\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/ns-d3dkmddi-_dxgk_vidpntargetmodeset_interface)インターフェイスには、次の機能。

-   [インターフェイスの VidPN ターゲット モードの設定](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_target_mode)

    A [ *pfnCreateNewModeInfo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpntargetmodeset_createnewmodeinfo)新しいターゲット モードのセットを作成するための関数と[ *pfnAddMode* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_vidpntargetmodeset_addmode)モードをセットに追加するための関数。

ソースと特定のパスに属しているターゲットを取得するためのインターフェイス (関数のセット) はありません。 どのソースとターゲットに属している特定のパスを調べることによって、ディスプレイのミニポート ドライバーを調べる、 **VidPnSourceId**と**VidPnTargetId**のメンバー、 [ **D3DKMDT\_VIDPN\_存在\_パス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_present_path)パスを表す構造体です。

## <a name="see-also"></a>関連項目

[ディスプレイ アダプターではサポートされて、VidPN があるかどうかを決定します。](determining-whether-a-vidpn-is-supported-on-a-display-adapter.md)

[Cofunctional VidPN ソースとターゲット モードを列挙します。](enumerating-cofunctional-vidpn-source-and-target-modes.md)

[ビデオの存在するネットワーク用語](video-present-network-terminology.md)

[追加のモニター ターゲット モードを取得します。](obtaining-additional-monitor-target-modes.md)