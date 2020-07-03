---
title: WDI_TLV_REQUEST_LCI_REPORT
description: WDI_TLV_REQUEST_LCI_REPORT は、適切なタイミング測定 (FTM) 要求で、ターゲット BSS から場所の構成情報 (LCI) レポートを要求するかどうかに関する情報を含む TLV です。
ms.assetid: BFB15FF0-0272-4FDC-AD7A-94ECDA59D0ED
ms.date: 02/15/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_REQUEST_LCI_REPORT
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6b2ade18e17f79859cc22b9e41e277785b55258a
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916894"
---
# <a name="wdi_tlv_request_lci_report"></a>WDI_TLV_REQUEST_LCI_REPORT

**WDI_TLV_REQUEST_LCI_REPORT**は、適切なタイミング測定 (FTM) 要求で、ターゲット BSS から場所の構成情報 (lci) レポートを要求するかどうかに関する情報を含む TLV です。

この TLV は[WDI_TLV_FTM_TARGET_BSS_ENTRY](wdi-tlv-ftm-target-bss-entry.md)で使用されます。

## <a name="tlv-type"></a>TLV 型

0x158

## <a name="length"></a>長さ

UINT8 のサイズ (バイト単位)。

## <a name="values"></a>値

| Type | 説明 |
| --- | --- |
| UINT8 | 指定できる値 <ul><li>0: LCI レポートは必要ありません。</li><li>1: LCI レポートを要求する必要があります。</li></ul> |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
