---
title: KSCATEGORY_QUALITY
description: KSCATEGORY_QUALITY
ms.assetid: fc23e069-b514-41a3-b3c2-c65b35b2e431
keywords:
- KSCATEGORY_QUALITY デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_QUALITY
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: acfc5b26c1abe035bba17c0216327d7affda0cf1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354998"
---
# <a name="kscategoryquality"></a>KSCATEGORY_QUALITY


KSCATEGORY_QUALITY[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)品質管理の機能のカテゴリ (KS)。

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
<td align="left"><p>KSCATEGORY_QUALITY</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{97EBAACB-95BD-11D0-A3EA-00A0C9223196}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS デバイス用のドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_QUALITY 機能カテゴリをサポートすることを示す KSCATEGORY_QUALITY のインスタンスを登録します。

詳細については、次を参照してください。[品質管理](https://docs.microsoft.com/windows-hardware/drivers/stream/quality-management)します。

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

 

 





