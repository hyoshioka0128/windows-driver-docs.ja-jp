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
ms.openlocfilehash: 36fa9f32eacb042d91c44ff8578f8af89011fcc8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385473"
---
# <a name="processing-flow-delete-callouts"></a>フロー削除コールアウトの処理


フィルター エンジンは吹き出しの呼び出しますコールアウトで処理されているデータ フローが停止したら、 [ *flowDeleteFn* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_callout_flow_delete_notify_fn0)コールアウト ドライバーでは、データにコンテキストを以前が関連付けられている場合、引き出し関数フロー。 吹き出しの*flowDeleteFn*コールアウト関数のコールアウト ドライバーに関連付けられているデータ フロー、データ フローが停止する前にコンテキストをクリーンアップするのに必要なを実行します。

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

フィルター エンジンは、データ フローが停止したときに、データ フローに吹き出しが関連付けられたコンテキストを自動的に削除されます。 そのため、コールアウトを呼び出す必要はありません、 [ **FwpsFlowRemoveContext0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsflowremovecontext0)関数からその[ *flowDeleteFn* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_callout_flow_delete_notify_fn0)コールアウト関数データ フローからコンテキストを削除します。

 

 





