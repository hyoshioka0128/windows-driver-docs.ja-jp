---
title: フロー削除コールアウトの処理
description: フロー削除コールアウトの処理
ms.assetid: e947b3b3-27c6-408f-aa02-6b20fa1b9748
keywords:
- Windows Filtering Platform コールアウト ドライバー WDK、フローの削除の吹き出し
- コールアウト ドライバー WDK Windows フィルタ リング プラットフォーム、フローのコールアウトを削除します。
- フローの削除コールアウト WDK Windows フィルタ リング プラットフォーム
- flowDeleteFn
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc130d5246f663238fd1a65aa94811b1b190c159
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327650"
---
# <a name="processing-flow-delete-callouts"></a>フロー削除コールアウトの処理


フィルター エンジンは吹き出しの呼び出しますコールアウトで処理されているデータ フローが停止したら、 [ *flowDeleteFn* ](https://msdn.microsoft.com/library/windows/hardware/ff550025)コールアウト ドライバーでは、データにコンテキストを以前が関連付けられている場合、引き出し関数フロー。 吹き出しの*flowDeleteFn*コールアウト関数のコールアウト ドライバーに関連付けられているデータ フロー、データ フローが停止する前にコンテキストをクリーンアップするのに必要なを実行します。

例:

```C++
// Context structure to be associated with data flows
typedef struct FLOW_CONTEXT_ {
  ...
} FLOW_CONTEXT, *PFLOW_CONTEXT;

#define FLOW_CONTEXT_POOL_TAG 'fcpt'

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

 

 





