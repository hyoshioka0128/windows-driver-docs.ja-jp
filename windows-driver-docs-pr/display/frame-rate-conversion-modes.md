---
title: フレーム レート変換モード
description: フレーム レート変換モード
ms.assetid: cbb609b5-6021-4f47-855d-24882533a7a0
keywords:
- フレーム レート変換 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e76a69528af4e9c8cfd84e27134db2a0185ad2da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549164"
---
# <a name="frame-rate-conversion-modes"></a>フレーム レート変換モード


## <span id="ddk_frame_rate_conversion_modes_gg"></span><span id="DDK_FRAME_RATE_CONVERSION_MODES_GG"></span>


DDI によってサポートされることがあるフレーム レート変換モードの例を次に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Mode</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>フレームの繰り返し/削除</p></td>
<td align="left"><p>宛先表面に、選択したソースのサンプルをコピーすることで余分なメモリを使用しているため、推奨されるモードはありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>テンポラルの線形補間</p></td>
<td align="left"><p>将来と前の参照フィールドは、アルファ ブレンドして新しいフレームを生成します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>動きベクトルを送る</p></td>
<td align="left"><p>シーン内の別のオブジェクトの動きベクトルは、補間に行われる前に個々 の動きを時間軸を整列に使用されます。</p></td>
</tr>
</tbody>
</table>

 

 

 





