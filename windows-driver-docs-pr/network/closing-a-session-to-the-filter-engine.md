---
title: フィルター エンジンへのセッションを閉じる
description: フィルター エンジンへのセッションを閉じる
ms.assetid: e145fb8c-fe9f-4834-8df0-f2ceb5b13b09
keywords:
- Windows Filtering Platform コールアウト ドライバー WDK、セッションの終了
- コールアウト ドライバー WDK Windows フィルタ リング プラットフォーム、セッションの終了
- フィルター エンジン WDK Windows フィルタ リング プラットフォーム
- 終了は、エンジン セッション WDK Windows フィルタ リング プラットフォームのフィルター処理します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff129f1a737643dc3ee0cc8e2eeb286680aa4835
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384216"
---
# <a name="closing-a-session-to-the-filter-engine"></a>フィルター エンジンへのセッションを閉じる


コールアウト ドライバーが必要な管理タスクを実行した後は、フィルター エンジンへのセッションが閉じる必要があります。 コールアウト ドライバーは呼び出すことによって、 [ **FwpmEngineClose0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpmk/nf-fwpmk-fwpmengineclose0)関数。 例:

```C++
status =
 FwpmEngineClose0(
 engineHandle  // An handle to the open session
    );
```

 

 





