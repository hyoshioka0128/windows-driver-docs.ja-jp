---
title: リトリートおよびアドバンス操作
description: リトリートおよびアドバンス操作
ms.assetid: 90d4acae-e66c-486b-8b38-59f7fe159047
keywords:
- ネットワークデータ WDK, 事前操作
- ネットワークデータ WDK、retreat 操作
- データ WDK ネットワーク, 事前操作
- データ WDK ネットワーク、retreat 操作
- パケット WDK ネットワーク、事前操作
- パケット WDK ネットワーク、retreat 操作
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f290b62cae10ed8e9c50282631dd6c3917e8198
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842024"
---
# <a name="retreat-and-advance-operations"></a>リトリートおよびアドバンス操作





NDIS では、[**ネットワーク\_のバッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)構造を操作するための、retreat 関数と advance 関数が用意されています。 [Retreat 操作](retreat-operations.md)は、現在のドライバーで使用できる*データ領域*を増やします。 [前払い操作](advance-operations.md)のリリースで*使用されたデータ領域*。

Retreat 操作は、送信操作中、またはドライバーが基になるドライバーに受信したデータを返すときに必要です。 たとえば、送信操作中に、ドライバーは[**NdisRetreatNetBufferDataStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisretreatnetbufferdatastart)関数を呼び出して、ヘッダーデータ用の領域を確保できます。

事前操作は、送信操作が完了したとき、またはドライバーが基になるドライバーからデータを受信したときに必要です。 たとえば、受信操作中に、ドライバーは[**NdisAdvanceNetBufferDataStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisadvancenetbufferdatastart)関数を呼び出して、下位レベルのドライバーによって使用されていたヘッダーデータをスキップできます。 この場合、ヘッダーデータは*未使用のデータ領域*のバッファーに残ります。

次の図は、ネットワークデータとこれらの操作の関係を示しています。

![データ領域の割り当てを示す図](images/netbufferdata-basic.png)

次のトピックでは、advance 操作と retreat 操作の詳細について説明します。

[Retreat 操作](retreat-operations.md)

[詳細操作](advance-operations.md)

 

 





