---
title: NDIS 構成関数
description: NDIS 構成関数
ms.assetid: 248e08d0-6145-499a-b307-2a5ffbd3733f
keywords:
- WDK NDIS の構成関数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0229b025dc27fe2859e7e6642fbe77d138024c3b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387279"
---
# <a name="ndis-configuration-functions"></a>NDIS 構成関数





NDIS にはドライバーの構成を簡略化するには、次の関数が含まれています。

[**NdisOpenConfigurationEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenconfigurationex)

[**NdisMGetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismgetbusdata)

[**NdisMSetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetbusdata)

NDIS ミニポート ドライバーを呼び出し、アダプターの構成情報を取得する**NdisOpenConfigurationEx**と[**エミュレーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreadconfiguration)します。 ドライバーを呼び出すことができます**NdisMGetBusData** bus 固有の情報を取得します。 ドライバーを呼び出すことができます**NdisMSetBusData** bus 固有の情報を設定します。

プロトコル ドライバーでは、アダプターの名前へのレジストリ パスを使用して、ドライバーと基になるアダプター間のバインディングに固有の構成パラメーターを読み取ります。 NDIS への呼び出しで、レジストリ パスを提供する、 [ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)関数。 ドライバーは、このレジストリ パスを渡すことができます、 [ **NdisOpenProtocolConfiguration** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553683(v=vs.85))関数またはレジストリを直接呼び出します。 代わりに、ドライバーを渡すことができます、 *BindParameters*構造体を**NdisOpenConfigurationEx**を同じパラメーターを読み取る関数。

 

 





