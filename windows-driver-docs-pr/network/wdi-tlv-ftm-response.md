---
title: WDI_TLV_FTM_RESPONSE
description: WDI_TLV_FTM_RESPONSE は、BSS ターゲットからのタイミング測定 (FTM) 応答情報を含む TLV です。
ms.assetid: 7FD63544-F7FF-4593-A525-A6BEA2A56BB7
ms.date: 02/13/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_FTM_RESPONSE
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: cc78b2579bc31650291e5212e992dcc2f2a28316
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918282"
---
# <a name="wdi_tlv_ftm_response"></a>WDI_TLV_FTM_RESPONSE

**WDI_TLV_FTM_RESPONSE**は、BSS ターゲットからのタイミング測定 (FTM) 応答情報を含む TLV です。 

この TLV は、 [NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE](ndis-status-wdi-indication-request-ftm-complete.md)タスクの完了を示すペイロードデータで使用されます。

## <a name="tlv-type"></a>TLV 型

0x163

## <a name="length"></a>長さ

含まれているすべての TLVs のサイズの合計 (バイト単位)。

## <a name="values"></a>値

| TLV | 型 | 複数の TLV インスタンスを使用できます | 省略可能 | 説明 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_BSSID](wdi-tlv-bssid.md) | [**WDI_MAC_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) |  |   | この FTM 応答が属するターゲットの BSSID です。 |
| [WDI_TLV_FTM_RESPONSE_STATUS](wdi-tlv-ftm-response-status.md) | [**WDI_FTM_RESPONSE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_ftm_response_status) |  |   | FTM 応答の状態。 成功した場合、この TLV の残りのフィールドが存在します。 |
| [WDI_TLV_RETRY_AFTER](wdi-tlv-retry-after.md)| UINT16 |  |  | このターゲットから新しい FTM を要求するまでに経過する必要がある時間 (秒単位)。 |
| [WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS](wdi-tlv-ftm-number-of-measurements.md) | UINT16 |  |   | ラウンドトリップ時間 (RTT) を提供するために使用される測定値の数。 [FTM 応答の状態] が [成功] の場合、このフィールドは必須です。 |
| [WDI_TLV_BSS_ENTRY_SIGNAL_INFO](wdi-tlv-bss-entry-signal-info.md) | INT32 |   |   | FTM ターゲットから受信した信号強度インジケーター (RSSI)。 これは、1.0 ミリワット (dBm) に参照されるデシベル単位です。 [FTM 応答の状態] が [成功] の場合、このフィールドは必須です。 |
| 上の行と同じ  | UINT32 |   |   | FTM ターゲットのリンク品質値。 0 ~ 100 の範囲で指定します。 値が100の場合は、最高のリンク品質が指定されます。 [FTM 応答の状態] が [成功] の場合、このフィールドは必須です。 |
| [WDI_TLV_RTT](wdi-tlv-rtt.md) | UINT32 |   |   | 測定されたラウンドトリップ時間 (RTT) (秒単位)。 [FTM 応答の状態] が [成功] の場合、このフィールドは必須です。 |
| [WDI_TLV_RTT_ACCURACY](wdi-tlv-rtt-accuracy.md) | UINT32 |   |   | 指定された RTT 測定値に対する真の精度または予想される近さの次数。 単位は、のようになります。 詳細については、 [WDI_TLV_RTT_ACCURACY](wdi-tlv-rtt-accuracy.md)を参照してください。 |
| [WDI_TLV_RTT_VARIANCE](wdi-tlv-rtt-variance.md) | UINT64 |   |   | RTT を計算するために複数の測定値が使用された場合、このフィールドは、使用される測定値の統計的分散を提供します。 |
| [WDI_TLV_LCI_REPORT_STATUS](wdi-tlv-lci-report-status.md) | [**WDI_LCI_REPORT_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_lci_report_status) |   |   | LCI レポートが要求された場合、このフィールドには状態の結果が表示されます。 成功した場合、次のフィールドが存在し、必須となります。 |
| [WDI_TLV_LCI_REPORT_BODY](wdi-tlv-lci-report-body.md) | TLV\<LIST\<UINT8>> |   |   | 9.4.2.22.10 [802-11-2016](https://standards.ieee.org/standard/802_11-2016.html)のセクションで定義されている場所の構成情報 (lci) レポート。 lci サブ要素や、使用可能なその他のオプションのサブ要素が含まれます。 つまり、これは、測定レポート要素の測定レポートセクションです ( [802-11-2016 標準](https://standards.ieee.org/standard/802_11-2016.html)のセクション 9.4.2.22)。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
