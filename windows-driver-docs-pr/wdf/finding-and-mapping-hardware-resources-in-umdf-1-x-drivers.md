---
title: 検索と UMDF 1.x ドライバー内のハードウェア リソースのマッピング
description: 検索と UMDF 1.x ドライバー内のハードウェア リソースのマッピング
ms.assetid: 51CB254D-1B2C-43F5-925A-209810E2F5FC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94c5268c4512da8a60573f2229e5076f2c1a9457
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560454"
---
# <a name="finding-and-mapping-hardware-resources-in-umdf-1x-drivers"></a>検索と UMDF 1.x ドライバー内のハードウェア リソースのマッピング


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

UMDF バージョン 2.0 以降を使用している場合は、次を参照してください。[マッピング ハードウェア リソースの検索と](finding-and-mapping-hardware-resources.md)します。

1.x UMDF ドライバー内のハードウェア リソースを受け取るその[ **IPnpCallbackHardware2::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/hh439734)コールバック メソッド。 ドライバーを使用して、 [ **IWDFCmResourceList** ](https://msdn.microsoft.com/library/windows/hardware/hh439762)インターフェイスを翻訳済みのリソースの一覧を確認し、メモリ マップト レジスタ、I/O ポート、および割り込みを特定します。

ドライバーは、呼び出すことによって、リソースのリストを反復処理[ **IWDFCmResourceList::GetCount** ](https://msdn.microsoft.com/library/windows/hardware/hh439767)と[ **IWDFCmResourceList::GetDescriptor** ](https://msdn.microsoft.com/library/windows/hardware/hh439771).

ドライバーは、メモリ マップト レジスタを受信する場合、ドライバーを呼び出す必要があります[ **IWDFDevice3::MapIoSpace** ](https://msdn.microsoft.com/library/windows/hardware/hh451225)それらにアクセスできる前に、レジスタにマップします。 通常、ドライバーはマップでのレジスタの[ **IPnpCallbackHardware2::OnPrepareHardware** ](https://msdn.microsoft.com/library/windows/hardware/hh439734)メソッド。 ドライバーでのレジスタの割り当てを解除、 [ **IPnpCallbackHardware2::OnReleaseHardware** ](https://msdn.microsoft.com/library/windows/hardware/hh439739)呼び出すことによってコールバック[ **IWDFDevice3::UnmapIoSpace** ](https://msdn.microsoft.com/library/windows/hardware/hh451237). I/O ポートのマッピングは必要ないことに注意してください。

例については、ドライバーを検索し、メモリ マップト マップ リソースを登録する方法を示しますが、次を参照してください。 [ **IWDFDevice3::MapIoSpace**](https://msdn.microsoft.com/library/windows/hardware/hh451225)します。

 

 





