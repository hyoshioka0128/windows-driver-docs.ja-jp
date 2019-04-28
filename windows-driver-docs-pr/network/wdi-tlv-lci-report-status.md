---
title: WDI_TLV_LCI_REPORT_STATUS
description: WDI_TLV_LCI_REPORT_STATUS は問題ありませんタイミング測定 (FTM) 要求中にいずれかが要求された場合、場所の構成情報 (LCI) レポートの状態の結果を含む TLV です。
ms.assetid: 81122FDB-3E1C-472D-80D2-1C8F29F00D2D
ms.date: 02/15/2019
keywords:
- WDI_TLV_LCI_REPORT_STATUS ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 2fa629a2ef72b9e83df9e56f83b323644399b255
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365362"
---
# <a name="wditlvlcireportstatus"></a>WDI_TLV_LCI_REPORT_STATUS

**WDI_TLV_LCI_REPORT_STATUS**細かいタイミング測定 (FTM) 要求中にいずれかが要求された場合、場所の構成情報 (LCI) レポートの状態の結果を含む TLV は、します。

この TLV がで使用される[WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)します。

## <a name="tlv-type"></a>TLV 型

0x15F

## <a name="length"></a>長さ

Uint32 型のサイズをバイト単位で。

## <a name="values"></a>値

| 型 | 説明 |
| --- | --- |
| [**WDI_LCI_REPORT_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_lci_report_status) | LCI レポートの状態です。 |

## <a name="requirements"></a>必要条件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
