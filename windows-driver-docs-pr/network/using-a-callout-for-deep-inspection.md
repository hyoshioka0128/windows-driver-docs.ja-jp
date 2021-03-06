---
title: 詳細検査へのコールアウトの使用
description: 詳細検査へのコールアウトの使用
ms.assetid: 464c74ae-5e37-41f1-b305-ef57039b28ba
keywords:
- WDK Windows フィルタ リング プラットフォーム、詳細な検査のコールアウトを分類します。
- 詳細な検査 WDK Windows フィルタ リング プラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90398573152f2a067fcdd237243f97084cbd155a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369631"
---
# <a name="using-a-callout-for-deep-inspection"></a>詳細検査へのコールアウトの使用


吹き出しの詳細な検査を実行するときにその[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)コールアウト関数は、固定のデータ フィールド、メタデータ フィールド、およびそれに渡されるすべての未処理のパケット データの任意の組み合わせとされている、関連するデータを検査できますフィルターまたはデータに関連付けられたコンテキストに格納されているフロー。

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

値*フィルター -&gt;action.type*吹き出しのアクションを決定します[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)に吹き出し関数が返す必要があります、 **actionType**メンバー指す構造体の*classifyOut*パラメーター。 これらのアクションの詳細については、次を参照してください。、 [ **FWPS\_ACTION0** ](https://docs.microsoft.com/windows/desktop/api/fwpstypes/ns-fwpstypes-fwps_action0_)構造体。

コールアウトは、外側のパケット データの追加の処理を実行する必要がある場合その[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)コールアウト関数、データの許可またはブロックする必要があります、かどうかにする必要があります保留パケット データの処理までを決定できる前に、データが完了するとします。 パケット データを保留する方法については、次を参照してください。[型のコールアウト](types-of-callouts.md)と[ **FwpsPendOperation0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpspendoperation0)します。

いくつかのレイヤーをフィルター処理、*データ*吹き出しのフィルター エンジンによって渡されるパラメーター [classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)コールアウト関数は**NULL**します。

ストリーム データの詳細な検査を実行する方法については、次を参照してください。[コールアウトを使用して、Stream データの詳細な検査](using-a-callout-for-deep-inspection-of-stream-data.md)します。

 

 





