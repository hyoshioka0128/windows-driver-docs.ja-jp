---
title: KSK プロパティ\_PIN\_PROPOSEDATAFORMAT
description: クライアントは、KSK プロパティ\_ピン留め\_PROPOSEDATAFORMAT プロパティを使用して、pin ファクトリによってインスタンス化された pin が特定のデータ形式をサポートしているかどうかを判断します。
ms.assetid: f1657fd1-0988-48b8-95d0-c6026965848b
keywords:
- KSPROPERTY_PIN_PROPOSEDATAFORMAT ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_PROPOSEDATAFORMAT
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 12/28/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8335ad13571e10391acc240298eba3e597b9b0c3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838842"
---
# <a name="ksproperty_pin_proposedataformat"></a>KSK プロパティ\_PIN\_PROPOSEDATAFORMAT


クライアントは、KSK プロパティ\_ピン留め\_PROPOSEDATAFORMAT プロパティを使用して、pin ファクトリによってインスタンス化された pin が特定のデータ形式をサポートしているかどうかを判断します。

## <span id="ddk_ksproperty_pin_proposedataformat_ks"></span><span id="DDK_KSPROPERTY_PIN_PROPOSEDATAFORMAT_KS"></span>


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
<td><p>[はい]</p></td>
<td><p>フィルター</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)"><strong>KSDATAFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSPROPERTY_PIN_PROPOSEDATAFORMAT には、提案されたデータ形式を指定する KSDATAFORMAT 型の構造体が含まれています。 このプロパティは、KSP_PIN を使用して指定します。この場合、メンバーは関連するピンファクトリを指定します。

KSK プロパティ\_PIN\_PROPOSEDATAFORMAT には、提案されたデータ形式を指定する[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)型の構造が含まれています。

[**Ksk プロパティ\_型\_GET**](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)は、windows 7 以降のバージョンの windows でサポートされています。 Windows Vista **Ksk プロパティ\_型\_GET**はサポートされ*ていません*。 

**KSPROPERTY_TYPE_GET**このプロパティを使用すると、オーディオドライバーは pin の既定のデータ形式に関する情報を提供できます。 **KSPROPERTY_TYPE_GET**は、ドライバーが[**KSEVENT_PINCAPS_FORMATCHANGE**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksevent-pincaps-formatchange)をサポートしていない限り、このプロパティに対してを実装することはできません。 
 

このプロパティを KSPROPERTY_TYPE_SET と共に使用すると、KS フィルターは STATUS\_SUCCESS を返します。これは、提案されたデータ形式で pin を設定したり、開いたりすることができます。 Pin を提案されたデータ形式に設定できない場合は、STATUS_NO_MATCH が返されます。 その他のエラーについては、適切なエラーが返されます。 ドライバーが[**KSPROPERTY_AUDIOSIGNALPROCESSING_MODES**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audiosignalprocessing-modes)をサポートしている場合、このプロパティは、いずれかのオーディオシグナル処理モードでサポートされている場合、STATUS_SUCCESS を返す必要があります。 


このプロパティで KSPROPERTY_TYPE_SET を使用しても、実際にはデータ形式は変更されません。 クライアントは、 [**Ksk プロパティ\_接続\_DATAFORMAT**](ksproperty-connection-dataformat.md)を使用して、データ形式を変更します。 **KSPROPERTY_TYPE_SET**は省略可能で、このプロパティに対してを実装します。


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
<td>Ks (Ks を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_ピン留め**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)
 
[**KSEVENT_PINCAPS_FORMATCHANGE**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksevent-pincaps-formatchange)

[**KS Caching**](https://docs.microsoft.com/en-us/windows-hardware/drivers/stream/ks-properties)

[**KSK プロパティ\_TYPE\_GET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)
 
[**KSPROPERTY_AUDIOSIGNALPROCESSING_MODES**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audiosignalprocessing-modes)





