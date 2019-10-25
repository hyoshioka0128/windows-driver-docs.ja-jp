---
title: 仮想ミニポートの初期化
description: 仮想ミニポートの初期化
ms.assetid: 5f2e23a9-375b-4b0d-95d2-5a3af1acb3be
keywords:
- 仮想ミニポートの初期化
- 仮想ミニポート WDK ネットワーク
- NDIS 中間ドライバー WDK、仮想ミニポート
- 中間ドライバー WDK ネットワーク、仮想ミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c63bc08df4e433c1784da4b64cca0d5fa5be3c83
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824496"
---
# <a name="initializing-a-virtual-miniport"></a>仮想ミニポートの初期化





仮想ミニポートの初期化を開始するために、中間ドライバーは[**NdisIMInitializeDeviceInstanceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiminitializedeviceinstanceex)関数を呼び出します。 通常、中間ドライバーは、その[*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数からこの呼び出しを行います。 中間ドライバーが**NdisIMInitializeDeviceInstanceEx**を呼び出し、プラグアンドプレイマネージャーが ndis に仮想デバイスを起動するように要求すると、ndis はドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出します。

**NdisIMInitializeDeviceInstanceEx**が返される前にプラグアンドプレイマネージャーが仮想デバイスを起動する場合は、 *MiniportInitializeEx*への呼び出しを**NdisIMInitializeDeviceInstanceEx**のコンテキストで行うことができます。 中間ドライバーが複数の仮想ミニポートを提供する場合、ドライバーは、使用可能にする各仮想ミニポートに対して**NdisIMInitializeDeviceInstanceEx**を呼び出す必要があります。

NDIS は、 *MiniportInitializeEx*に初期化パラメーターを渡します。これは、 [**NDIS\_ミニポート\_INIT\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_init_parameters)構造体で、 *miniportinitparameters*にあります。 構造体の**Imdeviceinstancecontext**メンバーは、仮想デバイスのコンテキスト領域へのポインターを指定します。 ドライバーは、このポインターを*Devicecontext*パラメーターで[**NdisIMInitializeDeviceInstanceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiminitializedeviceinstanceex)関数に渡しました。

*MiniportInitializeEx*では、中間ドライバーは仮想ミニポートを初期化するために必要な操作を実行します。 この初期化は、他のすべてのミニポートアダプターの初期化に似ています。

 

 





