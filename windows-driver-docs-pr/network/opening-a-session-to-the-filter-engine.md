---
title: フィルター エンジンへのセッションを開く
description: フィルター エンジンへのセッションを開く
ms.assetid: 23db0e2d-7f27-4323-801c-346e14f0f83e
keywords:
- Windows Filtering Platform コールアウト ドライバー WDK、セッションを開く
- コールアウト ドライバー WDK Windows フィルタ リング プラットフォーム、セッションを開く
- フィルター エンジン WDK Windows フィルタ リング プラットフォーム
- 開くフィルター エンジン セッション WDK Windows フィルタ リング プラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 455f6b34ad5e1bc6551de23406673649cf5136bf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384228"
---
# <a name="opening-a-session-to-the-filter-engine"></a>フィルター エンジンへのセッションを開く


コールアウト ドライバーでは、フィルター エンジンにフィルターを追加するなどの管理タスクを実行するフィルター エンジンへのセッションを開く必要があります。 コールアウト ドライバーを呼び出すことによって、フィルター エンジンにセッションを開くと、 [ **FwpmEngineOpen0** ](https://msdn.microsoft.com/library/windows/hardware/ff550075)関数。 次に、例を示します。

```cpp
HANDLE engineHandle;
NTSTATUS status;

// Open a session to the filter engine
status =
 FwpmEngineOpen0(
    NULL,              // The filter engine on the local system
    RPC_C_AUTHN_WINNT, // Use the Windows authentication service
    NULL,              // Use the calling thread's credentials
    NULL,              // There are no session-specific parameters
    &engineHandle      // Pointer to a variable to receive the handle
    );
```

コールアウト ドライバーでは、フィルター エンジンへのセッションを正常に開きましたが後、は、その他の Windows フィルタ リング プラットフォームの管理関数を呼び出す、返されたハンドルを使用できます。

 

 





