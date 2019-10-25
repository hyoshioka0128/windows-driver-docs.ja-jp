---
title: フィルター エンジンへのセッションを開く
description: フィルター エンジンへのセッションを開く
ms.assetid: 23db0e2d-7f27-4323-801c-346e14f0f83e
keywords:
- Windows フィルタリングプラットフォームのコールアウトドライバーの WDK、開いているセッション
- コールアウトドライバー WDK Windows フィルタリングプラットフォーム、開いているセッション
- フィルターエンジン WDK Windows フィルタリングプラットフォーム
- フィルターエンジンセッションを開く WDK Windows フィルタリングプラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c54fd6bf706ee5208d50e08a9462514fec0dcda
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843761"
---
# <a name="opening-a-session-to-the-filter-engine"></a>フィルター エンジンへのセッションを開く


コールアウトドライバーは、フィルターエンジンへのフィルターの追加などの管理タスクを実行するために、フィルターエンジンに対するセッションを開く必要があります。 コールアウトドライバーは、 [**FwpmEngineOpen0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpmk/nf-fwpmk-fwpmengineopen0)関数を呼び出すことによって、フィルターエンジンに対するセッションを開きます。 次に、例を示します。

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

コールアウトドライバーがフィルターエンジンへのセッションを正常に開くと、返されたハンドルを使用して、他の Windows フィルタリングプラットフォーム管理関数を呼び出すことができます。

 

 





