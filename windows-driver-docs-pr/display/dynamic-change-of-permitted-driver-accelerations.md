---
title: 許可されたドライバー アクセラレータの動的変更
description: 許可されたドライバー アクセラレータの動的変更
ms.assetid: a80bb755-f4ff-4d5d-aff1-28f8262061ae
keywords:
- 高速化レベル WDK Windows 2000 を表示します。
- ドライバー WDK Windows 2000 のアクセラレータの表示
- コントロール パネルのスライダー コントロール WDK Windows 2000 の表示
- GDI の高速化変更 WDK Windows 2000 を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7dc372788775254e965fa3c38e8a80f5cda4ab37
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327941"
---
# <a name="dynamic-change-of-permitted-driver-accelerations"></a>許可されたドライバー アクセラレータの動的変更


## <span id="ddk_dynamic_change_of_permitted_driver_accelerations_gg"></span><span id="DDK_DYNAMIC_CHANGE_OF_PERMITTED_DRIVER_ACCELERATIONS_GG"></span>


ドライバーの高速化のレベルは、コントロール パネルの [表示] アイコンをクリックして生成されるスライダーを使用して、ユーザー インターフェイスで変更できます。 このスライダーで設定された値、によっては、GDI は、ドライバーのアクセラレータの次の表に示すは、次のレベルをできます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">値</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>すべてのディスプレイ ドライバー アクセラレーションが許可されます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556289" data-raw-source="[&lt;strong&gt;DrvSetPointerShape&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556289)"><strong>DrvSetPointerShape</strong> </a>と<a href="https://msdn.microsoft.com/library/windows/hardware/ff556185" data-raw-source="[&lt;strong&gt;DrvCreateDeviceBitmap&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556185)"> <strong>DrvCreateDeviceBitmap</strong> </a>は無効になります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>だけでなく、1 より高度なディスプレイ ドライバーのアクセラレータが許可されないなど<a href="https://msdn.microsoft.com/library/windows/hardware/ff556302" data-raw-source="[&lt;strong&gt;DrvStretchBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556302)"> <strong>DrvStretchBlt</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556220" data-raw-source="[&lt;strong&gt;DrvFillPath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556220)"> <strong>DrvFillPath</strong> </a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556236" data-raw-source="[&lt;strong&gt;DrvGradientFill&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556236)"> <strong>DrvGradientFill</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556245" data-raw-source="[&lt;strong&gt;DrvLineTo&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556245)"> <strong>DrvLineTo</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556176" data-raw-source="[&lt;strong&gt;DrvAlphaBlend&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556176)"> <strong>DrvAlphaBlend</strong></a>、および<a href="https://msdn.microsoft.com/library/windows/hardware/ff557283" data-raw-source="[&lt;strong&gt;DrvTransparentBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557283)"> <strong>DrvTransparentBlt</strong></a>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>2、だけでなく、DirectDraw、Direct3D アクセラレータをすべてが許可されていません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>3、だけでなくほぼすべてのディスプレイ ドライバーの加速度は許可されません、塗りつぶしの純色、を除き<a href="https://msdn.microsoft.com/library/windows/hardware/ff556182" data-raw-source="[&lt;strong&gt;DrvCopyBits&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556182)"> <strong>DrvCopyBits</strong></a>、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff557277" data-raw-source="[&lt;strong&gt;DrvTextOut&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff557277)"> <strong>DrvTextOut</strong> </a>、および<a href="https://msdn.microsoft.com/library/windows/hardware/ff556316" data-raw-source="[&lt;strong&gt;DrvStrokePath&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556316)"> <strong>DrvStrokePath</strong></a>します。 <a href="https://msdn.microsoft.com/library/windows/hardware/ff556217" data-raw-source="[&lt;strong&gt;DrvEscape&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556217)"><strong>DrvEscape</strong> </a>は無効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p>5</p></td>
<td align="left"><p>ハードウェア アクセラレーションは許可されません。 ドライバーは、システム メモリの画面から、画面へのビット ブロック転送を実行するのみ呼び出されます。</p></td>
</tr>
</tbody>
</table>

 

ディスプレイ ドライバーによって現在の高速化のレベルを特定できます。

-   実装することによって、GDI から高速化のレベルに変更の通知を受信[ **DrvNotify**](https://msdn.microsoft.com/library/windows/hardware/ff556252)します。

-   呼び出す[ **EngQueryDeviceAttribute** ](https://msdn.microsoft.com/library/windows/hardware/ff564986)を現在の高速化のレベルを照会します。

 

 





