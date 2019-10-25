---
title: フロー削除コールアウトの処理
description: フロー削除コールアウトの処理
ms.assetid: e947b3b3-27c6-408f-aa02-6b20fa1b9748
keywords:
- Windows フィルタリングプラットフォームコールアウトドライバー WDK、フロー削除コールアウト
- コールアウトドライバー WDK Windows フィルタリングプラットフォーム、フロー削除コールアウト
- フロー削除コールアウト WDK Windows フィルタリングプラットフォーム
- flowDeleteFn
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0c5ca8806306a7a680ec2b1d71fa9fc10a38e16
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843487"
---
# <a name="processing-flow-delete-callouts"></a>フロー削除コールアウトの処理


コールアウトによって処理されているデータフローが停止した場合、コールアウトドライバーが以前にデータフローに関連付けられていた場合、フィルターエンジンはコールアウトの[*Flowdeletefn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_flow_delete_notify_fn0)コールアウト関数を呼び出します。 コールアウトの*Flowdeletefn*コールアウト関数は、データフローが停止する前に、データフローに関連付けられているコールアウトドライバーがコンテキストに必要なクリーンアップを実行します。

次に、例を示します。

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

フィルターエンジンは、データフローが停止したときに、データフローに関連付けられているコールアウトのコンテキストを自動的に削除します。 そのため、フローでは、 [*Flowdeletefn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_flow_delete_notify_fn0)コールアウト関数から[**FwpsFlowRemoveContext0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpsflowremovecontext0)関数を呼び出して、データフローからコンテキストを削除する必要はありません。

 

 





