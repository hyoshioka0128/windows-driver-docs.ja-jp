---
title: KSK プロパティ \_ 未加工 \_ AVC \_ CMD
description: KSK プロパティの \_ 未加工の \_ AVC \_ CMD プロパティは、未加工の AV/C コマンドを発行します。 未加工の AV/C コマンドは、IEEE 1394 バスデバイスでのみサポートされています。
ms.assetid: f3ff3815-0f4f-4fcb-89bd-e77d8002813c
keywords:
- ストリーミングメディアデバイスの KSPROPERTY_RAW_AVC_CMD
topic_type:
- apiref
api_name:
- KSPROPERTY_RAW_AVC_CMD
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 0415da68b5475246045bdf6e28e380e0b3199620
ms.sourcegitcommit: 8143bb312ead6582b4b3e0ad34b6266dcfd74fb5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/18/2020
ms.locfileid: "84992480"
---
# <a name="ksproperty_raw_avc_cmd"></a>KSK プロパティ \_ 未加工 \_ AVC \_ CMD

KSK プロパティの \_ 未加工の \_ AVC \_ CMD プロパティは、未加工の AV/C コマンドを発行します。 未加工の AV/C コマンドは、IEEE 1394 バスデバイスでのみサポートされています。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

| 取得 | オン | 移行先 | プロパティ記述子の型 | プロパティ値の型 |
|--|--|--|--|--|
| はい | はい | デバイス | [**KSPROPERTY_EXTXPORT_S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s) | 埋め込み**RawAVC**構造体 |

プロパティ値 (操作データ) は、 **RawAVC** \_ \_ 実行する未加工の AV/C コマンドを記述する、ksproperty EXTXPORT S 構造体の埋め込み RawAVC メンバーです。

## <a name="remarks"></a>Remarks

このプロパティは、AV/C コマンドをサポートできるデバイスでのみ使用できます。また、 [**Ksk プロパティ \_ extdevice \_ ポート**](ksproperty-extdevice-port.md)は \_ \_ 、 [**ksk プロパティ \_ extdevice \_ S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extdevice_s)構造体の**devport**メンバー内の DEV ポート1394を返します。

IEEE 1394 デバイスのドライバー開発者は、必要に応じて、標準インターフェイスでサポートされていないデバイストランスポート制御 (ユーザーモードの**Iamexttransport** COM インターフェイスメソッド**put \_ モード**や**get \_ モード**など) を拡張するために、ドライバーでこのプロパティをサポートすることができます。

Usb[ビデオクラスドライバー](https://docs.microsoft.com/windows-hardware/drivers/stream/usb-video-class-driver)ではこの機能が提供されるため、usb デバイスでこのプロパティのサポートを実装する必要はありません。 通常、アプリケーションでは、 **Iksk コントロール**COM インターフェイスを使用して、IEEE 1394 デバイスを制御できます。 ただし、 **Iksk コントロール**COM インターフェイスには、USB および IEEE 1394 バス間で移植可能なテープシークをサポートするための標準的な方法が用意されていません。 したがって、テープシークを実行するには、呼び出し元は**Ikscontrol** COM インターフェイスの代わりに**DeviceIoControl**関数を使用する必要があります。 呼び出し元は、生の AV/C コマンドと、シークする絶対トラック番号 (ATN) または時間コードを使用して、1394 AV/C デバイスでテープシークを実行します。 これは、このプロパティが USB デバイスに適用されない主な理由です。

USB デバイスと1394デバイスでのテープの場所の検索の違いの詳細については、「[デジタルビデオアプリケーションの互換性](https://go.microsoft.com/fwlink/?linkid=2085071)」ホワイトペーパーを参照してください。

## <a name="requirements"></a>必要条件

| &nbsp; | &nbsp; |
| --- | --- |
| **ヘッダー** | Ksmedia .h (Ksk を含む) |

## <a name="see-also"></a>関連項目

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ EXTXPORT \_ S**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_extxport_s)
