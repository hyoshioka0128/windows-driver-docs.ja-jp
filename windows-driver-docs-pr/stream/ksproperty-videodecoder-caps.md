---
title: KSK プロパティ\_VIDEODECODER\_CAPS
description: '\_VIDEODECODER\_CAPS プロパティには、ビデオデコーダーの基本機能が記述されています。 このプロパティを実装する必要があります。'
ms.assetid: 8b252f36-911b-4f51-894d-3aae9aa9dfde
keywords:
- KSPROPERTY_VIDEODECODER_CAPS ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_VIDEODECODER_CAPS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9eeef2f2314ec7e34d249680b78f438d28d5b54d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837872"
---
# <a name="ksproperty_videodecoder_caps"></a>KSK プロパティ\_VIDEODECODER\_CAPS


\_VIDEODECODER\_CAPS プロパティには、ビデオデコーダーの基本機能が記述されています。 このプロパティを実装する必要があります。

## <span id="ddk_ksproperty_videodecoder_caps_ks"></span><span id="DDK_KSPROPERTY_VIDEODECODER_CAPS_KS"></span>


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
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい]</p></td>
<td><p>必須ではない</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_caps_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_CAPS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_caps_s)"><strong>KSPROPERTY_VIDEODECODER_CAPS_S</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_caps_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_VIDEODECODER_CAPS_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_caps_s)"><strong>KSPROPERTY_VIDEODECODER_CAPS_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は、サポートされている標準、時間の短縮、水平同期のパルスなど、ビデオデコーダーデバイスのハードウェア機能を指定する、VIDEODECODER\_CAPS\_S 構造体\_KSK プロパティです。ビデオデコーダーは、垂直同期期間中に生成されます。

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
<td>Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSK プロパティ\_VIDEODECODER\_CAPS\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_videodecoder_caps_s)

 

 






