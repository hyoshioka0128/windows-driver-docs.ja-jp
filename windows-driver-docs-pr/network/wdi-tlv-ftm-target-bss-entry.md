---
title: WDI_TLV_FTM_TARGET_BSS_ENTRY
description: WDI_TLV_FTM_TARGET_BSS_ENTRY は、適切なタイミング測定 (FTM) の手順を完了する必要がある BSS ターゲットの情報を含む TLV です。
ms.assetid: 04C996C7-8207-4363-A990-5CF39B0333F8
ms.date: 02/13/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_FTM_TARGET_BSS_ENTRY
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 02143fd558d5829172cdd77934dd6a3433438a1f
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916874"
---
# <a name="wdi_tlv_ftm_target_bss_entry"></a>WDI_TLV_FTM_TARGET_BSS_ENTRY

**WDI_TLV_FTM_TARGET_BSS_ENTRY**は、適切なタイミング測定 (FTM) の手順を完了する必要がある BSS ターゲットの情報を含む TLV です。 

この TLV は、 [OID_WDI_TASK_REQUEST_FTM](oid-wdi-task-request-ftm.md)のタスクパラメーターで使用されます。

## <a name="tlv-type"></a>TLV 型

0x162

## <a name="length"></a>長さ

含まれているすべての TLVs のサイズの合計 (バイト単位)。

## <a name="values"></a>値

| TLV | 型 | 複数の TLV インスタンスを使用できます | 省略可能 | 説明 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_BSSID](wdi-tlv-bssid.md) | [**WDI_MAC_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) |   |   | ターゲット BSS の BSSID。 |
| [WDI_TLV_PROBE_RESPONSE_FRAME](wdi-tlv-probe-response-frame.md) | TLV\<LIST\<UINT8>> |   | X | プローブ応答フレーム。 プローブ応答が受信されなかった場合、このフィールドは空になります。 |
| [WDI_TLV_BEACON_FRAME](wdi-tlv-beacon-frame.md) | TLV\<LIST\<UINT8>> |   | X | ビーコンフレーム。 ビーコンが受信されていない場合、このフィールドは空です。 |
| [WDI_TLV_BSS_ENTRY_SIGNAL_INFO](wdi-tlv-bss-entry-signal-info.md) | INT32 |   |   | ピアからのビーコンまたはプローブ応答の受信信号強度インジケーター (RSSI) の値。 これは、1.0 ミリワット (dBm) に参照されるデシベル単位です。 |
|  | UINT32 |   |   | 0 ~ 100 の範囲のリンク品質値。 値が100の場合は、最高のリンク品質が指定されます。 |
| [WDI_TLV_BSS_ENTRY_CHANNEL_INFO](wdi-tlv-bss-entry-channel-info.md) | UINT32 |   |   | ターゲット BSS の論理チャネル番号。 |
|   | UINT32 |   |   | ターゲット BSS のバンド ID。 |
| [WDI_TLV_BSS_ENTRY_DEVICE_CONTEXT](wdi-tlv-bss-entry-device-context.md) | TLV\<LIST\<UINT8>> |  |  | IHV コンポーネントが指定した、このピアに関するコンテキストデータ。 これは、IHV コンポーネントが管理する必要がある BSS ごとのエントリ状態を格納するために、米国ドルになる場合があります。 有効期間管理の問題を回避するには、IHV コンポーネントでこのフィールドのポインターを使用しないようにする必要があります。 |
| [WDI_TLV_REQUEST_LCI_REPORT](wdi-tlv-request-lci-report.md) | UINT8 |   |   | 指定できる値 <ul><li>0: LCI レポートは必要ありません。</li><li>1: LCI レポートを要求する必要があります。</li></ul> |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
