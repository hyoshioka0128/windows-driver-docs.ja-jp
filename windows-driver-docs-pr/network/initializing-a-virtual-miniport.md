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
ms.openlocfilehash: 737dc0e97e8aef5ce5cacb172676c84c150049df
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578611"
---
# <a name="initializing-a-virtual-miniport"></a>仮想ミニポートの初期化





仮想ミニポートの初期化を開始する中間のドライバーを呼び出し、 [ **NdisIMInitializeDeviceInstanceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff562727)関数。 通常、中間のドライバーでは、この呼び出しからその[ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)関数。 ドライバーの中間の呼び出し後**NdisIMInitializeDeviceInstanceEx**プラグを Play manager 要求の仮想デバイスを起動する NDIS、NDIS 呼び出してドライバーの[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数。

呼び出し*MiniportInitializeEx*のコンテキストでできる**NdisIMInitializeDeviceInstanceEx**が開始する前に仮想デバイスのプラグ アンド プレイ manager 場合**NdisIMInitializeDeviceInstanceEx**を返します。 中間のドライバーでは、1 つ以上の仮想ミニポートを提供する場合、ドライバーを呼び出す必要があります**NdisIMInitializeDeviceInstanceEx**の各仮想ミニポート利用可能にします。

NDIS に初期化パラメーターを渡す*MiniportInitializeEx*で、 [ **NDIS\_ミニポート\_INIT\_パラメーター** ](https://msdn.microsoft.com/library/windows/hardware/ff565972)構造体*MiniportInitParameters*します。 **IMDeviceInstanceContext**構造体のメンバーが仮想デバイスのコンテキストの領域へのポインターを指定します。 ドライバーへのポインターを渡された、 [ **NdisIMInitializeDeviceInstanceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff562727)関数の*DeviceContext*パラメーター。

*MiniportInitializeEx*、中間のドライバーが仮想ミニポートを初期化するために必要な操作を実行します。 この初期化は、他のミニポート アダプタの初期化に似ています。

 

 





