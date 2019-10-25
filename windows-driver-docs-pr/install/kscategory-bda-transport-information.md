---
title: KSCATEGORY_BDA_TRANSPORT_INFORMATION
description: KSCATEGORY_BDA_TRANSPORT_INFORMATION
ms.assetid: 0af3159c-8c44-4c42-8141-944bb734623c
keywords:
- KSCATEGORY_BDA_TRANSPORT_INFORMATION デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_BDA_TRANSPORT_INFORMATION
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8b9afac2662c6f043bdc6ba1ff605473e8260e38
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837445"
---
# <a name="kscategory_bda_transport_information"></a>KSCATEGORY_BDA_TRANSPORT_INFORMATION


KSCATEGORY_BDA_TRANSPORT_INFORMATION [device インターフェイスクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)は、 [broadcast driver architecture](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index) (BDA) でのトランスポート情報フィルター (TIF) の[カーネルストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)(KS) 機能カテゴリに対して定義されています。

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
<td align="left"><p>KSCATEGORY_BDA_TRANSPORT_INFORMATION</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{A2E3074F-6C3D-11d3-B653-00C04F79498E}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

BDA デバイス用のドライバーは、デバイスが BDA トランスポート情報フィルターをサポートしていることをオペレーティングシステムに示すために、KSCATEGORY_BDA_TRANSPORT_INFORMATION のインスタンスを登録します。

BDA トランスポート情報フィルターの KS 機能カテゴリの詳細については、「 [Bda フィルターカテゴリ guid](https://docs.microsoft.com/windows-hardware/drivers/stream/bda-filter-category-guids)」を参照してください。

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

 

 





