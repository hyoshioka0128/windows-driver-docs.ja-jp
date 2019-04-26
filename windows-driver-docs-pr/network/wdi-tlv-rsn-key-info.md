---
title: WDI_TLV_RSN_KEY_INFO
description: WDI_TLV_RSN_KEY_INFO は、Rsn Eapol キー パラメーターを含む TLV です。
ms.assetid: 8C7C77F7-FF62-485C-94C4-EE0F1E57D771
ms.date: 04/02/2018
keywords:
- WDI_TLV_RSN_KEY_INFO ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: c86ecacd424f00a41db920352ce3bd618aa7e0ff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359093"
---
# <a name="wditlvrsnkeyinfo"></a>WDI_TLV_RSN_KEY_INFO

WDI_TLV_RSN_KEY_INFO は、Rsn Eapol キー パラメーターを含む TLV です。 この TLV の値であり、 [WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY](wdi-tlv-pm-protocol-offload-80211rsn-rekey.md) TLV します。

## <a name="tlv-type"></a>TLV 型

0x148

## <a name="length"></a>長さ

次の値のバイト単位でサイズ。

## <a name="values"></a>値

| 型 | 説明 |
| --- | --- |
| UINT32 | プロトコルのオフロード ID を指定する UINT32 値 これは、オフロードされたプロトコルを識別する OS で提供される値です。 OS では、追加要求を送信します。 または、上にあるドライバーへの要求が完了すると、前に、プロトコル間で一意の値に OS セット ProtocolOffloadId をネットワーク アダプターにオフロードします。 |
| UINT64 | 再生のカウンターを指定する UINT64 値。 |
| UINT8\[16\] | IEEE 802.11 キー確認キー (KCK) を指定する UINT8 配列を指定します。 |
| UINT8\[16\] | IEEE 802.11 キー暗号化キー (KEK) を指定する UINT8 配列。  |
 

## <a name="requirements"></a>要件

| | |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1803 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
