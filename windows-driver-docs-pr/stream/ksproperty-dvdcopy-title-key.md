---
title: KSPROPERTY\_DVDCOPY\_タイトル\_キー
description: KSPROPERTY\_DVDCOPY\_タイトル\_キー プロパティは、DVD 著作権保護の認証プロセスの現在のコンテンツからタイトル キー情報を取得します。
ms.assetid: 7c07bf75-cbc4-4319-a1a6-4f05d228d91a
keywords:
- KSPROPERTY_DVDCOPY_TITLE_KEY ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DVDCOPY_TITLE_KEY
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85370626318c1e961f76b378c555f33e0b8615b7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548780"
---
# <a name="kspropertydvdcopytitlekey"></a>KSPROPERTY\_DVDCOPY\_タイトル\_キー


KSPROPERTY\_DVDCOPY\_タイトル\_キー プロパティは、DVD 著作権保護の認証プロセスの現在のコンテンツからタイトル キー情報を取得します。

## <span id="ddk_ksproperty_dvdcopy_title_key_ks"></span><span id="DDK_KSPROPERTY_DVDCOPY_TITLE_KEY_KS"></span>


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
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567640" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_TITLEKEY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567640)"><strong>KS_DVDCOPY_TITLEKEY</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KS\_DVDCOPY\_タイトルの現在のキーを記述する TITLEKEY 構造体。

<a name="remarks"></a>注釈
-------

タイトルのキーの詳細については、次を参照してください。 [DVD 著作権保護](https://msdn.microsoft.com/library/windows/hardware/ff558736)します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KS\_DVDCOPY\_TITLEKEY**](https://msdn.microsoft.com/library/windows/hardware/ff567640)

 

 






