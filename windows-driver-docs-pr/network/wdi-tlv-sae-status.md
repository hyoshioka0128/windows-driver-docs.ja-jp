---
title: WDI_TLV_SAE_STATUS
description: WDI_TLV_SAE_STATUS は、Equals (SAE) 認証エラーの状態の同時認証を含む TLV です。
ms.assetid: 7B6B8D4B-35B4-4AEA-A969-4BB514AB968E
ms.date: 02/15/2019
keywords:
- WDI_TLV_SAE_STATUS ネットワークドライバー (Windows Vista 以降)
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: f3f48f0a490a06908a85320c004a04783641758a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841736"
---
# <a name="wdi_tlv_sae_status"></a>WDI_TLV_SAE_STATUS

**WDI_TLV_SAE_STATUS**は、EQUALS (SAE) 認証エラーの状態の同時認証を含む TLV です。

この TLV は、 [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)のコマンドパラメーターと[NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md)のペイロードデータで使用されます。

## <a name="tlv-type"></a>TLV 型

0x14C

## <a name="length"></a>長さ

UINT32 のサイズ (バイト単位)。

## <a name="values"></a>値

| タスクバーの検索ボックスに | 説明 |
| --- | --- |
| [**WDI_SAE_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_sae_status) | SAE 認証エラーの状態。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1903 |
| サポートされている最小のサーバー | WIN ENT LTSB 2016 Estonian 64 Bits |
| Header | Wditypes |
