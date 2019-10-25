---
title: NDIS 構成関数
description: NDIS 構成関数
ms.assetid: 248e08d0-6145-499a-b307-2a5ffbd3733f
keywords:
- 構成関数 WDK NDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44dfcebfbc70ec7f8a50c79f639252b3b8a383c9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823694"
---
# <a name="ndis-configuration-functions"></a>NDIS 構成関数





NDIS には、ドライバーの構成を簡素化するための次の関数が含まれています。

[**NdisOpenConfigurationEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenconfigurationex)

[**NdisMGetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismgetbusdata)

[**NdisMSetBusData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetbusdata)

アダプターの構成情報を取得するために、NDIS ミニポートドライバーは**NdisOpenConfigurationEx**と[**NdisReadConfiguration**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreadconfiguration)を呼び出します。 ドライバーは**NdisMGetBusData**を呼び出して、バス固有の情報を取得できます。 ドライバーは**NdisMSetBusData**を呼び出して、バス固有の情報を設定できます。

プロトコルドライバーは、アダプター名へのレジストリパスを使用して、ドライバーと基になるアダプターのバインドに固有の構成パラメーターを読み取ります。 NDIS は、 [*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数の呼び出しでレジストリパスを提供します。 ドライバーは、このレジストリパスを[**NdisOpenProtocolConfiguration**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553683(v=vs.85))関数に渡したり、レジストリ呼び出しを直接実行したりすることができます。 別の方法として、ドライバーは、 **NdisOpenConfigurationEx**関数に*bindparameters*構造体を渡して、同じパラメーターを読み取ることができます。

 

 





