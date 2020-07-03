---
title: WDI_TLV_FTM_REQUEST_TIMEOUT
description: WDI_TLV_FTM_REQUEST_TIMEOUT は、細かなタイミング測定 (FTM) を完了するための最大時間 (ミリ秒単位) を含む TLV です。
ms.assetid: C2C4CDEE-4CB6-49C1-8DBF-4A1AE71954ED
ms.date: 02/15/2019
keywords:
- Windows Vista 以降のネットワークドライバーの WDI_TLV_FTM_REQUEST_TIMEOUT
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: bd2b64133a71087cb89c201cffaa07c757fdaa64
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85916148"
---
# <a name="wdi_tlv_ftm_request_timeout"></a>WDI_TLV_FTM_REQUEST_TIMEOUT

**WDI_TLV_FTM_REQUEST_TIMEOUT**は、細かなタイミング測定 (FTM) を完了するための最大時間 (ミリ秒単位) を含む TLV です。

この TLV は、 [OID_WDI_TASK_REQUEST_FTM](oid-wdi-task-request-ftm.md)のタスクパラメーターで使用されます。

## <a name="tlv-type"></a>TLV 型

0x161

## <a name="length"></a>長さ

UINT32 のサイズ (バイト単位)。

## <a name="values"></a>値

| Type | 説明 |
| --- | --- |
| UINT32 | FTM を完了するまでの最大時間 (ミリ秒単位)。 タイムアウトは、150ミリ秒にターゲットの数を乗算した値に設定されます。 |

## <a name="requirements"></a>要件

**サポートされている最小クライアント**: windows 10、バージョン1903の**サポートされている最小サーバー**: windows server 2016**ヘッダー**: Wditypes
