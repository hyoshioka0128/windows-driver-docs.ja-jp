---
title: TrueType フォント ドライバー関数
description: TrueType フォント ドライバー関数
ms.assetid: 9ed59393-c4a6-4d3f-9a18-c9e5493c2dc9
keywords:
- フォント WDK グラフィックス、truetype フォント ドライバー関数
- GDI WDK Windows 2000 の表示、フォント、truetype フォント ドライバー関数
- グラフィック ドライバー WDK Windows 2000 を表示、フォント、truetype フォント ドライバー関数
- TrueType フォント ドライバー WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b85efd35685036a3a523bfcc4e331e739589103
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558252"
---
# <a name="truetype-font-driver-functions"></a>TrueType フォント ドライバー関数


## <span id="ddk_truetype_font_driver_functions_gg"></span><span id="DDK_TRUETYPE_FONT_DRIVER_FUNCTIONS_GG"></span>


TrueType フォント ドライバーでは、次の表に示す関数をサポートする必要があります。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556235" data-raw-source="[&lt;strong&gt;DrvGetTrueTypeFile&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556235)"><strong>DrvGetTrueTypeFile</strong></a></p></td>
<td align="left"><p>TrueType フォントのメモリ マップト ファイルへの GDI 効率的にアクセスを提供します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556269" data-raw-source="[&lt;strong&gt;DrvQueryTrueTypeOutline&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556269)"><strong>DrvQueryTrueTypeOutline</strong></a></p></td>
<td align="left"><p>Native TrueType 形式のグリフのハンドルを返します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556271" data-raw-source="[&lt;strong&gt;DrvQueryTrueTypeTable&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556271)"><strong>DrvQueryTrueTypeTable</strong></a></p></td>
<td align="left"><p>TrueType フォント ファイルの形式で特定のファイルに、GDI にアクセスします。</p></td>
</tr>
</tbody>
</table>

 

これらすべての関数は、TrueType フォント ファイルに関する情報を GDI を提供します。 *DrvQueryTrueTypeTable* TrueType フォント ファイルの形式で特定のテーブルに、GDI のアクセス権を付与する必要があります。 *DrvQueryTrueTypeOutline* TrueType のネイティブ形式で GDI グリフのアウトラインを送信する必要があります。 *DrvGetTrueTypeFile* GDI メモリに効率的にアクセスできるようにする、truetype フォント ドライバーのプライベートなエントリ ポイントには、TrueType フォント ファイルがマップされた GDI を返します。

 

 





