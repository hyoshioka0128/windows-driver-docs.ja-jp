---
title: デバッグ\_OUTCB\_XXX
description: デバッグ\_OUTPUTCB\_XXX 定数は、出力のフラグ。 出力のフラグは、それに伴う出力の種類を示すビット フィールドを形成します。
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
ms.openlocfilehash: 3aa4ac3c8b0bd599996574a6a02e0fbbe19842ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579765"
---
# <a name="debugoutcbxxx"></a>デバッグ\_OUTCB\_XXX


デバッグ\_OUTCB\_XXX 定数は、出力のフラグ。 出力のフラグは、それに伴う出力の種類を示すビット フィールドを形成します。

デバッグ\_OUTCB\_XXX Output2 に送信できる出力コールバック通知の種類を定義します。

使用可能な値は、次に示します。

|定数|説明|
|-----|-------|
|DEBUG_OUTCB_TEXT|以下のプレーン テキスト コンテンツ、フラグは、引数マスクです。|
|DEBUG_OUTCB_DML|デバッガー マークアップ コンテンツ、下のフラグは、引数マスクです。|
|DEBUG_OUTCB_EXPLICIT_FLUSH|明示的な出力フラッシュ、フラグ、および引数の通知には 0 です。|


<a name="requirements"></a>必要条件
------------

|||
|-----|-------|
|Header|DbgEng.h (DbgEng.h を含む)|

 

 





