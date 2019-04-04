---
title: KSCATEGORY_MULTIPLEXER
description: KSCATEGORY_MULTIPLEXER
ms.assetid: 3023769a-9b98-4c12-90b1-f83294a45ab0
keywords:
- KSCATEGORY_MULTIPLEXER デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_MULTIPLEXER
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ba54a090e39a5c976b8432f8ac5f93cc388fcc55
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550768"
---
# <a name="kscategorymultiplexer"></a>KSCATEGORY_MULTIPLEXER


KSCATEGORY_MULTIPLEXER[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)マルチプレクサーのデバイスの機能のカテゴリ (KS)。

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
<td align="left"><p>KSCATEGORY_MULTIPLEXER</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{7A5DE1D3-01A1-452c-B481-4FA2B96271E8}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS デバイス用のドライバーでは、オペレーティング システムに、デバイスが KSCATEGORY_MULTIPLEXER 機能カテゴリをサポートすることを示す KSCATEGORY_MULTIPLEXER のインスタンスを登録します。

INF ファイルでこの機能のカテゴリを登録する方法の例は、次を参照してください。、 *Bdan.inf* INF ファイルでのソフトウェアのチューナー サンプルに含まれている、 *src/swtuner/algtuner* WDK のディレクトリ。

Multiplexers については、[トポロジ フィルター](https://msdn.microsoft.com/library/windows/hardware/ff538552)を参照してください。

KSCATEGORY_MULTIPLEXER 機能のカテゴリの詳細については、[エンコーダーのインストールと登録](https://msdn.microsoft.com/library/windows/hardware/ff559551)を参照してください。

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

 

 





