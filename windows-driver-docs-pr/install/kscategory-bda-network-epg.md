---
title: KSCATEGORY_BDA_NETWORK_EPG
description: KSCATEGORY_BDA_NETWORK_EPG
ms.assetid: 70a02c74-f092-4d1b-bf35-392da5c4fcb6
keywords:
- KSCATEGORY_BDA_NETWORK_EPG デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_BDA_NETWORK_EPG
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1db89acde8da9e7bf76785769b4d2eac45179510
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580904"
---
# <a name="kscategorybdanetworkepg"></a>KSCATEGORY_BDA_NETWORK_EPG


KSCATEGORY_BDA_NETWORK_EPG[デバイス インターフェイス クラス](https://msdn.microsoft.com/library/windows/hardware/ff541339)が定義されている、[カーネル ストリーミング](https://msdn.microsoft.com/library/windows/hardware/ff568277)(KS) で、電子番組ガイド (EPG) の機能のカテゴリ、[ブロードキャスト ドライバーアーキテクチャ](https://msdn.microsoft.com/library/windows/hardware/ff556573)(性 BDA)。

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
<td align="left"><p>KSCATEGORY_BDA_NETWORK_EPG</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{71985F49-1CA1-11d3-9CC8-00C04F7971E0}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>コメント
-------

BDA デバイス用のドライバーでは、デバイスが BDA EPG フィルターをサポートしているオペレーティング システムに示すために KSCATEGORY_BDA_NETWORK_EPG のインスタンスを登録します。

詳細については、[BDA フィルター カテゴリ Guid](https://msdn.microsoft.com/library/windows/hardware/ff556521)を参照してください。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows XP、DirectX 9.0 a がインストールされている、Windows 2000 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Bdamedia.h (Bdamedia.h を含む)</td>
</tr>
</tbody>
</table>

 

 





