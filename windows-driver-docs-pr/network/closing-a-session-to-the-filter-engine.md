---
title: フィルター エンジンへのセッションを閉じる
description: フィルター エンジンへのセッションを閉じる
ms.assetid: e145fb8c-fe9f-4834-8df0-f2ceb5b13b09
keywords:
- Windows フィルタリングプラットフォームコールアウトドライバー WDK、セッションの終了
- コールアウトドライバー WDK Windows フィルタリングプラットフォーム、セッションの終了
- フィルターエンジン WDK Windows フィルタリングプラットフォーム
- フィルターエンジンセッションを閉じる WDK Windows フィルタリングプラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7efde17cc8c0ca1242a0d8e98ce9eee9e7cdf255
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838195"
---
# <a name="closing-a-session-to-the-filter-engine"></a>フィルター エンジンへのセッションを閉じる


コールアウトドライバーは、必要な管理タスクを実行した後、セッションをフィルターエンジンに対して終了します。 コールアウトドライバーは、 [**FwpmEngineClose0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpmk/nf-fwpmk-fwpmengineclose0)関数を呼び出すことによってこれを行います。 次に、例を示します。

```C++
status =
 FwpmEngineClose0(
 engineHandle  // An handle to the open session
    );
```

 

 





