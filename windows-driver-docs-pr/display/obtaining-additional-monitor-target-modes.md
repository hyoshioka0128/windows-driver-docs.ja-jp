---
title: 追加のモニター ターゲット モードの取得
description: 追加のモニター ターゲット モードの取得
ms.assetid: fc0e2d43-8fc2-4757-ba77-f72a01e04343
keywords:
- 監視対象モード WDK 表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9481aa19a9e238df3021b6587369df9de8b2678
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840524"
---
# <a name="obtaining-additional-monitor-target-modes"></a>追加のモニター ターゲット モードの取得


Windows 7 以降では、新しい monitor インターフェイスを使用できるようになり、 [**DXGK\_monitor\_interface\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_monitor_interface_v2)が提供されます。 元の[**DXGK\_MONITOR\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgk_monitor_interface)インターフェイスにはない2つの追加関数が用意されています。

[**pfnGetAdditionalMonitorModeSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_monitor_getadditionalmonitormodeset)

[**pfnReleaseAdditionalMonitorModeSet**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_monitor_releaseadditionalmonitormodeset)

これらの関数は、表示ミニポートドライバーで、ターゲットモードを VidPN ターゲットに追加するための動的でスケーラブルな方法を提供します。 一方、DXGK\_MONITOR\_INTERFACE インターフェイスでは、ターゲットモードの静的リストのみが提供されます。 これらの関数を使用すると、ドライバーはオペレーティングシステムに対して、列挙する必要がある追加モードの一覧を照会できます。 ドライバーは、要求されたモードを検証し、モニターがサポートしていないモードを拒否することができます。

ディスプレイミニポートドライバーが、ドライバーによって実装された[**DxgkDdiEnumVidPnCofuncModality**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_enumvidpncofuncmodality)関数への呼び出しを受信し、ターゲットモードを列挙すると、

互換性のあるタイミング情報をターゲットモードセットに追加するには、次の手順を実行する必要があります。

1.  [**Pfngetadditionalmonitormodeset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_monitor_getadditionalmonitormodeset)を呼び出すときに取得する、フィルター処理された追加のターゲットモードを返します。 また、 [Cofunctional な VidPN ソースモードとターゲットモードの列挙](enumerating-cofunctional-vidpn-source-and-target-modes.md)に関するページで説明されているように、通常のターゲットモードも返される必要があります。

2.  **Pfngetadditionalmonitormodeset**関数は、次の値を返します。
    -   *Ppadditionalmodes set*。 [**DXGK\_targetmode\_詳細\_タイミング**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_dxgk_targetmode_detail_timing)形式の追加のタイミングモードの一覧です。
    -   *Pnumber モードは、* タイミングモードの数です。

3.  これらのタイミングモードをすべて反復処理します。

4.  互換性のないすべてのタイミングモードと、 *DxgkDdiEnumVidPnCofuncModality*の呼び出し中に既に指定されていた標準モードをすべて除外します。

5.  残りのタイミングモードを[**D3DKMDT\_VIDPN\_ターゲット\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmdt/ns-d3dkmdt-_d3dkmdt_vidpn_target_mode)の種類に変換します。

6.  残りのすべてのタイミングモードを、VidPN ターゲットモードセットに追加します。

7.  [**Pfnreleaseadditionalmonitormodeset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_monitor_releaseadditionalmonitormodeset)を呼び出して、 **pfnreleaseadditionalmonitormodeset**から返された追加のタイミングモードの一覧を解放します。

表示ミニポートドライバーは、ハードウェアによってサポートされているすべての追加のタイミングモードを、VidPN ソースモードセットとターゲットモードセットに追加する必要があります。 表示モードマネージャー (DMM) によってモードの一覧が生成されると、モニターでサポートされていない、追加のタイミングモードを含むすべての表示モードがモニターでサポートされていないと表示され、raw モードの一覧にのみ表示されます。 モニターが接続されているかどうかに関係なく、ミニポートドライバーは、モニターでサポートされているすべての VidPN ソースおよびターゲットモードセットを報告する必要があります。 監視がサポートされているモードのみを報告するドライバーは、現在接続されているモニターでサポートされていない追加のモードも報告する必要があります。

## <a name="crt-monitors"></a>CRT モニター

CRT モニターの場合、DMM は追加のターゲットモードとして、ビデオエレクトロニクス標準の関連付け (VESA) 仕様で定義されている 640 x 480 x 60Hz の標準モニターのタイミングを追加します。 *vesa と業界標準のコンピューターディスプレイモニターのガイドラインタイミングバージョン 1.0*。

