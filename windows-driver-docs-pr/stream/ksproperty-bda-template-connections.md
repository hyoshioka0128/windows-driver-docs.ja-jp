---
title: KSPROPERTY\_BDA\_テンプレート\_接続
description: クライアントを使用して、KSPROPERTY\_BDA\_テンプレート\_ピンとテンプレートのトポロジのノード間の接続の一覧を取得する接続。
ms.assetid: 59268751-34fd-4291-bf36-45a435a4ccf2
keywords:
- KSPROPERTY_BDA_TEMPLATE_CONNECTIONS ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_BDA_TEMPLATE_CONNECTIONS
api_location:
- Bdamedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96e6f0d2a57868707467aa795ddb6395622c7e59
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384279"
---
# <a name="kspropertybdatemplateconnections"></a>KSPROPERTY\_BDA\_テンプレート\_接続


クライアントを使用して、KSPROPERTY\_BDA\_テンプレート\_ピンとテンプレートのトポロジのノード間の接続の一覧を取得する接続。

## <span id="ddk_ksproperty_bda_template_connections_ks"></span><span id="DDK_KSPROPERTY_BDA_TEMPLATE_CONNECTIONS_KS"></span>


### <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>X</p></td>
<td><p>フィルター</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>BDA_TEMPLATE_CONNECTION</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

返された BDA\_テンプレート\_接続構造には、テンプレートのトポロジ内の接続がについて説明します。

Pin とテンプレートのトポロジのノード間の接続の一覧は、配列 bda\_テンプレート\_接続構造体。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Bdamedia.h (Bdamedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**BdaPropertyTemplateConnections**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdasup/nf-bdasup-bdapropertytemplateconnections)

[**BDA\_テンプレート\_接続**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdatypes/ns-bdatypes-_bda_template_connection)

[**KSPIN\_記述子\_例**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin_descriptor_ex)

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 






