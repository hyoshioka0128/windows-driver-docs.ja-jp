---
title: WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS
description: WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS では、現在構成されている Rsn Eapol キー情報を含む TLV です。
ms.assetid: DFF81CBD-1B10-456F-AD8D-1163DD80C981
ms.date: 04/02/2018
keywords:
- WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.openlocfilehash: 72a812bd7b11c7f1118ec14a7f2a934ba0c09b56
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557927"
---
# <a name="wditlvpmprotocolrsnoffloadkeys"></a>WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS

WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS では、現在構成されている Rsn Eapol キー情報を含む TLV です。 この TLV がで使用される、 [NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED](ndis-status-wdi-indication-cipher-key-updated.md)状態を示す値。

## <a name="tlv-type"></a>TLV 型

0x149

## <a name="values"></a>値

| 種類 | 説明 |
| --- | --- |
| WDI_RSN_OFFLOAD_KEYS_CONTAINER | 現在構成されている Rsn Eapol キー情報。 |

## <a name="requirements"></a>要件

| | |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1803 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
