---
title: リトリートおよびアドバンス操作
description: リトリートおよびアドバンス操作
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
ms.openlocfilehash: 03bc41e1ba5bc8af3061492005ab700b23ce06e1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373886"
---
# <a name="retreat-and-advance-operations"></a>リトリートおよびアドバンス操作





NDIS を操作する撤退と高度な機能を提供します[ **NET\_バッファー** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer)構造体。 [退却操作](retreat-operations.md)行っている*使用データ領域*現在のドライバーを使用できます。 [操作を進める](advance-operations.md)リリース*使用データ領域*します。

送信操作中に撤退の操作が必要なまたはドライバーが返されるときに、基になるドライバーにデータを受信します。 たとえば、送信操作中にドライバーを呼び出すことができます、 [ **NdisRetreatNetBufferDataStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisretreatnetbufferdatastart)ヘッダー データの領域を確保する関数。

送信操作が完了すると、またはドライバーが、基になるドライバーからデータを受信すると、高度な操作が必要です。 たとえば、受信操作中にドライバーを呼び出すことができます、 [ **NdisAdvanceNetBufferDataStart** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisadvancenetbufferdatastart)下位レベルのドライバーで使用されたヘッダーのデータをスキップする関数。 この場合、ヘッダー データはバッファー、*未使用データ領域*します。

次の図は、ネットワーク データとこれらの操作間のリレーションシップを示します。

![データ領域の割り当てを示す図](images/netbufferdata-basic.png)

事前と撤退操作の詳細については、以下のトピックです。

[撤退操作](retreat-operations.md)

[高度な操作](advance-operations.md)

 

 





