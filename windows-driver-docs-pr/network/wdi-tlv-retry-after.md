---
title: WDI_TLV_RETRY_AFTER
description: WDI_TLV_RETRY_AFTER は、ターゲット BSS から新しい詳細なタイミング測定 (FTM) を要求するまでに経過する時間を秒単位で表す TLV です。
ms.assetid: BFB15FF0-0272-4FDC-AD7A-94ECDA59D0ED
ms.date: 02/15/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_RETRY_AFTER
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 5d055b2fc04adb932c60c97f08a53e6ba33897ab
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917656"
---
# <a name="wdi_tlv_retry_after"></a>WDI_TLV_RETRY_AFTER

**WDI_TLV_RETRY_AFTER**は、ターゲット BSS から新しい詳細なタイミング測定 (FTM) を要求するまでに経過する時間を秒単位で表す TLV です。

この TLV は[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)で使用されます。

## <a name="tlv-type"></a>TLV 型

0x15A

## <a name="length"></a>長さ

UINT16 のサイズ (バイト単位)。

## <a name="values"></a>値

| Type | 説明 |
| --- | --- |
| UINT16 | ターゲット BSS から新しい詳細なタイミング測定 (FTM) を要求するまでに経過する必要がある時間 (秒単位)。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
