---
title: NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT
description: NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT ステータス表示は、デバイスに関する要請されていない情報をユーザーモードクライアントに渡すためにミニポートドライバーによって使用されます。
ms.assetid: 6A9EA354-86F0-4C3F-974E-4FC164239D6A
ms.date: 06/14/2018
keywords:
- Windows Vista 以降のネットワークドライバーの NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT
ms.localizationpriority: medium
ms.openlocfilehash: 618f52d23b1a19e84b64a79ae585e8f269e28ce9
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968131"
---
# <a name="ndis_status_wdi_indication_device_service_event"></a>NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT

NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT の状態の表示は、デバイスに関する要請されていない情報をユーザーモードクライアントに渡すために、IHV ミニポートドライバーによって使用されます。

デバイスサービスの兆候は、 *D0*電源状態の場合にのみミニポートドライバーによって送信され、デバイスが*Dx*から復帰しないようにする必要があります。 WDI は、 *Dx*で受信した場合にスタックを転送せずに、この表示を削除します。

この表示は、現在、既定のポート (ステーション) でのみ処理されます。

ミニポートドライバーは、必要に応じて、デバイスサービスの GUID とオペコードのペアごとに個別の通知を送信する必要があります。

## <a name="payload-data"></a>ペイロードデータ

| Type | 複数の TLV インスタンスを使用できます | 省略可能 | 説明 |
| --- | --- | --- | --- |
| [WDI_TLV_DEVICE_SERVICE_PARAMS_DATA_BLOB](wdi-tlv-device-service-params-data-blob.md) |   | X | IHV ミニポートドライバーから受信した情報。 |
| [WDI_TLV_DEVICE_SERVICE_PARAMS_GUID](wdi-tlv-device-service-params-guid.md) |   |   | この指示が属するデバイスサービスを識別する GUID (IHV/OEM による定義による)。 |
| [WDI_TLV_DEVICE_SERVICE_PARAMS_OPCODE](wdi-tlv-device-service-params-opcode.md) |   |   | デバイスサービス固有のオペコード。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: Windows 10、バージョン1809

**サポートされている最小サーバー**: Windows server 2016

**ヘッダー**: Dot11wdi

