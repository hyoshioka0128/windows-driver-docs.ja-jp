---
title: ストリーム データの詳細検査へのコールアウトの使用
description: ストリーム データの詳細検査へのコールアウトの使用
ms.assetid: 433d2d9a-c95e-4315-8678-8614791cd529
keywords:
- コールアウトの分類 WDK Windows フィルタリングプラットフォーム、詳細な検査
- 詳細検査 WDK Windows フィルタリングプラットフォーム
- ストリームデータの詳細検査 WDK Windows フィルタリングプラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f3ab0281ebb3fe236196ce8947a0d422db860bf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842998"
---
# <a name="using-a-callout-for-deep-inspection-of-stream-data"></a>ストリーム データの詳細検査へのコールアウトの使用


コールアウトがストリームデータを検査すると[、その分類](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)関数は、固定データフィールド、メタデータフィールド、および渡された生のストリームデータの任意の組み合わせと、関連付けられたコンテキストに格納されている関連データを調べることができます。フィルターまたはデータフローを使用します。

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
  FWPS_STREAM_CALLOUT_IO_PACKET0 *ioPacket;
  FWPS_STREAM_BUFFER0 *dataStream;
  UINT32 bytesRequired;
  SIZE_T bytesToPermit;
  SIZE_T bytesToBlock;
  ...

  // Get a pointer to the stream callout I/O packet
 ioPacket = (FWPS_STREAM_CALLOUT_IO_PACKET0 *)layerData;

  // Get the data fields from inFixedValues
  ...

  // Get any metadata fields from inMetaValues
  ...

  // Get the pointer to the data stream
 dataStream = ioPacket->dataStream;

  // Get any filter context data from filter->context
  ...

  // Get any flow context data from flowContext
  ...

  // Inspect the various data sources to determine
  // the action to be taken on the data
  ...

  // If more stream data is required to make a determination...
 if (...) {

    // Let the filter engine know how many more bytes are needed
 ioPacket->streamAction = FWPS_STREAM_ACTION_NEED_MORE_DATA;
 ioPacket->countBytesRequired = bytesRequired;
 ioPacket->countBytesEnforced = 0;

    // Set the action to continue to the next filter
 classifyOut->actionType = FWP_ACTION_CONTINUE;

 return;
  }
  ...

  // If some or all of the data should be permitted...
 if (...) {

    // No stream-specific action is required
 ioPacket->streamAction = FWPS_STREAM_ACTION_NONE;

    // Let the filter engine know how many of the leading bytes
    // in the stream should be permitted
 ioPacket->countBytesRequired = 0;
 ioPacket->countBytesEnforced = bytesToPermit;

    // Set the action to permit the data
 classifyOut->actionType = FWP_ACTION_PERMIT;

 return;
  }

  ...

  // If some or all of the data should be blocked...
 if (...) {

    // No stream-specific action is required
 ioPacket->streamAction = FWPS_STREAM_ACTION_NONE;

    // Let the filter engine know how many of the leading bytes
    // in the stream should be blocked
 ioPacket->countBytesRequired = 0;
 ioPacket->countBytesEnforced = bytesToBlock;

    // Set the action to block the data
 classifyOut->actionType = FWP_ACTION_BLOCK;

 return;
  }

  ...

  // If the decision to permit or block should be passed
  // to the next filter in the filter engine...
 if (...) {

    // No stream-specific action is required
 ioPacket->streamAction = FWPS_STREAM_ACTION_NONE;

    // No bytes are affected by this callout
 ioPacket->countBytesRequired = 0;
 ioPacket->countBytesEnforced = 0;

 return;
  }

  ...
}
```

*ClassifyOut*パラメーターによって示される構造体の**actionType**メンバーで、コールアウトの[classid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)によってどのようなアクションが返されるかは、*フィルター処理&gt;アクション*の値によって決まります。 これらのアクションの詳細については、「 [**Fwps\_ACTION0**](https://docs.microsoft.com/windows/desktop/api/fwpstypes/ns-fwpstypes-fwps_action0_)構造体」を参照してください。

パケットおよびストリームデータ検査の詳細については、「[パケットおよびストリームデータの検査](inspecting-packet-and-stream-data.md)」を参照してください。

 

 





