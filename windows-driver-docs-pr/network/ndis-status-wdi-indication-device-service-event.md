---
title: NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT
description: NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT 状態の表示は、ユーザー モードのクライアント デバイスに関する情報を要請していないに渡すミニポート ドライバーによって使用されます。
ms.assetid: 6A9EA354-86F0-4C3F-974E-4FC164239D6A
ms.date: 06/14/2018
keywords:
- NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 28c22b0e161cd002c06548486f9b01ab59437d2e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572374"
---
# <a name="ndisstatuswdiindicationdeviceserviceevent"></a>NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT

NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT 状態の表示は、ユーザー モードのクライアント デバイスに関する情報を要請していないに渡す、IHV ミニポート ドライバーによって使用されます。

ミニポート ドライバーによってデバイスのサービスの問題を送信する必要がある時にのみ、 *D0*電源の状態、およびその必要があります、デバイスからの復帰を*Dx*します。 WDI は受信した場合、スタックを転送せずこのを示す値を削除の場合に*Dx*します。

この通知は現在、既定のポート (ステーション) でのみ処理されます。

ミニポート ドライバーには、デバイス サービス GUID とオペレーション コード ペアごとに必要なときに別の通知を送信する必要があります。

## <a name="payload-data"></a>ペイロード データ

| 型 | 許可されている複数の TLV インスタンス | 省略可能 | 説明 |
| --- | --- | --- | --- |
| [WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB](wdi-tlv-device-service-params-data-blob.md) |   | x | IHV ミニポート ドライバーから受信した情報。 |
| [WDI_TLV_DEVICE_SERVICE_PARAMS_GUID](wdi-tlv-device-service-params-guid.md) |   |   | この通知が所属する (IHV と OEM によって定義される) と、デバイス サービスを識別する GUID。 |
| [WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE](wdi-tlv-device-service-params-opcode.md) |   |   | デバイス サービスに固有のオペコードにします。 |

## <a name="requirements"></a>必要条件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 Version 1809 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Dot11wdi.h |
