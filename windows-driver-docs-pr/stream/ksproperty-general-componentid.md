---
title: KSPROPERTY\_全般\_COMPONENTID
description: KSPROPERTY\_全般\_COMPONENTID プロパティは、省略可能なプロパティにより、クライアントは KSCOMPONENTID 構造体に格納されているコンポーネントの一般的な情報にアクセスします。
ms.assetid: fbbdf3f6-c71a-4a6d-ba15-ec7b7bdc1e0e
keywords:
- KSPROPERTY_GENERAL_COMPONENTID ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_GENERAL_COMPONENTID
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 866414c5c0ded0200ac59971e9425a57af2134c9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354819"
---
# <a name="kspropertygeneralcomponentid"></a>KSPROPERTY\_全般\_COMPONENTID


KSPROPERTY\_全般\_COMPONENTID プロパティが省略可能なプロパティに格納されているコンポーネントの一般的な情報にアクセスするクライアントを許可する、 [ **KSCOMPONENTID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kscomponentid)構造体。

## <span id="ddk_ksproperty_general_componentid_ks"></span><span id="DDK_KSPROPERTY_GENERAL_COMPONENTID_KS"></span>


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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kscomponentid" data-raw-source="[&lt;strong&gt;KSCOMPONENTID&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kscomponentid)"><strong>KSCOMPONENTID</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

[ **KSCOMPONENTID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kscomponentid)構造の GUID 値に含まれる**製造元**、**製品**、**コンポーネント**、および**名前**します。 ULONG の値が含まれている**バージョン**と**リビジョン**します。

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
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSCOMPONENTID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kscomponentid)

 

 






