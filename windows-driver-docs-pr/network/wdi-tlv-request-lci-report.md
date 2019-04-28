---
title: WDI_TLV_REQUEST_LCI_REPORT
description: WDI_TLV_REQUEST_LCI_REPORT では、に関する情報を含むかどうか、場所の構成情報 (LCI 細かいタイミング測定 (FTM) 要求中にターゲット BSS からレポートを要求する必要があります TLV です。
ms.assetid: BFB15FF0-0272-4FDC-AD7A-94ECDA59D0ED
ms.date: 02/15/2019
keywords:
- WDI_TLV_REQUEST_LCI_REPORT ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 70c3c232db4b4dd0930a39df75b67fe02b072bcb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360167"
---
# <a name="wditlvrequestlcireport"></a>WDI_TLV_REQUEST_LCI_REPORT

**WDI_TLV_REQUEST_LCI_REPORT**細かいタイミング測定 (FTM) 要求時に場所の構成情報 (LCI) レポート要求ターゲット BSS から使用するかどうかの情報を含む TLV は、します。

この TLV がで使用される[WDI_TLV_FTM_TARGET_BSS_ENTRY](wdi-tlv-ftm-target-bss-entry.md)します。

## <a name="tlv-type"></a>TLV 型

0x158

## <a name="length"></a>長さ

UINT8 のサイズをバイト単位で。

## <a name="values"></a>値

| 型 | 説明 |
| --- | --- |
| UINT8 | 設定可能な値: <ul><li>0:LCI レポートは必要ありません。</li><li>1:LCI レポートを要求する必要があります。</li></ul> |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
