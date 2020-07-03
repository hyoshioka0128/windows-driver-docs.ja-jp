---
title: WDI_TLV_LCI_REPORT_STATUS
description: WDI_TLV_LCI_REPORT_STATUS は、場所の構成情報 (LCI) レポートの状態の結果を含む TLV です。これは、適切なタイミング測定 (FTM) 要求で要求された場合に発生します。
ms.assetid: 81122FDB-3E1C-472D-80D2-1C8F29F00D2D
ms.date: 02/15/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_LCI_REPORT_STATUS
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 2b3a3fe0f60e6a550413b5e4c855eeea811d1584
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916767"
---
# <a name="wdi_tlv_lci_report_status"></a>WDI_TLV_LCI_REPORT_STATUS

**WDI_TLV_LCI_REPORT_STATUS**は、場所の構成情報 (lci) レポートの状態の結果を含む TLV です。これは、適切なタイミング測定 (FTM) 要求で要求された場合に発生します。

この TLV は[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)で使用されます。

## <a name="tlv-type"></a>TLV 型

0x15F

## <a name="length"></a>長さ

UINT32 のサイズ (バイト単位)。

## <a name="values"></a>値

| Type | 説明 |
| --- | --- |
| [**WDI_LCI_REPORT_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_lci_report_status) | LCI レポートの状態です。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
