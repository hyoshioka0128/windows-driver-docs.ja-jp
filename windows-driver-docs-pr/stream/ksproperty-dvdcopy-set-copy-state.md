---
title: KSPROPERTY\_DVDCOPY\_設定\_コピー\_状態
description: KSPROPERTY\_DVDCOPY\_設定\_コピー\_STATE プロパティは、DVD デコーダーのストリームのコピー状態を設定します。 このプロパティは、実装するために省略可能です。
ms.assetid: f4e46d79-c70b-413a-9702-a73d3776ee2c
keywords:
- KSPROPERTY_DVDCOPY_SET_COPY_STATE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_DVDCOPY_SET_COPY_STATE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0459fcb26a1fcc48325c9a0747707891b03b506
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368106"
---
# <a name="kspropertydvdcopysetcopystate"></a>KSPROPERTY\_DVDCOPY\_設定\_コピー\_状態


KSPROPERTY\_DVDCOPY\_設定\_コピー\_STATE プロパティは、DVD デコーダーのストリームのコピー状態を設定します。 このプロパティは、実装するために省略可能です。

## <span id="ddk_ksproperty_dvdcopy_set_copy_state_ks"></span><span id="DDK_KSPROPERTY_DVDCOPY_SET_COPY_STATE_KS"></span>


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
<td><p>〇</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ks_dvdcopy_set_copy_state" data-raw-source="[&lt;strong&gt;KS_DVDCOPY_SET_COPY_STATE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ks_dvdcopy_set_copy_state)"><strong>KS_DVDCOPY_SET_COPY_STATE</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、KS\_DVDCOPY\_設定\_コピー\_DVD デコーダー ストリームの著作権保護の状態を記述する状態の構造体。

<a name="remarks"></a>注釈
-------

このプロパティは、このピンに CSS 認証が必要かどうかを示します。 既定値があると見なされます、プロパティが実装されていない場合、 **KS\_DVDCOPYSTATE\_認証\_REQUIRED**値から、 [ **KS\_DVDCOPYSTATE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ks_dvdcopystate)列挙体。

このプロパティの主な用途は、複数の pin と同じ復号化をサポートするデコーダーのです。 たとえば、1 つのフィルターは、サブピクチャとビデオ デコーディングの両方を提供する場合、キーだけを 2 つの pin のいずれかの交換です。 フィルターを返す場合は、 **KS\_DVDCOPYSTATE\_認証\_いない\_REQUIRED**ピンのいずれかで、常に返す必要があります**KS\_DVDCOPYSTATE\_認証\_REQUIRED**プロパティに発行する最初の pin にします。

このプロパティとして発行するときに、**取得**呼び出し、フィルターは、いずれかを返すことが**KS\_DVDCOPYSTATE\_認証\_REQUIRED**または KS\_DVDCOPYSTATE\_認証\_いない\_必要な作業です。

このプロパティとして発行するときに、**設定**呼び出し、これを著作権保護のネゴシエーションのフェーズが入力されているかを示すハードウェア デコーダーによって使用情報の呼び出し。 デコーダーが、セットを保持できる\_新しい CSS キーが必要であることを示す、適切なビットが受信されるまでに、次のいずれかの状態します。

<span id="KS_DVDCOPYSTATE_INITIALIZE"></span><span id="ks_dvdcopystate_initialize"></span>**KS\_DVDCOPYSTATE\_INITIALIZE**  
ディスク キーのネゴシエーションのシーケンスの先頭を示します。

<span id="KS_DVDCOPYSTATE_INITIALIZE_TITLE"></span><span id="ks_dvdcopystate_initialize_title"></span>**KS\_DVDCOPYSTATE\_INITIALIZE\_TITLE**  
タイトルのキーのネゴシエーション シーケンスの先頭を示します。

<span id="KS_DVDCOPYSTATE_DONE"></span><span id="ks_dvdcopystate_done"></span>**KS\_DVDCOPYSTATE\_DONE**  
キーのネゴシエーションのシーケンスの完了を示します。

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
<td>Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KS\_DVDCOPY\_SET\_COPY\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ks_dvdcopy_set_copy_state)

[**KS\_DVDCOPYSTATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ks_dvdcopystate)

[DVD の著作権保護](https://docs.microsoft.com/windows-hardware/drivers/stream/dvd-copyright-protection)

[同じハードウェア上の複数のデータ ストリーム](https://docs.microsoft.com/windows-hardware/drivers/stream/multiple-data-streams-on-the-same-hardware)

[データ フローとキー交換の同期](https://docs.microsoft.com/windows-hardware/drivers/stream/synchronizing-key-exchange-with-data-flow)

 

 






