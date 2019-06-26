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
ms.openlocfilehash: 46a3b49bf2b5ad3c0fca3dc5ff90ddfc001a7d15
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366558"
---
# <a name="opening-a-session-to-the-filter-engine"></a>フィルター エンジンへのセッションを開く


コールアウト ドライバーでは、フィルター エンジンにフィルターを追加するなどの管理タスクを実行するフィルター エンジンへのセッションを開く必要があります。 コールアウト ドライバーを呼び出すことによって、フィルター エンジンにセッションを開くと、 [ **FwpmEngineOpen0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpmk/nf-fwpmk-fwpmengineopen0)関数。 例:

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

 

 





