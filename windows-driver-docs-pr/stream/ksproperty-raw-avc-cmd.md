---
title: KSK プロパティ\_未加工\_AVC\_CMD
description: '\_未加工\_AVC\_CMD プロパティによって、未加工の AV/C コマンドが発行されます。 未加工の AV/C コマンドは、IEEE 1394 バスデバイスでのみサポートされています。'
ms.assetid: f3ff3815-0f4f-4fcb-89bd-e77d8002813c
keywords:
- KSPROPERTY_RAW_AVC_CMD ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_RAW_AVC_CMD
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e7beb93bdf99679821789a3502571a6c5b789ef7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838835"
---
# <a name="ksproperty_raw_avc_cmd"></a>KSK プロパティ\_未加工\_AVC\_CMD

\_未加工\_AVC\_CMD プロパティによって、未加工の AV/C コマンドが発行されます。 未加工の AV/C コマンドは、IEEE 1394 バスデバイスでのみサポートされています。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

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
<td><p>デバイス</p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_EXTXPORT_S&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)"><strong>KSPROPERTY_EXTXPORT_S</strong></a></p></td>
<td><p>埋め込み<strong>RawAVC</strong>構造体</p></td>
</tr>
</tbody>
</table>

プロパティ値 (操作データ) は、実行する未加工の AV/C コマンドを記述する KSK プロパティ\_EXTXPORT\_S 構造体の埋め込み**RawAVC**メンバーです。

## <a name="remarks"></a>注釈

このプロパティは、AV/C コマンドをサポートできるデバイスでのみ使用できます。また、 [**Ksk プロパティ\_extdevice\_port**](ksproperty-extdevice-port.md)は、ksk プロパティ\_Extdevice の**DEVPORT**メンバーで DEV\_PORT\_1394 を返し[ **\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extdevice_s)構造体。

IEEE 1394 デバイスのドライバー開発者は、標準インターフェイス (ユーザーモードの**Iamexttransport** COM インターフェイスメソッドなど) でサポートされていないデバイストランスポートコントロールを拡張するために、必要に応じてドライバーでこのプロパティをサポートできます。 **\_モード**を設定し、 **\_モードを取得**します)。

Usb[ビデオクラスドライバー](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver)ではこの機能が提供されるため、usb デバイスでこのプロパティのサポートを実装する必要はありません。 通常、アプリケーションでは、 **Iksk コントロール**COM インターフェイスを使用して、IEEE 1394 デバイスを制御できます。 ただし、 **Iksk コントロール**COM インターフェイスには、USB および IEEE 1394 バス間で移植可能なテープシークをサポートするための標準的な方法が用意されていません。 したがって、テープシークを実行するには、呼び出し元は**Ikscontrol** COM インターフェイスの代わりに**DeviceIoControl**関数を使用する必要があります。 呼び出し元は、生の AV/C コマンドと、シークする絶対トラック番号 (ATN) または時間コードを使用して、1394 AV/C デバイスでテープシークを実行します。 これは、このプロパティが USB デバイスに適用されない主な理由です。

USB デバイスと1394デバイスでのテープの場所の検索の違いの詳細については、「[デジタルビデオアプリケーションの互換性](https://go.microsoft.com/fwlink/?linkid=2085071)」ホワイトペーパーを参照してください。

## <a name="requirements"></a>要件

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

[**KSK プロパティ\_EXTXPORT\_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)
