---
title: WDI_TLV_LCI_REPORT_BODY
description: WDI_TLV_LCI_REPORT_BODY は、細かなタイミング測定 (FTM) 要求の場所の構成レポート (LCI) を含む TLV です。
ms.assetid: D80AB500-0B4F-47AC-ADF7-DDB5635FF1F2
ms.date: 02/15/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_LCI_REPORT_BODY
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6197c77ce1c54ba0038ff198828f595ebf4ab12c
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916109"
---
# <a name="wdi_tlv_lci_report_body"></a>WDI_TLV_LCI_REPORT_BODY

**WDI_TLV_LCI_REPORT_BODY**は、細かなタイミング測定 (FTM) 要求の場所の構成レポート (lci) を含む TLV です。

この TLV は[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)で使用されます。

## <a name="tlv-type"></a>TLV 型

0x160

## <a name="length"></a>長さ

UINT8 要素の配列のサイズ (バイト単位)。 配列には1つ以上の要素が含まれている必要があります。

## <a name="values"></a>値

| Type | 説明 |
| --- | --- |
| UINT8 [] | LCI レポート。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
