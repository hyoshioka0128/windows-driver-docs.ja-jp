---
title: WDI_TLV_RSN_KEY_INFO
description: WDI_TLV_RSN_KEY_INFO は、Rsn の Eapol キーパラメーターを含む TLV です。
ms.assetid: 8C7C77F7-FF62-485C-94C4-EE0F1E57D771
ms.date: 04/02/2018
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_RSN_KEY_INFO
ms.localizationpriority: medium
ms.openlocfilehash: edb27701ccdb71c0bb2e3d3987fa95cbbbe28b73
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968587"
---
# <a name="wdi_tlv_rsn_key_info"></a>WDI_TLV_RSN_KEY_INFO

WDI_TLV_RSN_KEY_INFO は、Rsn の Eapol キーパラメーターを含む TLV です。 この TLV は、 [WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY](wdi-tlv-pm-protocol-offload-80211rsn-rekey.md) TLV の値です。

## <a name="tlv-type"></a>TLV 型

0x148

## <a name="length"></a>長さ

次の値のサイズ (バイト単位)。

## <a name="values"></a>値

| Type | [説明] |
| --- | --- |
| UINT32 | プロトコルオフロード ID を指定する UINT32 値。 オフロードプロトコルを識別する OS 提供の値です。 OS が追加要求を送信する前、またはそれ以降のドライバーへの要求を完了する前に、OS は ProtocolOffloadId をネットワークアダプターのプロトコルオフロード間で一意の値に設定します。 |
| UINT64 | Replay カウンターを指定する UINT64 値。 |
| UINT8 \[ 16\] | IEEE 802.11 キー確認キー (KCK) を指定する配列。 |
| UINT8 \[ 16\] | IEEE 802.11 キー暗号化キー (KEK) を指定する UINT8 配列。  |
 

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: Windows 10、バージョン1803

**サポートされている最小サーバー**: Windows server 2016

**ヘッダー**: Wditypes

