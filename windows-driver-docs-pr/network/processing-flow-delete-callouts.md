---
title: 処理フローの削除の吹き出し
description: 処理フローの削除の吹き出し
ms.assetid: e947b3b3-27c6-408f-aa02-6b20fa1b9748
keywords:
- Windows Filtering Platform コールアウト ドライバー WDK、フローの削除の吹き出し
- コールアウト ドライバー WDK Windows フィルタ リング プラットフォーム、フローのコールアウトを削除します。
- フローの削除コールアウト WDK Windows フィルタ リング プラットフォーム
- flowDeleteFn
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbc5ecb92c479723d6f39a3ae3df407c7d64becb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550994"
---
# <a name="processing-flow-delete-callouts"></a>処理フローの削除の吹き出し


フィルター エンジンは吹き出しの呼び出しますコールアウトで処理されているデータ フローが停止したら、 [ *flowDeleteFn* ](https://msdn.microsoft.com/library/windows/hardware/ff550025)コールアウト ドライバーでは、データにコンテキストを以前が関連付けられている場合、引き出し関数フロー。 吹き出しの*flowDeleteFn*コールアウト関数のコールアウト ドライバーに関連付けられているデータ フロー、データ フローが停止する前にコンテキストをクリーンアップするのに必要なを実行します。

次に、例を示します。

```C++
// Context structure to be associated with data flows
typedef struct FLOW_CONTEXT_ {
  ...
} FLOW_CONTEXT, *PFLOW_CONTEXT;

#define FLOW_CONTEXT_POOL_TAG &#39;fcpt&#39;

// flowDeleteFn callout function
VOID NTAPI
 FlowDeleteFn(
    IN UINT16  layerId,
    IN UINT32  calloutId,
    IN UINT64  flowContext
    )
{
  PFLOW_CONTEXT context;

  // Get the flow context structure
 context = (PFLOW_CONTEXT)flowContext;

  // Cleanup the flow context structure
  ...

  // Free the memory for the flow context structure
 ExFreePoolWithTag(
 context,
    FLOW_CONTEXT_POOL_TAG
    );
}
```

フィルター エンジンは、データ フローが停止したときに、データ フローに吹き出しが関連付けられたコンテキストを自動的に削除されます。 そのため、コールアウトを呼び出す必要はありません、 [ **FwpsFlowRemoveContext0** ](https://msdn.microsoft.com/library/windows/hardware/ff551169)関数からその[ *flowDeleteFn* ](https://msdn.microsoft.com/library/windows/hardware/ff550025)コールアウト関数データ フローからコンテキストを削除します。

 

 





