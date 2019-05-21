---
title: WIA_IPS_PRINTER_ENDORSER_COUNTER_DIGITS
description: WIA_IPS_PRINTER_ENDORSER_COUNTER_DIGITS プロパティには、常にページ カウンターに印刷する最小桁数がについて説明します。
keywords:
- WIA_IPS_PRINTER_ENDORSER_COUNTER_DIGITS イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_IPS_PRINTER_ENDORSER_COUNTER_DIGITS
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: e9f5f675abdfbaf8a044c6a875fae7d34de74dda
ms.sourcegitcommit: 2ddaca0dbaf96076ad54d39ac1e77d91e644de67
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2019
ms.locfileid: "65958680"
---
# <a name="wiaipsprinterendorsercounterdigits"></a>WIA\_IP\_プリンター\_裏書き\_カウンター\_桁の数字

**WIA\_IP\_プリンター\_裏書き\_カウンター\_桁**プロパティは、常にページ カウンターに印刷する最小桁数をについて説明します。 残りの空の数字、存在する場合は必須で指定された埋め込み文字で、 [ **WIA\_IP\_プリンター\_裏書き\_PADDING** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-printer-endorser-padding)、サポートされている場合は、プロパティ、またはゼロ (0) それ以外の場合。

このプロパティは初期化され、WIA ミニ ドライバーによって維持されます。

プロパティの種類:VT\_UI4

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

## <a name="remarks"></a>注釈

このプロパティは省略可能と・ インプリント ・/機能の有効な項目をサポートする、 [ **WIA\_IP\_プリンター\_裏書き\_有効\_形式\_指定子**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-printer-endorser-valid-format-specifiers)プロパティを**WIA\_印刷\_ページ\_カウント**値。 実装された場合、プロパティの値がゼロ (0) より厳密に大きい場合があります。

## <a name="requirements"></a>必要条件

| &nbsp; | &nbsp; |
| --- |:--- |
| **ヘッダー** | Wiadef.h (Wiadef.h を含む) |
