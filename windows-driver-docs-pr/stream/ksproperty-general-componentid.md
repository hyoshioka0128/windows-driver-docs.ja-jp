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
ms.openlocfilehash: 09b0907cebc3a4b08ac03471373c3690e2649566
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363992"
---
# <a name="kspropertygeneralcomponentid"></a>KSPROPERTY\_全般\_COMPONENTID


KSPROPERTY\_全般\_COMPONENTID プロパティが省略可能なプロパティに格納されているコンポーネントの一般的な情報にアクセスするクライアントを許可する、 [ **KSCOMPONENTID** ](https://msdn.microsoft.com/library/windows/hardware/ff561027)構造体。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561027" data-raw-source="[&lt;strong&gt;KSCOMPONENTID&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561027)"><strong>KSCOMPONENTID</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

[ **KSCOMPONENTID** ](https://msdn.microsoft.com/library/windows/hardware/ff561027)構造の GUID 値に含まれる**製造元**、**製品**、**コンポーネント**、および**名前**します。 ULONG の値が含まれている**バージョン**と**リビジョン**します。

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


[**KSCOMPONENTID**](https://msdn.microsoft.com/library/windows/hardware/ff561027)

 

 






