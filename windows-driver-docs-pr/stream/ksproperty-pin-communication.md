---
title: KSPROPERTY\_PIN\_通信
description: KSPROPERTY\_PIN\_通信プロパティ pin ファクトリによってインスタンス化するピンの IRP のフローの方向を指定します。
ms.assetid: d5f62731-39de-4ec4-83d5-f4253373aaa4
keywords:
- KSPROPERTY_PIN_COMMUNICATION ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_COMMUNICATION
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c89eeaba1ee022da9edea31885667d1c2d3981e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362623"
---
# <a name="kspropertypincommunication"></a>KSPROPERTY\_PIN\_通信


KSPROPERTY\_PIN\_通信プロパティ pin ファクトリによってインスタンス化するピンの IRP のフローの方向を指定します。

## <span id="ddk_ksproperty_pin_communication_ks"></span><span id="DDK_KSPROPERTY_PIN_COMMUNICATION_KS"></span>


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
<td><p>いいえ</p></td>
<td><p>Pin</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p>KSPIN_COMMUNICATION</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS フィルターには、この暗証番号 (pin) ファクトリによってインスタンス化される pin の通信の方向を指定します、次の値のいずれかが返されます。

<span id="KSPIN_COMMUNICATION_NONE"></span><span id="kspin_communication_none"></span>KSPIN\_通信\_NONE  
暗証番号 (pin) ファクトリは、いずれかのピンをインスタンス化できません。

<span id="KSPIN_COMMUNICATION_SINK"></span><span id="kspin_communication_sink"></span>KSPIN\_通信\_シンク  
暗証番号 (pin) ファクトリには、IRP シンク ピンがインスタンス化します。 このようなピンを接続できるは、IRP ソース ピンのみです。

<span id="KSPIN_COMMUNICATION_SOURCE"></span><span id="kspin_communication_source"></span>KSPIN\_通信\_ソース  
暗証番号 (pin) ファクトリには、ソース ピンの IRP がインスタンス化します。 このようなピンを接続できるは、IRP シンク ピンのみです。

<span id="KSPIN_COMMUNICATION_BOTH"></span><span id="kspin_communication_both"></span>KSPIN\_通信\_両方  
暗証番号 (pin) ファクトリでは、pin は IRP シンクと IRP のソースの両方をインスタンス化します。

<span id="KSPIN_COMMUNICATION_BRIDGE"></span><span id="kspin_communication_bridge"></span>KSPIN\_通信\_ブリッジ  
この pin は、他のピンに接続できませんが、KS 以外の I/O 要求を受信するには、インスタンスを作成できます。

ソースのピンは、ピンをシンクする Irp を送信します。 ソース暗証番号 (pin) が読み取りまたは書き込み、およびシンク暗証番号 (pin) はデータを読み取りまたはそこから書き込まれる必要があります。 詳細については、次を参照してください。 [ **KSPROPERTY\_PIN\_データフロー**](ksproperty-pin-dataflow.md)します。

Stream ミニドライバーは、このプロパティを直接処理する必要はありません。ストリーム クラス ドライバーは、必要に応じて詳細情報のクエリに Stream 要求のブロックを使って、このプロパティを処理します。

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


[**KSPROPERTY\_PIN\_データ フロー**](ksproperty-pin-dataflow.md)

 

 






