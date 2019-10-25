---
title: KSCATEGORY_BDA_RECEIVER_COMPONENT
description: KSCATEGORY_BDA_RECEIVER_COMPONENT
ms.assetid: f160662e-651c-444f-aa82-cfc73c19e41d
keywords:
- KSCATEGORY_BDA_RECEIVER_COMPONENT デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_BDA_RECEIVER_COMPONENT
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f3655ca89af5103eff28f8c236481b82bc023662
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828727"
---
# <a name="kscategory_bda_receiver_component"></a>KSCATEGORY_BDA_RECEIVER_COMPONENT


KSCATEGORY_BDA_RECEIVER_COMPONENT [device インターフェイスクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)は、 [broadcast driver architecture](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index) (BDA) の受信側の[kernel streaming](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2) (KS) 機能カテゴリに対して定義されています。

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
<td align="left"><p>KSCATEGORY_BDA_RECEIVER_COMPONENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{FD0A5AF4-B41D-11d2-9C95-00C04F7971E0}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

BDA デバイス用のドライバーは、デバイスが BDA レシーバーフィルターをサポートしていることをオペレーティングシステムに示す KSCATEGORY_BDA_RECEIVER_COMPONENT のインスタンスを登録します。

BDA レシーバーフィルターの KS 機能カテゴリの詳細については、「[コモンコントロールノードとフィルター](https://docs.microsoft.com/windows-hardware/drivers/stream/common-control-nodes-and-filters)」、「 [bda ミニドライバーの開始](https://docs.microsoft.com/windows-hardware/drivers/stream/starting-a-bda-minidriver)」、および「 [bda フィルターカテゴリ guid](https://docs.microsoft.com/windows-hardware/drivers/stream/bda-filter-category-guids)」を参照してください。

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

 

 





