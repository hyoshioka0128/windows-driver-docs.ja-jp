---
title: デバッグ \_ OUTCB \_ XXX
description: DEBUG \_ outputcb \_ XXX 定数は出力フラグです。 出力フラグは、それに付随する出力の種類を示すビットフィールドを形成します。
ms.date: 11/28/2018
topic_type:
- apiref
api_name:
- DEBUG_OUTCB_TEXT
- DEBUG_OUTCB_DML
- DEBUG_OUTCB_EXPLICIT_FLUSH
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: ce23bc0a751c52eab4eaf65fb84c9965330c7403
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968021"
---
# <a name="debug_outcb_xxx"></a>デバッグ \_ OUTCB \_ XXX


DEBUG \_ outcb \_ XXX 定数は出力フラグです。 出力フラグは、それに付随する出力の種類を示すビットフィールドを形成します。

デバッグ \_ outcb \_ XXX は、Output2 に送信できるさまざまな種類の出力コールバック通知を定義します。

指定できる値は次のとおりです。

|定数|説明|
|-----|-------|
|DEBUG_OUTCB_TEXT|プレーンテキストコンテンツ、フラグは次のとおりです。引数は mask です。|
|DEBUG_OUTCB_DML|デバッガーのマークアップコンテンツ、フラグは次のとおりです。引数は mask です。|
|DEBUG_OUTCB_EXPLICIT_FLUSH|明示的な出力フラッシュ、フラグ、および引数の通知は0です。|


<a name="requirements"></a>要件
------------

**ヘッダー**: dbgeng .H (dbgeng .h を含む)


 

 





