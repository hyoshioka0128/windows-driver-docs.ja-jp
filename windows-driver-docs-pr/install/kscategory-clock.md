---
title: KSCATEGORY_CLOCK
description: KSCATEGORY_CLOCK
ms.assetid: 1a5afadd-f76f-4184-a93e-af82769ecc1b
keywords:
- KSCATEGORY_CLOCK デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_CLOCK
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5952e676bf68fb821d9b9ef745ec82c4d1dd02eb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384251"
---
# <a name="kscategoryclock"></a>KSCATEGORY_CLOCK


KSCATEGORY_CLOCK[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)クロック デバイスの機能のカテゴリ (KS)。

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
<td align="left"><p>KSCATEGORY_CLOCK</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{53172480-4791-11D0-A5D6-28DB04C10000}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS デバイス用のドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_CLOCK 機能カテゴリをサポートすることを示す KSCATEGORY_CLOCK のインスタンスを登録します。

カーネルのクロックのストリームの詳細については、次を参照してください。 [KS ミニドライバー アーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-minidriver-architecture)、 [KS クロック](https://docs.microsoft.com/windows-hardware/drivers/stream/ks-clocks)、および[AVStream クロック](https://docs.microsoft.com/windows-hardware/drivers/stream/avstream-clocks)します。

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
<td align="left">Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

 

 