## <a name="dtv-and-hdtv-monitors"></a>DTV モニターと HDTV モニター

デジタルテレビ (DTV) モニターと高解像度テレビ (HDTV) モニターの場合、DMM は、次の表に示すように[、自動テスト](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)グラフィックス0043で必要なすべての標準 DTV モードを追加のターゲットモードとして追加します。 ディスプレイミニポートドライバーは、ディスプレイハードウェアでサポートされていないすべてのモードを排除する必要があります。

**59.95 hz DTV システム:**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DTV 形式</th>
<th align="left">HDTV 形式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>640 x 480p x ゲーム (59.94 Hz、縦横比4:3</p></td>
<td align="left"><p>640 x 480p x ゲーム (59.94 Hz、縦横比4:3</p></td>
</tr>
<tr class="even">
<td align="left"><p>720 (1440) x 480i x ゲーム (59.94 Hz、縦横比4:3</p></td>
<td align="left"><p>720 (1440) x 480i x ゲーム (59.94 Hz、縦横比4:3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>720 (1440) x 480i x ゲーム (59.94 Hz、縦横比16:9</p></td>
<td align="left"><p>720 (1440) x 480i x ゲーム (59.94 Hz、縦横比16:9</p></td>
</tr>
<tr class="even">
<td align="left"><p>720 x 480p x ゲーム (59.94 Hz、縦横比4:3</p></td>
<td align="left"><p>720 x 480p x ゲーム (59.94 Hz、縦横比4:3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>720 x 480p x ゲーム (59.94 Hz、縦横比16:9</p></td>
<td align="left"><p>720 x 480p x ゲーム (59.94 Hz、縦横比16:9</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>1280 x 720p x ゲーム (59.94 Hz、縦横比16:9</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>1920 x1080i x ゲーム (59.94 Hz、縦横比16:9</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>1920 x 1080p x ゲーム (59.94 Hz、縦横比16:9</p></td>
</tr>
</tbody>
</table>

 

**50Hz DTV システム:**

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DTV 形式</th>
<th align="left">HDTV 形式</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>640 x 480p x ゲーム (59.94 Hz、縦横比4:3</p></td>
<td align="left"><p>640 x 480p x ゲーム (59.94 Hz、縦横比4:3</p></td>
</tr>
<tr class="even">
<td align="left"><p>720 (1440) x 576i x 50Hz、縦横比4:3</p></td>
<td align="left"><p>720 (1440) x 576i x 50Hz、縦横比4:3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>720 (1440) x 576i x 50Hz、縦横比16:9</p></td>
<td align="left"><p>720 (1440) x 576i x 50Hz、縦横比16:9</p></td>
</tr>
<tr class="even">
<td align="left"><p>720 x 576p x 50Hz、縦横比4:3</p></td>
<td align="left"><p>720 x 576p x 50Hz、縦横比4:3</p></td>
</tr>
<tr class="odd">
<td align="left"><p>720 x 576p x 50Hz、縦横比16:9</p></td>
<td align="left"><p>720 x 576p x 50Hz、縦横比16:9</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>1280 x 720p x 50Hz、縦横比16:9</p></td>
</tr>
<tr class="odd">
<td align="left"></td>
<td align="left"><p>1920 x 1080i x 50Hz、縦横比16:9</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>1920 x 1080p x 50Hz、縦横比16:9</p></td>
</tr>
</tbody>
</table>

 

Windows Vista 用に記述されたミニポートドライバーは、引き続き自動テストグラフィックス-0043 に準拠し[ている必要](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)があります。また、これらのテーブルに指定されている追加の DTV モードを追加します。 Windows 7 向けに作成されたドライバーは、新しい**Pfngetadditionalmonitormodeset**関数と**pfngetadditionalmonitormodeset**関数をサポートするだけで済みます。


 
## <a name="see-also"></a>関連項目

[表示アダプターでの VidPN がサポートされているかどうかの確認](determining-whether-a-vidpn-is-supported-on-a-display-adapter.md)

[Cofunctional な VidPN ソースモードとターゲットモードを列挙しています](enumerating-cofunctional-vidpn-source-and-target-modes.md)

[動画に関するネットワークの用語](video-present-network-terminology.md)

[VidPN オブジェクトとインターフェイス](vidpn-objects-and-interfaces.md)