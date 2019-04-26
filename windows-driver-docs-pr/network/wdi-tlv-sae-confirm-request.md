---
title: WDI_TLV_SAE_CONFIRM_REQUEST
description: WDI_TLV_SAE_CONFIRM_REQUEST では、同時認証の Equals (SAE) 確認要求のパラメーターを含む TLV です。
ms.assetid: 9E46D8BA-D359-45B3-8074-FA54F4618E71
ms.date: 02/15/2019
keywords:
- WDI_TLV_SAE_CONFIRM_REQUEST ネットワーク ドライバーが Windows Vista 以降
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 2037de1054b6a4117fbe03a4bddbdf74fb8c5322
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359344"
---
# <a name="wditlvsaeconfirmrequest"></a>WDI_TLV_SAE_CONFIRM_REQUEST

**WDI_TLV_SAE_CONFIRM_REQUEST**同時認証の Equals (SAE) 確認要求のパラメーターを含む TLV です。 

この TLV がのコマンド パラメーターで使用される[OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md)します。

## <a name="tlv-type"></a>TLV 型

0x151

## <a name="length"></a>長さ

すべてのサイズ (バイト) を合計には、TLVs が含まれています。

## <a name="values"></a>値

| TLV | 種類 | 許可されている複数の TLV インスタンス | 省略可能 | 説明 |
| --- | --- | --- | --- | --- |
| [WDI_TLV_SAE_SEND_CONFIRM](wdi-tlv-sae-send-confirm.md) | UINT16 |   |   | 確認を送信フィールド、リプレイ カウンターとして使用します。 |
| [WDI_TLV_SAE_CONFIRM](wdi-tlv-sae-confirm.md) | TLV\<一覧\<UINT8 &GT;&GT; |  |   | 確認入力 フィールドにします。 |

## <a name="requirements"></a>要件

|   |   |
| --- | --- |
| サポートされている最小のクライアント | Windows 10 バージョン 1903 |
| サポートされている最小のサーバー | Windows Server 2016 |
| Header | Wditypes.hpp |
