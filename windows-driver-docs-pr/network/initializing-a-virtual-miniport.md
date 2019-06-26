---
title: 仮想ミニポートの初期化
description: 仮想ミニポートの初期化
ms.assetid: 5f2e23a9-375b-4b0d-95d2-5a3af1acb3be
keywords:
- 初期化中の仮想ミニポート
- 仮想ミニポート WDK ネットワーク
- NDIS 中間ドライバー WDK、仮想ミニポート
- 中間ドライバー WDK、仮想ネットワークのミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2900e4c7b800b2d6f004ad60ad121b2b9f2eef8e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381302"
---
# <a name="initializing-a-virtual-miniport"></a>仮想ミニポートの初期化





仮想ミニポートの初期化を開始する中間のドライバーを呼び出し、 [ **NdisIMInitializeDeviceInstanceEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisiminitializedeviceinstanceex)関数。 通常、中間のドライバーでは、この呼び出しからその[ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)関数。 ドライバーの中間の呼び出し後**NdisIMInitializeDeviceInstanceEx**プラグを Play manager 要求の仮想デバイスを起動する NDIS、NDIS 呼び出してドライバーの[ *MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)関数。

呼び出し*MiniportInitializeEx*のコンテキストでできる**NdisIMInitializeDeviceInstanceEx**が開始する前に仮想デバイスのプラグ アンド プレイ manager 場合**NdisIMInitializeDeviceInstanceEx**を返します。 中間のドライバーでは、1 つ以上の仮想ミニポートを提供する場合、ドライバーを呼び出す必要があります**NdisIMInitializeDeviceInstanceEx**の各仮想ミニポート利用可能にします。

NDIS に初期化パラメーターを渡す*MiniportInitializeEx*で、 [ **NDIS\_ミニポート\_INIT\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_init_parameters)構造体*MiniportInitParameters*します。 **IMDeviceInstanceContext**構造体のメンバーが仮想デバイスのコンテキストの領域へのポインターを指定します。 ドライバーへのポインターを渡された、 [ **NdisIMInitializeDeviceInstanceEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisiminitializedeviceinstanceex)関数の*DeviceContext*パラメーター。

*MiniportInitializeEx*、中間のドライバーが仮想ミニポートを初期化するために必要な操作を実行します。 この初期化は、他のミニポート アダプタの初期化に似ています。

 

 





