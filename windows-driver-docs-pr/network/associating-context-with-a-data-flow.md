---
title: コンテキストとデータ フローの関連付け
description: コンテキストとデータ フローの関連付け
ms.assetid: 75f5838e-626d-4a59-810e-fec9a40640ed
keywords:
- WDK Windows フィルタ リング プラットフォーム、データ フローに関連付けられたコンテキストのコールアウトを分類します。
- コンテキスト WDK Windows フィルタ リング プラットフォーム
- flowContext パラメーター WDK Windows フィルタ リング プラットフォーム
- WDK Windows Filtering Platform のデータ フローとコンテキストの関連付け
ms.date: 01/14/2019
ms.localizationpriority: medium
ms.openlocfilehash: 737e0598b7bc2e6575d899028f8dea5933f0c61c
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57348577"
---
# <a name="associating-context-with-a-data-flow"></a>コンテキストとデータ フローの関連付け


データ フローをサポートするフィルタ リング層でデータを処理する吹き出し、コールアウト ドライバーは、各データ フローでコンテキストを関連付けることができます。 このようなコンテキストでは、フィルター エンジンに対して非透過的です。 吹き出しの[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887)コールアウト関数はこのコンテキストを使用して、そのデータ フローのフィルター エンジンによって呼び出されたときに [次へ] に、データ フローに固有の状態情報を保存します。 フィルター エンジンでは、このコンテキストを渡しますを通じて吹き出しの classifyFn コールアウト関数に、 *flowContext*パラメーター。 コンテキストが、データ フローに関連付けられていない場合、 *flowContext*パラメーターが 0 です。

Flow では、データ、吹き出しのコンテキストの関連付け[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887)コールアウト関数呼び出し、 [ **FwpsFlowAssociateContext0** ](https://msdn.microsoft.com/library/windows/hardware/ff551165)関数。 例:

```cpp
// Context structure to be associated with data flows
typedef struct FLOW_CONTEXT_ {
  .
  .  // Driver-specific content
  .
} FLOW_CONTEXT, *PFLOW_CONTEXT;

#define FLOW_CONTEXT_POOL_TAG 'fcpt'

// classifyFn callout function
VOID NTAPI
 ClassifyFn(
    IN const FWPS_INCOMING_VALUES0  *inFixedValues,
    IN const FWPS_INCOMING_METADATA_VALUES0  *inMetaValues,
    IN OUT VOID  *layerData,
    IN const FWPS_FILTER0  *filter,
    IN UINT64  flowContext,
    IN OUT FWPS_CLASSIFY_OUT  *classifyOut
  )
{
  PFLOW_CONTEXT context;
  UINT64 flowHandle;
  NTSTATUS status;

  ...

  // Check for the flow handle in the metadata
  if (FWPS_IS_METADATA_FIELD_PRESENT(
      inMetaValues,
      FWPS_METADATA_FIELD_FLOW_HANDLE))
  {
    // Get the flow handle
    flowHandle = inMetaValues->flowHandle;

    // Allocate the flow context structure
    context =
      (PFLOW_CONTEXT)ExAllocatePoolWithTag(
        NonPagedPool,
        sizeof(FLOW_CONTEXT),
        FLOW_CONTEXT_POOL_TAG
      );

    // Check the result of the memory allocation
    if (context == NULL) 
    {
 
      // Handle memory allocation error
      ...
    }
    else
    {

      // Initialize the flow context structure
      ...

      // Associate the flow context structure with the data flow
      status = FwpsFlowAssociateContext0(
                flowHandle,
                FWPS_LAYER_STREAM_V4,
                calloutId,
                (UINT64)context
              );

      // Check the result
      if (status != STATUS_SUCCESS)
      {
        // Handle error
        ...
      }
    }
  }

  ...

}
```

コンテキストが既にデータ フローに関連付けられている場合にする必要がありますまず前に削除する新しいコンテキストをデータ フローを関連付けることができます。 データ フロー、吹き出しからのコンテキストを削除する[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887)コールアウト関数呼び出し、 [ **FwpsFlowRemoveContext0** ](https://msdn.microsoft.com/library/windows/hardware/ff551169)関数。 例:

```C++
// Context structure to be associated with data flows
typedef struct FLOW_CONTEXT_ {
  ...
} FLOW_CONTEXT, *PFLOW_CONTEXT;

#define FLOW_CONTEXT_POOL_TAG 'fcpt'

// classifyFn callout function
VOID NTAPI
 ClassifyFn(
    IN const FWPS_INCOMING_VALUES0  *inFixedValues,
    IN const FWPS_INCOMING_METADATA_VALUES0  *inMetaValues,
    IN OUT VOID  *layerData,
    IN const FWPS_FILTER0  *filter,
    IN UINT64  flowContext,
    OUT FWPS_CLASSIFY_OUT  *classifyOut
  )
{
  PFLOW_CONTEXT context;
  UINT64 flowHandle;
  NTSTATUS status;

  ...

  // Check for the flow handle in the metadata
 if (FWPS_IS_METADATA_FIELD_PRESENT(
    inMetaValues,
    FWPS_METADATA_FIELD_FLOW_HANDLE))
  {
    // Get the flow handle
     flowHandle = inMetaValues->flowHandle;

    // Check whether there is a context associated with the data flow
     if (flowContext != 0) 
     {
        // Get a pointer to the flow context structure
        context = (PFLOW_CONTEXT)flowContext;

        // Remove the flow context structure from the data flow
        status = FwpsFlowRemoveContext0(
                  flowHandle,
                  FWPS_LAYER_STREAM_V4,
                  calloutId
                );

      // Check the result
      if (status != STATUS_SUCCESS)
      {
        // Handle error
        ...
      }

      // Cleanup the flow context structure
      ...

      // Free the memory for the flow context structure
      ExFreePoolWithTag(
        context,
        FLOW_CONTEXT_POOL_TAG
        );
    }
  }

  ...

}
```

前の例で、 *calloutId*変数にはコールアウトのランタイム識別子が含まれています。 ランタイム識別子は、フィルター エンジンに登録される引き出し線とコールアウト ドライバー コールアウト ドライバーに返された同じ識別子です。