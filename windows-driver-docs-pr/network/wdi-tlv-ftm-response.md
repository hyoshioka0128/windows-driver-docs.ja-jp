---
title: WDI_TLV_FTM_RESPONSE
description: WDI_TLV_FTM_RESPONSE は、BSS ターゲットから正常タイミング測定 (FTM) 応答の情報を含む TLV です。
ms.assetid: 7FD63544-F7FF-4593-A525-A6BEA2A56BB7
ms.date: 02/13/2019
keywords:
- WDI_TLV_FTM_RESPONSE ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6d2b4ba9140eb8577e76af1f48bfcc458f04ebe6
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905285"
---
# <a name="wditlvftmresponse"></a>WDI_TLV_FTM_RESPONSE

**WDI_TLV_FTM_RESPONSE** BSS ターゲットから正常タイミング測定 (FTM) 応答の情報を含む TLV です。 

この TLV がのペイロード データに使用される、 [NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE](ndis-status-wdi-indication-request-ftm-complete.md)タスクの完了を示す値。

## <a name="tlv-type"></a>TLV 型

0x163

## <a name="length"></a>長さ

すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値

| TLV | 種類 | 許可されている複数の TLV インスタンス | 省略可能 | 説明 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_BSSID](wdi-tlv-bssid.md) | [**WDI_MAC_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) |  |   | この FTM 応答が所属するターゲットの BSSID します。 |
| [WDI_TLV_FTM_RESPONSE_STATUS](wdi-tlv-ftm-response-status.md) | [**WDI_FTM_RESPONSE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_ftm_response_status) |  |   | FTM 応答状態。 成功した場合、この TLV 内のフィールドの残りの部分に存在する場合。 |
| [WDI_TLV_RETRY_AFTER](wdi-tlv-retry-after.md)| UINT16 |  |  | このターゲットから新しい FTM を要求しようとする前に渡す必要がありますを秒単位で期間です。 |
| [WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS](wdi-tlv-ftm-number-of-measurements.md) | UINT16 |  |   | ラウンド トリップ時間 (RTT) を提供するために使用する測定値の数。 FTM 応答の状態が、成功の場合は、このフィールドは必須です。 |
| [WDI_TLV_BSS_ENTRY_SIGNAL_INFO](wdi-tlv-bss-entry-signal-info.md) | INT32 |   |   | FTM ターゲットから受信信号強度インジケーター (RSSI)。 これを参照して、1.0 ミリ ワット (dBm) デシベル単位の単位です。 FTM 応答の状態が、成功の場合は、このフィールドは必須です。 |
| 行の上と同じ  | UINT32 |   |   | FTM ターゲットは、0 から 100 までのリンクの品質の値。 100 の値には、リンクの最高の品質を指定します。 FTM 応答の状態が、成功の場合は、このフィールドは必須です。 |
| [WDI_TLV_RTT](wdi-tlv-rtt.md) | UINT32 |   |   | ピコで測定ラウンドト リップ時間 (RTT)。 FTM 応答の状態が、成功の場合は、このフィールドは必須です。 |
| [WDI_TLV_RTT_ACCURACY](wdi-tlv-rtt-accuracy.md) | UINT32 |   |   | 正確さ、または期待される範囲の値を true に指定された RTT 測定、近さの程度。 単位は、ピコで。 詳細については、次を参照してください。、 [WDI_TLV_RTT_ACCURACY](wdi-tlv-rtt-accuracy.md)します。 |
| [WDI_TLV_RTT_VARIANCE](wdi-tlv-rtt-variance.md) | UINT64 |   |   | RTT を計算するには、複数の測定を使用した場合、このフィールドは、使用される測定値の統計的分散を提供します。 |
| [WDI_TLV_LCI_REPORT_STATUS](wdi-tlv-lci-report-status.md) | [**WDI_LCI_REPORT_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_lci_report_status) |   |   | LCI レポートが要求された場合、このフィールドは、状態の結果を提供します。 成功した場合、次のフィールドが存在し、必須にします。 |
| [WDI_TLV_LCI_REPORT_BODY](wdi-tlv-lci-report-body.md) | TLV\<一覧\<UINT8 &GT;&GT; |   |   | 9.4.2.22.10 のセクションで定義されている、場所の構成情報 (LCI) レポート、 [802-11-2016 standard](https://standards.ieee.org/standard/802_11-2016.html)LCI サブ要素とその他のオプションのサブ要素を含めて、します。 つまり、これは、測定レポート要素の測定レポート セクション (セクション 9.4.2.22 からに従って、 [802-11-2016 standard](https://standards.ieee.org/standard/802_11-2016.html))。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10、バージョンが 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
