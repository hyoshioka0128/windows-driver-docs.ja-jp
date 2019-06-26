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
ms.openlocfilehash: 601fcc7aafa24d14c16a14beeaaeccbc9e94f20f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384259"
---
# <a name="kscategorybdareceivercomponent"></a>KSCATEGORY_BDA_RECEIVER_COMPONENT


KSCATEGORY_BDA_RECEIVER_COMPONENT[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)(KS) で受信側の機能のカテゴリ、[ブロードキャストのドライバーのアーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_stream/index) (性 BDA)。

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

BDA デバイス用のドライバーでは、オペレーティング システムに、デバイスが BDA 受信者フィルターをサポートすることを示す KSCATEGORY_BDA_RECEIVER_COMPONENT のインスタンスを登録します。

KS 機能のカテゴリの詳細についての BDA 受信者フィルターを参照してください[一般的なコントロールのノードとフィルター](https://docs.microsoft.com/windows-hardware/drivers/stream/common-control-nodes-and-filters)、 [BDA ミニドライバーを開始](https://docs.microsoft.com/windows-hardware/drivers/stream/starting-a-bda-minidriver)、および[BDA フィルター カテゴリ Guid](https://docs.microsoft.com/windows-hardware/drivers/stream/bda-filter-category-guids)。

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
<td align="left"><p>Windows XP、DirectX 9.0 a がインストールされている、Windows 2000 以降のバージョンの Windows で使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Bdamedia.h (Bdamedia.h を含む)</td>
</tr>
</tbody>
</table>

 

 





