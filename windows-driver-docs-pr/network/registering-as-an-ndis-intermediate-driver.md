---
title: NDIS 中間ドライバーとしての登録
description: NDIS 中間ドライバーとしての登録
ms.assetid: 4a095fa7-0d8f-4d7d-885c-bc43cd34c784
keywords:
- 中間ドライバーの登録
- 中間ドライバー WDK ネットワーク、登録
- NDIS 中間ドライバー WDK、登録
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a241f8ad4f596fa63b10936a6f86741503193f03
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842083"
---
# <a name="registering-as-an-ndis-intermediate-driver"></a>NDIS 中間ドライバーとしての登録





NDIS 中間ドライバーは、その[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)関数のコンテキストで、 *miniportxxx*関数とその*protocolxxx*関数を ndis に登録する必要があります。 *Miniportxxx*関数を登録するには、中間ドライバーは、NDIS\_中間\_ドライバーフラグが設定された状態で[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)を呼び出す必要があります。 このフラグは、ドライバーが*Miniportdrivercharacteristics*に渡す、 [**NDIS\_ミニポート\_ドライバー\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)の構造にあります。 この呼び出しは、中間ドライバーの*Miniportxxx*関数をエクスポートします。 *Miniportxxx*関数の登録の詳細については、「[ミニポートドライバーとしての中間ドライバーの登録](registering-an-intermediate-driver-as-a-miniport-driver.md)」を参照してください。

中間ドライバーは、仮想ミニポートが初期化されるタイミングを制御します。したがって、ドライバーがアダプターで送信と要求を受け入れる準備ができていることを確認します。 NDIS は、プラグアンドプレイ (PnP) マネージャーが仮想ミニポートデバイスを起動した後、中間ドライバーが[**NdisIMInitializeDeviceInstanceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiminitializedeviceinstanceex)を呼び出した後、中間ドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出します。ドライブ. *MiniportInitializeEx*の呼び出しは、後で発生する可能性があるため、必ずしも**NdisIMInitializeDeviceInstanceEx**の呼び出しのコンテキスト内にあるとは限りません。 中間ドライバーが複数の仮想ミニポートをエクスポートする場合、ドライバーは、ネットワーク要求に使用できるようにする各仮想ミニポートに対して**NdisIMInitializeDeviceInstanceEx**を呼び出す必要があります。

*Protocolxxx*関数を登録するには、中間ドライバーで[**NdisRegisterProtocolDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisregisterprotocoldriver)関数を呼び出す必要があります。 *Protocolxxx*関数の登録の詳細については、「[プロトコルドライバーとしての中間ドライバーの登録](registering-an-intermediate-driver-as-a-protocol.md)」を参照してください。

 

 





