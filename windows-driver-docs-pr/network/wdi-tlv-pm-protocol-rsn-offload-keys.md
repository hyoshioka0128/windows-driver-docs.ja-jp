---
title: WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS
description: WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS は、現在構成されている Rsn Eapol キー情報を含む TLV です。
ms.assetid: DFF81CBD-1B10-456F-AD8D-1163DD80C981
ms.date: 04/02/2018
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS
ms.localizationpriority: medium
ms.openlocfilehash: a6e2eceea6140f3449bed66b0ae2aa960ffb5ed1
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968309"
---
# <a name="wdi_tlv_pm_protocol_rsn_offload_keys"></a>WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS

WDI_TLV_PM_PROTOCOL_RSN_OFFLOAD_KEYS は、現在構成されている Rsn Eapol キー情報を含む TLV です。 この TLV は、 [NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED](ndis-status-wdi-indication-cipher-key-updated.md)状態表示で使用されます。

## <a name="tlv-type"></a>TLV 型

0x149

## <a name="values"></a>値

| Type | [説明] |
| --- | --- |
| WDI_RSN_OFFLOAD_KEYS_CONTAINER | 現在構成されている Rsn Eapol キー情報。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: Windows 10、バージョン1803

**サポートされている最小サーバー**: Windows server 2016

**ヘッダー**: Wditypes

