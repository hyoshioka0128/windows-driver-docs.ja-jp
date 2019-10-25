---
title: ネットワーク ドライバーの共有メモリの使用
description: ネットワーク ドライバーの共有メモリの使用
ms.assetid: f7dfe785-6c1a-4f56-9018-76be9cdec7fc
keywords:
- ネットワークドライバー WDK、共有メモリ
- メモリ WDK ネットワーク
- 共有メモリの WDK ネットワーク
- メモリアドレス空間の共有
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24c3ee96b9a8a162a6bd6744012604af0d006c13
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842973"
---
# <a name="using-shared-memory-in-network-drivers"></a>ネットワーク ドライバーの共有メモリの使用





バスマスタダイレクトメモリアクセス (DMA) デバイス用のミニポートドライバーは、ネットワークインターフェイスカード (NIC) およびミニポートドライバーによって使用される共有メモリを割り当てます。

[**NdisMAllocateSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismallocatesharedmemory)は、バスマスタミニポートドライバーによって呼び出され、ネットワークアダプターとミニポートドライバー間の永続的な共有にメモリを割り当てることができます。 この関数は、共有メモリの仮想アドレスと物理アドレスを返します。 アドレスは、 [**NdisMFreeSharedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismfreesharedmemory)を呼び出すとメモリが解放されるまで有効です。

 

 





