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
ms.openlocfilehash: 2925b32deaf17d1f40a9bef4b34a44131078a13a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527216"
---
# <a name="kscategorybdaipsink"></a>KSCATEGORY_BDA_IP_SINK


KSCATEGORY_BDA_IP_SINK[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)でシンク フィルターの機能のカテゴリ (KS)、[ブロードキャスト ドライバー アーキテクチャ](https://msdn.microsoft.com/library/windows/hardware/ff556573)(性 BDA)。

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

詳細については、[BDA フィルター カテゴリ Guid](https://msdn.microsoft.com/library/windows/hardware/ff556521)を参照してください。

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

 

 





