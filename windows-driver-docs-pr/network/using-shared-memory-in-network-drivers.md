---
title: ネットワーク ドライバーの共有メモリの使用
description: ネットワーク ドライバーの共有メモリの使用
ms.assetid: f7dfe785-6c1a-4f56-9018-76be9cdec7fc
keywords:
- ネットワーク ドライバー WDK、共有メモリ
- メモリの WDK ネットワーク
- 共有メモリ WDK ネットワーク
- メモリ アドレス空間の共有
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80b41feb14999901e50a03014cb8b9484313f12d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354491"
---
# <a name="using-shared-memory-in-network-drivers"></a>ネットワーク ドライバーの共有メモリの使用





バス マスター ダイレクト メモリ アクセス (DMA) デバイス用のミニポート ドライバーは、ネットワーク インターフェイス カード (NIC) と、ミニポート ドライバーで使用するための共有メモリを割り当てます。

[**NdisMAllocateSharedMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismallocatesharedmemory)バス マスター ミニポート ドライバー、ネットワーク アダプターとミニポート ドライバーの間の永続的な共有メモリを割り当てることによって呼び出すことができます。 この関数は、仮想アドレスと共有メモリの物理アドレスを返します。 呼び出すまで、アドレスが有効な[ **NdisMFreeSharedMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismfreesharedmemory)メモリを解放します。

 

 





