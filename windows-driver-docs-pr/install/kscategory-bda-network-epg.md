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
ms.openlocfilehash: 208952b75db421324bd981882ce816195ae91426
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828764"
---
# <a name="kscategory_bda_network_epg"></a>KSCATEGORY_BDA_NETWORK_EPG


KSCATEGORY_BDA_NETWORK_EPG [device インターフェイスクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)は、 [broadcast driver architecture](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index) (BDA) の電子番組ガイド (EPG) の[kernel streaming](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2) (KS) 機能カテゴリに対して定義されています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">備わっている</th>
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

 

<a name="remarks"></a>注釈
-------

BDA デバイス用ドライバーは、デバイスが BDA EPG フィルターをサポートしていることをオペレーティングシステムに示すために、KSCATEGORY_BDA_NETWORK_EPG のインスタンスを登録します。

詳細については、「 [BDA フィルターカテゴリ guid](https://docs.microsoft.com/windows-hardware/drivers/stream/bda-filter-category-guids)」を参照してください。

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
<td align="left"><p>Windows XP、Windows 2000 (DirectX 9.0 がインストールされている)、およびそれ以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Bdamedia (Bdamedia を含む)</td>
</tr>
</tbody>
</table>

 

 





