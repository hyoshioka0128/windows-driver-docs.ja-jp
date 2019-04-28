---
title: KSPROPERTY\_PIN\_PROPOSEDATAFORMAT
description: クライアントの使用、KSPROPERTY\_PIN\_PROPOSEDATAFORMAT プロパティ ピンをピン留めするファクトリをインスタンス化されますが、特定のデータ形式をサポートするかどうかを判断します。
ms.assetid: f1657fd1-0988-48b8-95d0-c6026965848b
keywords:
- KSPROPERTY_PIN_PROPOSEDATAFORMAT ストリーミング メディア デバイス
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
ms.openlocfilehash: 8e6976f513c795a58600894cf8a3cc483bcbdcc9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380806"
---
# <a name="kspropertypinproposedataformat"></a>KSPROPERTY\_PIN\_PROPOSEDATAFORMAT


クライアントの使用、KSPROPERTY\_PIN\_PROPOSEDATAFORMAT プロパティ ピンをピン留めするファクトリをインスタンス化されますが、特定のデータ形式をサポートするかどうかを判断します。

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
<td><p>フィルター</p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566722" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566722)"><strong>KSP_PIN</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff561656" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff561656)"><strong>KSDATAFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KSPROPERTY_PIN_PROPOSEDATAFORMAT には KSDATAFORMAT、提案されたデータ形式を指定する型の構造が含まれます。 メンバーが、関連する pin ファクトリを指定します、KSP_PIN を使用してこのプロパティを指定します。

KSPROPERTY\_PIN\_PROPOSEDATAFORMAT には型の構造体が含まれています[ **KSDATAFORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff561656)、提案されたデータ形式を指定します。

[**KSPROPERTY\_型\_取得**](https://docs.microsoft.com/en-us/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier) Windows 7 および Windows の以降のバージョンでサポートされます。 Windows Vista で**KSPROPERTY\_型\_取得**は*はサポートされていません*します。 

**KSPROPERTY_TYPE_GET**このプロパティ、オーディオ ドライバー、暗証番号 (pin) の既定のデータ形式に関する情報を提供することができます。 **KSPROPERTY_TYPE_GET**ドライバーがサポートしていない限り、このプロパティの実装も[ **KSEVENT_PINCAPS_FORMATCHANGE**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksevent-pincaps-formatchange)します。 
 

KS フィルター ステータスを返します\_ピンに設定または提案されたデータの形式で開くことができる場合、KSPROPERTY_TYPE_SET をこのプロパティを使用する場合は成功します。 提案されたデータ形式には、pin を設定することはできませんの場合は、STATUS_NO_MATCH が返します。 その他のエラーでは、適切なエラーが返されます。 ドライバーがサポートしている場合[ **KSPROPERTY_AUDIOSIGNALPROCESSING_MODES**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audiosignalprocessing-modes)、オーディオ信号の処理モードのいずれかで、形式がサポートされている場合、このプロパティは STATUS_SUCCESS を返す必要があります。 


KSPROPERTY_TYPE_SET にこのプロパティを使用しても、データ形式が実際に変更はされません。 クライアントを使用して、 [ **KSPROPERTY\_接続\_DATAFORMAT** ](ksproperty-connection-dataformat.md)データ形式を変更します。 **KSPROPERTY_TYPE_SET**はこのプロパティを実装するために省略可能です。


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
<td>Ks.h (Ks.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**KSP\_暗証番号 (PIN)**](https://msdn.microsoft.com/library/windows/hardware/ff566722)

[**KSDATAFORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff561656)
 
[**KSEVENT_PINCAPS_FORMATCHANGE**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksevent-pincaps-formatchange)

[**KS プロパティ**](https://docs.microsoft.com/en-us/windows-hardware/drivers/stream/ks-properties)

[**KSPROPERTY\_型\_取得**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)
 
[**KSPROPERTY_AUDIOSIGNALPROCESSING_MODES**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audiosignalprocessing-modes)





