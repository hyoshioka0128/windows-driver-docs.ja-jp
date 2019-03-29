---
title: ディスプレイ ドライバーの条件的に必須の関数
description: ディスプレイ ドライバーの条件的に必須の関数
ms.assetid: c2de7e48-2ce6-466f-947e-bdac1d4fe422
keywords:
- グラフィックス DDI 関数 WDK Windows 2000 を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 941ba5b6c0714059ef8c94f32bfafb2d5b23779e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581318"
---
# <a name="conditionally-required-display-driver-functions"></a>ディスプレイ ドライバーの条件的に必須の関数


## <span id="ddk_conditionally_required_display_driver_functions_gg"></span><span id="DDK_CONDITIONALLY_REQUIRED_DISPLAY_DRIVER_FUNCTIONS_GG"></span>


ドライバーの実装方法や、基になるアダプターの機能に基づいて、その他のグラフィックス DDI 関数が必要な場合があります。 たとえば、ドライバーは、独自のサーフェイスを管理している場合 (を使用して[ **EngCreateDeviceSurface** ](https://msdn.microsoft.com/library/windows/hardware/ff564206)サーフェスを識別するハンドルを取得する)、ドライバーをする必要がありますには、少なくとも、次はサポート[描画関数](optional-display-driver-functions.md):

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556182" data-raw-source="[&lt;strong&gt;DrvCopyBits&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556182)"><strong>DrvCopyBits</strong></a></p></td>
<td align="left"><p>デバイスで管理されたラスター サーフェスと GDI 標準形式のビットマップを変換します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556316" data-raw-source="[&lt;strong&gt;DrvStrokePath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556316)"><strong>DrvStrokePath</strong></a></p></td>
<td align="left"><p>ときに (曲線または行) パスを描画する GDI によって呼び出されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff557277" data-raw-source="[&lt;strong&gt;DrvTextOut&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557277)"><strong>DrvTextOut</strong></a></p></td>
<td align="left"><p>指定した位置にあるグリフのセットを表示します。</p></td>
</tr>
</tbody>
</table>

 

**注**  ドライバー呼び出しが特定のサーフェイスで任意のシリアル化します。

 

ドライバーの標準フォーマットへの書き込みを*Dib*通常これらの操作のほとんどまたはすべてを管理する GDI を許可します。 表示をサポートする*設定可能なパレット*をサポートする必要があります、 [ **DrvSetPalette** ](https://msdn.microsoft.com/library/windows/hardware/ff556282)関数。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556282" data-raw-source="[&lt;strong&gt;DrvSetPalette&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556282)"><strong>DrvSetPalette</strong></a></p></td>
<td align="left"><p>ドライバーが指定したデバイスのパレットを認識する要求。 ドライバーは、特定のパレット内のエントリをできるだけ一致するようにハードウェアのパレットを設定します。</p></td>
</tr>
</tbody>
</table>

 

グラフィック ドライバーをすべての条件付きで必要な関数の一覧が表示されます。[条件付きでの必要なグラフィックス ドライバー関数](conditionally-required-graphics-driver-functions.md)します。

 

 





