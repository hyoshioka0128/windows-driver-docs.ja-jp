---
title: WDI_TLV_RETRY_AFTER
description: WDI_TLV_RETRY_AFTER は、ターゲット BSS から新しい問題タイミング測定 (FTM) を要求しようとする前に渡す必要がありますを秒単位で期間を格納する TLV です。
ms.assetid: BFB15FF0-0272-4FDC-AD7A-94ECDA59D0ED
ms.date: 02/15/2019
keywords:
- WDI_TLV_RETRY_AFTER ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 9c0375d4c9b2f382250606e252c072665f00b69a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360164"
---
# <a name="wditlvretryafter"></a>WDI_TLV_RETRY_AFTER

**WDI_TLV_RETRY_AFTER**ターゲット BSS から新しい問題タイミング測定 (FTM) を要求しようとする前に渡す必要がありますを秒単位で、期間を格納する TLV は、します。

この TLV がで使用される[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)します。

## <a name="tlv-type"></a>TLV 型

0x15A

## <a name="length"></a>長さ

Uint16 型のサイズをバイト単位で。

## <a name="values"></a>値

| 型 | 説明 |
| --- | --- |
| UINT16 | ターゲット BSS から新しい問題タイミング測定 (FTM) を要求しようとする前に渡す必要がありますを秒単位で期間です。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
