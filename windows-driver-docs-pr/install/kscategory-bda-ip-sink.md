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
ms.openlocfilehash: ab5ac8acc4332f3dc371f4c627a65430744719a0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828781"
---
# <a name="kscategory_bda_ip_sink"></a>KSCATEGORY_BDA_IP_SINK


KSCATEGORY_BDA_IP_SINK [device インターフェイスクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)は、 [broadcast driver architecture](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index) (BDA) のシンクフィルタの[kernel streaming](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2) (KS) 機能カテゴリに対して定義されています。

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

BDA デバイス用ドライバーは、デバイスが BDA IP シンクフィルターをサポートしていることを示すために、KSCATEGORY_BDA_IP_SINK のインスタンスを登録します。

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
<td align="left"><p>Windows Server 2003、Windows XP、Windows 2000 (DirectX 9.0 がインストールされている)、およびそれ以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Bdamedia (Bdamedia を含む)</td>
</tr>
</tbody>
</table>

 

 





