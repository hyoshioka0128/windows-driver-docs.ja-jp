---
title: データのログ
description: データのログ
ms.assetid: 1e4f00e0-0fc6-459d-bbdd-02fbca5b9945
keywords:
- コールアウト WDK Windows フィルタ リング プラットフォーム、ログ データの分類します。
- WDK Windows フィルタ リング プラットフォームのログ記録
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 075f872abbb618643976eaa3cc5977098a6568a0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354619"
---
# <a name="data-logging"></a>データのログ


データを決定するログに記録、吹き出しの[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)コールアウト関数は、データ フィールド、メタデータ フィールド、およびそれに渡される任意の生データの任意の組み合わせと格納されている関連するデータを検査できますフィルターまたはデータに関連付けられたコンテキストのフロー。

たとえば、コールアウトは、受信 (受信) IPv4 パケットの数は、ネットワーク層でのフィルターによって破棄の追跡場合、コールアウトが、FWPM でフィルター エンジンに追加されます\_レイヤー\_受信\_IPPACKET\_V4\_破棄レイヤー。 この場合、引き出し線の[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)コールアウト関数次の例のようになります。

```C++
ULONG TotalDiscardCount = 0;
ULONG FilterDiscardCount = 0;

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
  // Increment the total count of discarded packets
 InterlockedIncrement(&TotalDiscardCount);


  // Check whether a discard reason metadata field is present
 if (FWPS_IS_METADATA_FIELD_PRESENT(
 inMetaValues,
        FWPS_METADATA_FIELD_DISCARD_REASON))
  {
    // Check whether it is a general discard reason
 if (inMetaValues->discardMetadata.discardModule ==
        FWPS_DISCARD_MODULE_GENERAL)
    {
      // Check whether discarded by a filter
 if (inMetaValues->discardMetadata.discardReason ==
          FWPS_DISCARD_FIREWALL_POLICY)
      {
        // Increment the count of packets discarded by a filter
 InterlockedIncrement(&FilterDiscardCount);
      }
    }
  }

  // Take no action on the data
 classifyOut->actionType = FWP_ACTION_CONTINUE;
}
```

## <a name="related-topics"></a>関連トピック


[classifyFn](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

 

 






