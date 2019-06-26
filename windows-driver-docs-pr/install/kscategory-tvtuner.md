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
ms.openlocfilehash: 3374f175c2d5fe9e14222fd41ffd59a91e2f9d7b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385543"
---
# <a name="kscategorytvtuner"></a>KSCATEGORY_TVTUNER


KSCATEGORY_TVTUNER[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)テレビ チューナー デバイスの機能のカテゴリ (KS)。

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

ビデオ デバイスについては、次を参照してください。[ビデオ キャプチャ デバイス](https://docs.microsoft.com/windows-hardware/drivers/stream/video-capture-devices)、[フィルターのグラフ例](https://docs.microsoft.com/windows-hardware/drivers/stream/filter-graph-examples)、および[エンコーダー デバイス](https://docs.microsoft.com/windows-hardware/drivers/stream/encoder-devices)します。

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

 

 






