---
title: KSCATEGORY_TVTUNER
description: KSCATEGORY_TVTUNER
ms.assetid: 44d9d407-a94c-40de-b749-af50bc5718f4
keywords:
- KSCATEGORY_TVTUNER デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_TVTUNER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 78e5b04ccb3a57b1566fc5a785218ca88e8cc553
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380084"
---
# <a name="kscategorytvtuner"></a>KSCATEGORY_TVTUNER


KSCATEGORY_TVTUNER[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)テレビ チューナー デバイスの機能のカテゴリ (KS)。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">設定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>識別子</p></td>
<td align="left"><p>KSCATEGORY_TVTUNER</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{A799A800-A46D-11D0-A18C-00A02401DCD4}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS デバイス用のドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_TVTUNER 機能カテゴリをサポートすることを示す KSCATEGORY_TVTUNER のインスタンスを登録します。

INF ファイルでこの機能のカテゴリを登録する方法の例は、次を参照してください。、 *Bdan.inf* INF ファイルでのソフトウェアのチューナー サンプルに含まれている、 *src/swtuner/algtuner* WDK のディレクトリ。

ビデオ デバイスについては、次を参照してください。[ビデオ キャプチャ デバイス](https://msdn.microsoft.com/library/windows/hardware/ff568699)、[フィルターのグラフ例](https://msdn.microsoft.com/library/windows/hardware/ff559605)、および[エンコーダー デバイス](https://msdn.microsoft.com/library/windows/hardware/ff559535)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSCATEGORY_TVAUDIO**](kscategory-tvaudio.md)

 

 






