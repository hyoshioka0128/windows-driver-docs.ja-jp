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
ms.openlocfilehash: 3ab0edc9e4e4c9225c7007f141cd25e037ab3173
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338429"
---
# <a name="closing-a-session-to-the-filter-engine"></a>フィルター エンジンへのセッションを閉じる


コールアウト ドライバーが必要な管理タスクを実行した後は、フィルター エンジンへのセッションが閉じる必要があります。 コールアウト ドライバーは呼び出すことによって、 [ **FwpmEngineClose0** ](https://msdn.microsoft.com/library/windows/hardware/ff550072)関数。 次に、例を示します。

```C++
status =
 FwpmEngineClose0(
 engineHandle  // An handle to the open session
    );
```

 

 





