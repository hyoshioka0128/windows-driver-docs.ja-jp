---
title: WDI_TLV_LCI_REPORT_BODY
description: WDI_TLV_LCI_REPORT_BODY では、細かいタイミング Measuremement (FTM) 要求の場所の構成レポート (LCI) を含む TLV です。
ms.assetid: D80AB500-0B4F-47AC-ADF7-DDB5635FF1F2
ms.date: 02/15/2019
keywords:
- WDI_TLV_LCI_REPORT_BODY ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 6d92d7859feeac6e27efacab4574968369737bb1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390957"
---
# <a name="wditlvlcireportbody"></a>WDI_TLV_LCI_REPORT_BODY

**WDI_TLV_LCI_REPORT_BODY**細かいタイミング Measuremement (FTM) 要求の場所の構成レポート (LCI) を含む TLV は、します。

この TLV がで使用される[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)します。

## <a name="tlv-type"></a>TLV 型

0x160

## <a name="length"></a>長さ

UINT8 の要素の配列のサイズをバイト単位で。 配列には、1 つ以上の要素を含める必要があります。

## <a name="values"></a>値

| 型 | 説明 |
| --- | --- |
| UINT8[] | LCI レポートします。 |

## <a name="requirements"></a>必要条件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
