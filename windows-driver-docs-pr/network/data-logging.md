---
title: データのログ
description: データのログ
ms.assetid: 1e4f00e0-0fc6-459d-bbdd-02fbca5b9945
keywords:
- 吹き出しを分類する WDK Windows フィルタリングプラットフォーム、データログ
- WDK Windows フィルタリングプラットフォームのログ記録
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e812754f21123d251e60ac382185399bc27a8ae
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834978"
---
# <a name="data-logging"></a>データのログ


どのデータをログに記録するかを決定するために、コールアウトの[classid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)関数は、データフィールド、メタデータフィールド、および渡されたすべての生データの任意の組み合わせ、およびコンテキストに格納されている関連データを検査できます。フィルターまたはデータフローに関連付けられています。

たとえば、コールアウトがネットワーク層のフィルターによって破棄される受信 (受信) IPv4 パケットの数を追跡している場合、コールアウトは FWPM\_レイヤーのフィルターエンジンに追加され\_受信\_IPPACKET\_V4\_破棄されます。レイヤー. このような場合、コールアウトの[classid](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)関数は、次の例のようになります。

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


[Classid (場合)](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

 

 






