---
title: 撤退と高度な操作
description: 撤退と高度な操作
ms.assetid: 90d4acae-e66c-486b-8b38-59f7fe159047
keywords:
- ネットワーク データ WDK、高度な操作
- ネットワーク データ WDK、撤退操作
- データの WDK ネットワーク、高度な操作
- データの WDK ネットワー キング、撤退操作
- パケットの WDK ネットワーク、高度な操作
- パケット WDK ネットワー キング、撤退操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed28a175b80fa6a74e019968d00fffad49bba9c1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538957"
---
# <a name="retreat-and-advance-operations"></a>撤退と高度な操作





NDIS を操作する撤退と高度な機能を提供します[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376)構造体。 [退却操作](retreat-operations.md)行っている*使用データ領域*現在のドライバーを使用できます。 [操作を進める](advance-operations.md)リリース*使用データ領域*します。

送信操作中に撤退の操作が必要なまたはドライバーが返されるときに、基になるドライバーにデータを受信します。 たとえば、送信操作中にドライバーを呼び出すことができます、 [ **NdisRetreatNetBufferDataStart** ](https://msdn.microsoft.com/library/windows/hardware/ff564527)ヘッダー データの領域を確保する関数。

送信操作が完了すると、またはドライバーが、基になるドライバーからデータを受信すると、高度な操作が必要です。 たとえば、受信操作中にドライバーを呼び出すことができます、 [ **NdisAdvanceNetBufferDataStart** ](https://msdn.microsoft.com/library/windows/hardware/ff560703)下位レベルのドライバーで使用されたヘッダーのデータをスキップする関数。 この場合、ヘッダー データはバッファー、*未使用データ領域*します。

次の図は、ネットワーク データとこれらの操作間のリレーションシップを示します。

![データ領域の割り当てを示す図](images/netbufferdata-basic.png)

事前と撤退操作の詳細については、以下のトピックです。

[撤退操作](retreat-operations.md)

[高度な操作](advance-operations.md)

 

 





