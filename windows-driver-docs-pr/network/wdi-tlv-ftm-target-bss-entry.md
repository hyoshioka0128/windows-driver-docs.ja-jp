---
title: WDI_TLV_FTM_TARGET_BSS_ENTRY
description: WDI_TLV_FTM_TARGET_BSS_ENTRY では、細かいタイミング測定 (FTM) の手順を実行する必要がありますが、BSS ターゲットの情報を含む TLV です。
ms.assetid: 04C996C7-8207-4363-A990-5CF39B0333F8
ms.date: 02/13/2019
keywords:
- WDI_TLV_FTM_TARGET_BSS_ENTRY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 695c46e35e34d38083b4c95cedecfff1026ed6d6
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905369"
---
# <a name="wditlvftmtargetbssentry"></a>WDI_TLV_FTM_TARGET_BSS_ENTRY

**WDI_TLV_FTM_TARGET_BSS_ENTRY**どの正常タイミング測定 (FTM) での手順を完了する必要がある BSS ターゲットの情報を含む TLV は、します。 

この TLV がのタスク パラメーターで使用される[OID_WDI_TASK_REQUEST_FTM](oid-wdi-task-request-ftm.md)します。

## <a name="tlv-type"></a>TLV 型

0x162

## <a name="length"></a>長さ

すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値

| TLV | 種類 | 許可されている複数の TLV インスタンス | 省略可能 | 説明 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_BSSID](wdi-tlv-bssid.md) | [**WDI_MAC_ADDRESS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_mac_address) |   |   | ターゲット BSS の BSSID します。 |
| [WDI_TLV_PROBE_RESPONSE_FRAME](wdi-tlv-probe-response-frame.md) | TLV\<一覧\<UINT8 &GT;&GT; |   | x | プローブ応答フレーム。 プローブの応答を受信しなかった場合は、このフィールドが空です。 |
| [WDI_TLV_BEACON_FRAME](wdi-tlv-beacon-frame.md) | TLV\<一覧\<UINT8 &GT;&GT; |   | x | ビーコン フレーム。 ビーコンを受信しなかった場合は、このフィールドが空です。 |
| [WDI_TLV_BSS_ENTRY_SIGNAL_INFO](wdi-tlv-bss-entry-signal-info.md) | INT32 |   |   | ピアからビーコンまたはプローブの応答の受信信号強度指標 (RSSI) 値。 これを参照して、1.0 ミリ ワット (dBm) デシベル単位の単位です。 |
|  | UINT32 |   |   | 0 から 100 までのリンクの品質評価の値。 100 の値には、リンクの最高の品質を指定します。 |
| [WDI_TLV_BSS_ENTRY_CHANNEL_INFO](wdi-tlv-bss-entry-channel-info.md) | UINT32 |   |   | ターゲット BSS の論理のチャネルの数。 |
|   | UINT32 |   |   | ターゲット BSS のバンドの ID。 |
| [WDI_TLV_BSS_ENTRY_DEVICE_CONTEXT](wdi-tlv-bss-entry-device-context.md) | TLV\<一覧\<UINT8 &GT;&GT; |  |  | このピアに関する IHV コンポーネントから提供されるコンテキスト データ。 IHV コンポーネントが維持する必要がある BSS ごとのエントリの状態を格納する (米ドル) を指定できます。 有効期間管理を回避するためには、問題と、IHV コンポーネントは、このフィールドにポインターを使用しない必要があります。 |
| [WDI_TLV_REQUEST_LCI_REPORT](wdi-tlv-request-lci-report.md) | UINT8 |   |   | 設定可能な値: <ul><li>0:LCI レポートは必要ありません。</li><li>1:LCI レポートを要求する必要があります。</li></ul> |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10、バージョンが 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
