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
ms.openlocfilehash: ba9dac2aaae838a4cbae58592b136c5612dfbb11
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366710"
---
# <a name="kscategorybdanetworktuner"></a>KSCATEGORY_BDA_NETWORK_TUNER


KSCATEGORY_BDA_NETWORK_TUNER[デバイス インターフェイス クラス](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)が定義されている、[カーネル ストリーミング](https://docs.microsoft.com/windows-hardware/drivers/stream/streaming-minidrivers2)でネットワーク チューナー (KS) 機能のカテゴリ、[ブロードキャストのドライバーのアーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_stream/index) (性 BDA)。

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

BDA デバイス用のドライバーでは、オペレーティング システムに、デバイスが BDA ネットワーク チューナー フィルターをサポートすることを示す KSCATEGORY_BDA_NETWORK_TUNER のインスタンスを登録します。

INF ファイルでこの機能のカテゴリを登録する方法の例は、INF ファイルを参照してください。 *BDASwTunerATSC.inf*します。 *BDASwTunerATSC.inf*で BDA サンプルの汎用的なチューナーに含まれている、 *src\\swtuner\\BDAtuner\\gentuner* WDK のサブディレクトリ。

ネットワークのチューナー フィルター KS 機能のカテゴリの詳細については、次を参照してください。[一般的なコントロールのノードとフィルター](https://docs.microsoft.com/windows-hardware/drivers/stream/common-control-nodes-and-filters)と[BDA フィルター カテゴリ Guid](https://docs.microsoft.com/windows-hardware/drivers/stream/bda-filter-category-guids)します。

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

 

 





