---
title: KSCATEGORY_BDA_NETWORK_PROVIDER
description: KSCATEGORY_BDA_NETWORK_PROVIDER
ms.assetid: a73f7ea3-19bf-4328-a96f-f28ee91db242
keywords:
- KSCATEGORY_BDA_NETWORK_PROVIDER デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_BDA_NETWORK_PROVIDER
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f461d35f8d7291fea7b0d3eb739414ffdc0b4b12
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366720"
---
# <a name="kscategorybdanetworkprovider"></a>KSCATEGORY_BDA_NETWORK_PROVIDER


KSCATEGORY_BDA_NETWORK_PROVIDER[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)(KS) でのネットワーク プロバイダーの機能のカテゴリ、[ブロードキャスト ドライバーアーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_stream/index)(性 BDA)。

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
<td align="left"><p>KSCATEGORY_BDA_NETWORK_PROVIDER</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{71985F4B-1CA1-11d3-9CC8-00C04F7971E0}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

BDA デバイス用のドライバーでは、オペレーティング システムに、デバイスが BDA ネットワーク プロバイダー フィルターをサポートすることを示す KSCATEGORY_BDA_NETWORK_PROVIDER のインスタンスを登録します。

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
<td align="left"><p>Windows XP および Windows の以降のバージョンで使用できます。 DirectX 9.0 a がインストールされている Windows 2000 で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Bdamedia.h (Bdamedia.h を含む)</td>
</tr>
</tbody>
</table>

 

 





