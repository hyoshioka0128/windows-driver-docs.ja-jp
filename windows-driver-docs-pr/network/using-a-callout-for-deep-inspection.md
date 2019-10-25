---
title: 詳細検査へのコールアウトの使用
description: 詳細検査へのコールアウトの使用
ms.assetid: 464c74ae-5e37-41f1-b305-ef57039b28ba
keywords:
- コールアウトの分類 WDK Windows フィルタリングプラットフォーム、詳細な検査
- 詳細検査 WDK Windows フィルタリングプラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a3411b0f4a75a9303dbbbd7d46902f72ae5c224
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842999"
---
# <a name="using-a-callout-for-deep-inspection"></a>詳細検査へのコールアウトの使用


コールアウトが詳細検査を実行している場合[、その分類](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)関数は、固定データフィールド、メタデータフィールド、渡された未加工のパケットデータ、およびコンテキストに格納されている関連データの任意の組み合わせを調べることができます。フィルターまたはデータフローに関連付けられています。

次に、例を示します。

```C++
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
  PNET_BUFFER_LIST rawData;
  ...

  // Test for the FWPS_RIGHT_ACTION_WRITE flag to check the rights
  // for this callout to return an action. If this flag is not set,
  // a callout can still return a BLOCK action in order to VETO a
  // PERMIT action that was returned by a previous filter. In this
  // example the function just exits if the flag is not set.
 if (!(classifyOut->rights & FWPS_RIGHT_ACTION_WRITE))
  {
    // Return without specifying an action
 return;
  }

  // Get the data fields from inFixedValues
  ...

  // Get any metadata fields from inMetaValues
  ...

  // Get the pointer to the raw data
 rawData = (PNET_BUFFER_LIST)layerData;

  // Get any filter context data from filter->context
  ...

  // Get any flow context data from flowContext
  ...

  // Inspect the various data sources to determine
  // the action to be taken on the data
  ...

  // If the data should be permitted...
 if (...) {

    // Set the action to permit the data
 classifyOut->actionType = FWP_ACTION_PERMIT;

    // Check whether the FWPS_RIGHT_ACTION_WRITE flag should be cleared
 if (filter->flags & FWPS_FILTER_FLAG_CLEAR_ACTION_RIGHT)
    {
       // Clear the FWPS_RIGHT_ACTION_WRITE flag
 classifyOut->rights &= ~FWPS_RIGHT_ACTION_WRITE;
    }

 return;
  }

  ...

  // If the data should be blocked...
 if (...) {

    // Set the action to block the data
 classifyOut->actionType = FWP_ACTION_BLOCK;

    // Clear the FWPS_RIGHT_ACTION_WRITE flag
 classifyOut->rights &= ~FWPS_RIGHT_ACTION_WRITE;

 return;
  }

  ...

  // If the decision to permit or block should be passed
  // to the next filter in the filter engine...
 if (...) {

    // Set the action to continue with the next filter
 classifyOut->actionType = FWP_ACTION_CONTINUE;

 return;
  }

  ...
}
```

*ClassifyOut*パラメーターによって示される構造体の**actionType**メンバーで、コールアウトの[classid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)によってどのようなアクションが返されるかは、*フィルター処理&gt;アクション*の値によって決まります。 これらのアクションの詳細については、「 [**Fwps\_ACTION0**](https://docs.microsoft.com/windows/desktop/api/fwpstypes/ns-fwpstypes-fwps_action0_)構造体」を参照してください。

データを許可するかブロックする必要があるかを判断する前に、[コールアウトに](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)よってパケットデータの処理を追加で実行する必要がある場合は、データの処理が完了するまでパケットデータを保留する必要があります。 パケットデータを保留する方法の詳細については、「[種類のコールアウト](types-of-callouts.md)と[**FwpsPendOperation0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nf-fwpsk-fwpspendoperation0)」を参照してください。

一部のフィルターレイヤーでは、フィルターエンジンによってコールアウトの[classid の classid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)関数に渡されるレイヤー*データ*パラメーターが**NULL**です。

ストリームデータの詳細な検査を実行する方法については、「[ストリームデータの詳細な検査にコールアウトを使用](using-a-callout-for-deep-inspection-of-stream-data.md)する」を参照してください。

 

 





