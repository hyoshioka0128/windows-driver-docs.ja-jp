---
title: KSCATEGORY_BDA_NETWORK_TUNER
description: KSCATEGORY_BDA_NETWORK_TUNER
ms.assetid: d3f9d393-c8a1-4280-8796-a1de755f9508
keywords:
- KSCATEGORY_BDA_NETWORK_TUNER デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- KSCATEGORY_BDA_NETWORK_TUNER
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 117cd1684637f8c5d299aafe64c2f3a890c90a85
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837454"
---
# <a name="kscategory_bda_network_tuner"></a>KSCATEGORY_BDA_NETWORK_TUNER


KSCATEGORY_BDA_NETWORK_TUNER [device インターフェイスクラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)は、[ブロードキャストドライバーアーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/ddi/_stream/index)(BDA) のネットワークチューナーの[カーネルストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)(KS) 機能カテゴリに対して定義されています。

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
<td align="left"><p>KSCATEGORY_BDA_NETWORK_TUNER</p></td>
</tr>
<tr class="even">
<td align="left"><p>クラス GUID</p></td>
<td align="left"><p>{71985F48-1CA1-11d3-9CC8-00C04F7971E0}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

BDA デバイス用のドライバーは、デバイスが BDA ネットワークチューナーフィルターをサポートしていることをオペレーティングシステムに示すために、KSCATEGORY_BDA_NETWORK_TUNER のインスタンスを登録します。

この機能カテゴリを INF ファイルに登録する方法の例については、INF ファイル*BDASwTunerATSC*を参照してください。 *BDASwTunerATSC*は、 *BDAtuner の src\\Swtuner\\\\gentuner*サブディレクトリにある BDA サンプル汎用チューナーに含まれています。

ネットワークチューナーフィルターの KS 機能カテゴリの詳細については、「[コモンコントロールノードとフィルター](https://docs.microsoft.com/windows-hardware/drivers/stream/common-control-nodes-and-filters)および[BDA フィルターカテゴリ guid](https://docs.microsoft.com/windows-hardware/drivers/stream/bda-filter-category-guids)」を参照してください。

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

 

 





