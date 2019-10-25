---
title: KSK プロパティ\_PIN\_通信
description: KSK プロパティ\_ピン留め\_通信のプロパティは、pin ファクトリによってインスタンス化された pin の IRP フローの方向を指定します。
ms.assetid: d5f62731-39de-4ec4-83d5-f4253373aaa4
keywords:
- KSPROPERTY_PIN_COMMUNICATION ストリーミングメディアデバイス
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
ms.openlocfilehash: 49c0d21221ff8a3289b6b1668283e3d02de85fda
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842746"
---
# <a name="ksproperty_pin_communication"></a>KSK プロパティ\_PIN\_通信


KSK プロパティ\_ピン留め\_通信のプロパティは、pin ファクトリによってインスタンス化された pin の IRP フローの方向を指定します。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p>KSPIN_COMMUNICATION</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>注釈
-------

KS フィルターは、次のいずれかの値を返します。これは、このピンファクトリによってインスタンス化された pin の通信方向を指定します。

<span id="KSPIN_COMMUNICATION_NONE"></span><span id="kspin_communication_none"></span>KSPIN\_通信\_なし  
Pin ファクトリは、どのピンもインスタンス化しません。

<span id="KSPIN_COMMUNICATION_SINK"></span><span id="kspin_communication_sink"></span>KSPIN\_通信\_シンク  
Pin ファクトリは、IRP シンク pin をインスタンス化します。 このような pin は、IRP ソースのピンにのみ接続できます。

<span id="KSPIN_COMMUNICATION_SOURCE"></span><span id="kspin_communication_source"></span>KSPIN\_通信\_ソース  
Pin ファクトリは、IRP ソースピンをインスタンス化します。 このような pin は、IRP シンクピンにのみ接続できます。

<span id="KSPIN_COMMUNICATION_BOTH"></span><span id="kspin_communication_both"></span>KSPIN\_通信\_両方  
Pin ファクトリは、IRP シンクと IRP ソースの両方であるピンをインスタンス化します。

<span id="KSPIN_COMMUNICATION_BRIDGE"></span><span id="kspin_communication_bridge"></span>KSPIN\_通信\_ブリッジ  
この pin は他のピンに接続できませんが、インスタンスを作成して、非 KS i/o 要求を受け取ることができます。

ソースピンは、Irp をシンクピンに送信します。 ソースピンはデータの読み取りまたは書き込みを行うことができ、シンクピンはデータを読み取ったり書き込んだりすることがあります。 詳細については、「 [**Ksk プロパティ\_PIN\_データフロー**](ksproperty-pin-dataflow.md)」を参照してください。

Stream ミニドライバーは、このプロパティを直接処理する必要はありません。stream クラスドライバーは、必要に応じて詳細情報を照会するストリーム要求ブロックを使用して、このプロパティを処理します。

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


[**KSK プロパティ\_ピン留め\_データフロー**](ksproperty-pin-dataflow.md)

 

 






