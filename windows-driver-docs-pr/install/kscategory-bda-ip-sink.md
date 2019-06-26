---
title: KSCATEGORY_BDA_IP_SINK
description: KSCATEGORY_BDA_IP_SINK
ms.assetid: 7c9627b3-2d6b-471c-9101-0768890bfe10
keywords:
- KSCATEGORY_BDA_IP_SINK デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_BDA_IP_SINK
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c01736dbe080ec7abc90fd6d5a45835d6db426bd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353387"
---
# <a name="kscategorybdaipsink"></a>KSCATEGORY_BDA_IP_SINK


KSCATEGORY_BDA_IP_SINK[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)でシンク フィルターの機能のカテゴリ (KS)、[ブロードキャスト ドライバー アーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_stream/index)(性 BDA)。

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
<td align="left"><p>KSCATEGORY_BDA_IP_SINK</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{71985F4A-1CA1-11d3-9CC8-00C04F7971E0}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

BDA デバイス用のドライバーでは、デバイスがシンク BDA IP フィルターをサポートすることを示す KSCATEGORY_BDA_IP_SINK のインスタンスを登録します。

詳細については、次を参照してください。 [BDA フィルター カテゴリ Guid](https://docs.microsoft.com/windows-hardware/drivers/stream/bda-filter-category-guids)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Server 2003、Windows XP、DirectX 9.0 a がインストールされている、Windows 2000 および以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Bdamedia.h (Bdamedia.h を含む)</td>
</tr>
</tbody>
</table>

 

 





