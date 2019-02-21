---
title: 共有ネットワーク ドライバーのメモリを使用
description: 共有ネットワーク ドライバーのメモリを使用
ms.assetid: f7dfe785-6c1a-4f56-9018-76be9cdec7fc
keywords:
- ネットワーク ドライバー WDK、共有メモリ
- メモリの WDK ネットワーク
- 共有メモリ WDK ネットワーク
- メモリ アドレス空間の共有
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 806c597dcb2e7193567c5b757ea541a3c5cba99a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559080"
---
# <a name="using-shared-memory-in-network-drivers"></a>共有ネットワーク ドライバーのメモリを使用





バス マスター ダイレクト メモリ アクセス (DMA) デバイス用のミニポート ドライバーは、ネットワーク インターフェイス カード (NIC) と、ミニポート ドライバーで使用するための共有メモリを割り当てます。

[**NdisMAllocateSharedMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff562782)バス マスター ミニポート ドライバー、ネットワーク アダプターとミニポート ドライバーの間の永続的な共有メモリを割り当てることによって呼び出すことができます。 この関数は、仮想アドレスと共有メモリの物理アドレスを返します。 呼び出すまで、アドレスが有効な[ **NdisMFreeSharedMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff563589)メモリを解放します。

 

 





