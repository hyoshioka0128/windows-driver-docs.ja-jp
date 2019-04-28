---
title: WDI_TLV_FTM_REQUEST_TIMEOUT
description: WDI_TLV_FTM_REQUEST_TIMEOUT では、細かいタイミング測定 (FTM) を完了するミリ秒単位の最大時間を含む TLV です。
ms.assetid: C2C4CDEE-4CB6-49C1-8DBF-4A1AE71954ED
ms.date: 02/15/2019
keywords:
- WDI_TLV_FTM_REQUEST_TIMEOUT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: d5f324bf21fbd9ded8949036e63a2e4584ad854e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63382890"
---
# <a name="wditlvftmrequesttimeout"></a>WDI_TLV_FTM_REQUEST_TIMEOUT

**WDI_TLV_FTM_REQUEST_TIMEOUT**細かいタイミング測定 (FTM) を完了するミリ秒単位の最大時間を含む TLV は、します。

この TLV がのタスク パラメーターで使用される[OID_WDI_TASK_REQUEST_FTM](oid-wdi-task-request-ftm.md)します。

## <a name="tlv-type"></a>TLV 型

0x161

## <a name="length"></a>長さ

Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値

| 型 | 説明 |
| --- | --- |
| UINT32 | FTM を完了する、ミリ秒単位の最大時間。 タイムアウトは、ターゲットの数を掛けた 150 ミリ秒に設定されます。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
