---
title: KSK プロパティ\_SYSAUDIO\_コンポーネント\_ID
description: KSK プロパティ\_SYSAUDIO\_COMPONENT\_ID プロパティは、指定された仮想オーディオデバイスが使用する wave レンダリングデバイスからコンポーネント ID を取得します。
ms.assetid: ef4a940f-dfef-43ed-8895-d318fb603e5c
keywords:
- KSPROPERTY_SYSAUDIO_COMPONENT_ID オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_SYSAUDIO_COMPONENT_ID
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: da6fc58e40e98855adb888b9be714de6140ab3a9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830487"
---
# <a name="ksproperty_sysaudio_component_id"></a>KSK プロパティ\_SYSAUDIO\_コンポーネント\_ID


KSK プロパティ\_SYSAUDIO\_COMPONENT\_ID プロパティは、指定された仮想オーディオデバイスが使用する wave レンダリングデバイスからコンポーネント ID を取得します。

## <span id="ddk_ksproperty_sysaudio_component_id_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_COMPONENT_ID_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">[購入]</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>[はい]</p></td>
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/previous-versions/ff564262(v=vs.85)" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))"><strong>KSK プロパティ</strong></a>+ ULONG</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kscomponentid" data-raw-source="[&lt;strong&gt;KSCOMPONENTID&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kscomponentid)"><strong>KSCOMPONENTID</strong></a></p></td>
</tr>
</tbody>
</table>

 

プロパティ記述子 (インスタンスデータ) は、KSK プロパティ型の構造であり、その後に仮想オーディオデバイスを識別するデバイス ID を含む ULONG 変数が続きます。 SysAudio が*n 個*の仮想オーディオデバイスを列挙する場合 (「 [**KSK プロパティ\_SYSAUDIO\_デバイス\_数**](ksproperty-sysaudio-device-count.md))」を参照してください。有効なデバイス id の範囲は 0 ~ *n*-1 です。

プロパティ値 (操作データ) は、指定された仮想オーディオデバイスによって使用される wave レンダリングデバイスに関する製造元、製品、およびその他のハードウェア固有の情報を指定する KSCOMPONENTID 型の構造体です。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

SYSAUDIO\_コンポーネント\_ID プロパティ要求\_KSK プロパティは、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

DirectSound は、SysAudio の仮想オーディオデバイスの基礎となるオーディオハードウェアのミニポートドライバーと直接通信しません。 そのため、DirectSound は、そのコンポーネント ID 情報について、wave レンダリングデバイスを直接照会することができません。 SYSAUDIO\_コンポーネント\_ID プロパティ\_KSK プロパティは、この情報を SysAudio 経由で間接的に取得するための DirectSound の手段を提供します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia .h (Ksk を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))

[**KSCOMPONENTID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kscomponentid)

[**KSK プロパティ\_SYSAUDIO\_デバイス\_数**](ksproperty-sysaudio-device-count.md)

 

 






