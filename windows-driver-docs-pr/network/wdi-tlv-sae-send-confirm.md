---
title: WDI_TLV_SAE_SEND_CONFIRM
description: WDI_TLV_SAE_SEND_CONFIRM では、同時認証の Equals (SAE) 確認要求の送信の確認のフィールドが含まれる TLV です。
ms.assetid: F2251F48-7EED-460B-9EFD-554451E1172B
ms.date: 02/15/2019
keywords:
- WDI_TLV_SAE_SEND_CONFIRM ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 0c6405e10073daaef1bfdf5f0a196a3b8c45be42
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359053"
---
# <a name="wditlvsaesendconfirm"></a>WDI_TLV_SAE_SEND_CONFIRM

**WDI_TLV_SAE_SEND_CONFIRM**同時認証の Equals (SAE) 確認要求の送信の確認のフィールドが含まれる TLV です。 送信の確認 フィールドは、リプレイ カウンターとして使用されます。

この TLV がで使用される[WDI_TLV_SAE_CONFIRM_REQUEST](wdi-tlv-sae-confirm-request.md)します。

## <a name="tlv-type"></a>TLV 型

0x156

## <a name="length"></a>長さ

Uint16 型のサイズをバイト単位で。

## <a name="values"></a>値

| 型 | 説明 |
| --- | --- |
| UINT16 | 確認を送信フィールドです。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
