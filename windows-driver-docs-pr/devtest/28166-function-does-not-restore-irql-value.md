---
title: C28166
description: これを行うに必要な警告 C28166 の関数は IRQL を関数の開始時に現在、さらに値を復元しません。
ms.assetid: 5835b2e7-0a66-474c-ba1b-40618403075d
keywords:
- '警告は、WDK: PREfast for Drivers を一覧表示'
- 'エラーは、WDK: PREfast for Drivers を一覧表示'
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28166
ms.openlocfilehash: 9dc1669174b62b0db36a441be971d9fef2b56405
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361329"
---
# <a name="c28166"></a>C28166


C28166 を警告します。関数では、関数の開始時し、これを行うために必要な値に、IRQL が復元されません。

この警告は、関数があることを示します、  **\_IRQL\_必要\_同じ\_** 注釈、少なくとも 1 つのパスに関数の終了ではない、関数を使用ドライバーが関数のエントリで実行中の IRQL を IRQL を復元します。

通常、  **\_IRQL\_必要があります\_同じ\_** コールバック関数の注釈を使用します。

この警告を回避するドライバーする必要があります正しく、初期の IRQL の値を保存および復元はどのような関数の終了時に、同じ IRQL の値、  **\_IRQL\_必要\_同じ\_** 注釈をアサートします。

 

 





