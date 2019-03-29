---
title: GDI ハーフトーン サービス
description: GDI ハーフトーン サービス
ms.assetid: 21112cfc-f7c4-4cce-a9bb-c68d918f5678
keywords:
- GDI WDK Windows 2000 の表示、ハーフトーン
- グラフィックス ドライバー WDK Windows 2000 の表示、ハーフトーン
- 描画の WDK GDI、ハーフトーン
- ハーフトーン WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8832636c506c698e0576b0a8101915cad29f3c7f
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349542"
---
# <a name="gdi-halftone-services"></a>GDI ハーフトーン サービス


## <span id="ddk_gdi_halftone_services_gg"></span><span id="DDK_GDI_HALFTONE_SERVICES_GG"></span>


GDI ハーフトーン サポートには、次の表に示されているサービスが含まれます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567314" data-raw-source="[&lt;strong&gt;HT_ComputeRGBGammaTable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567314)"><strong>HT_ComputeRGBGammaTable</strong></a></p></td>
<td align="left"><p>ガンマ番号に基づいて、デバイスの赤、緑、および青の強度を計算する GDI をによりします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567317" data-raw-source="[&lt;strong&gt;HT_Get8BPPFormatPalette&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567317)"><strong>HT_Get8BPPFormatPalette</strong></a></p></td>
<td align="left"><p>ピクセル デバイスの種類ごとに標準の 8 ビットで使用するためのハーフトーン パレットを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567320" data-raw-source="[&lt;strong&gt;HT_Get8BPPMaskPalette&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567320)"><strong>HT_Get8BPPMaskPalette</strong></a></p></td>
<td align="left"><p>デバイスの種類をピクセルあたり 8 ビットのマスク パレットを返します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567308" data-raw-source="[&lt;strong&gt;HTUI_DeviceColorAdjustment&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567308)"><strong>HTUI_DeviceColorAdjustment</strong></a></p></td>
<td align="left"><p>デバイスのハーフトーン プロパティを調整するユーザーを許可する ダイアログ ボックスが表示されます。</p></td>
</tr>
</tbody>
</table>

 

 

 





