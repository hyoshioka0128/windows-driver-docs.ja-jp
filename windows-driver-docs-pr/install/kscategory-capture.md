---
title: KSCATEGORY_CAPTURE
description: KSCATEGORY_CAPTURE
ms.assetid: b33e9a04-00f2-4cfa-911e-55461ce5aae7
keywords:
- KSCATEGORY_CAPTURE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_CAPTURE
api_location:
- Ks.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a0fe40612ad4d3b9092f3185287fa4bdb70fbdaf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556734"
---
# <a name="kscategorycapture"></a>KSCATEGORY_CAPTURE


KSCATEGORY_CAPTURE[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)wave または MIDI データ ストリームをキャプチャする (KS) 機能のカテゴリ。

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
<td align="left"><p>KSCATEGORY_CAPTURE</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{65E8773D-8F56-11D0-A3B9-00A0C9223196}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS デバイス用のドライバーでは、デバイスが KSCATEGORY_CAPTURE 機能カテゴリをサポートすることを示す KSCATEGORY_CAPTURE のインスタンスを登録します。

INF ファイルでこの機能のカテゴリを登録する方法については、次を参照してください。、 *Ac97smpl.inf* INF ファイルに含まれている、 [AC'97 サンプル ドライバー](https://go.microsoft.com/fwlink/p/?linkid=256075) WDK で提供されています。

オーディオのアダプターのインターフェイス クラスのデバイスについては、[オーディオのアダプターのデバイスのインターフェイスをインストールする](https://msdn.microsoft.com/library/windows/hardware/ff536813)を参照してください。

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

 

 





