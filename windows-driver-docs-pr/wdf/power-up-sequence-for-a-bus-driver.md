---
title: バス ドライバーの電源投入シーケンス
description: バス ドライバーの電源投入シーケンス
ms.assetid: 689746F4-E1A5-40BA-9FC4-29B0702D6E3E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9b16f77a7341119f7a971f9225067aa33e08046
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842240"
---
# <a name="power-up-sequence-for-a-bus-driver"></a>バス ドライバーの電源投入シーケンス


次の図は、デバイスを完全に動作状態にするときに、図の下部にあるデバイスが挿入された状態から開始すると、フレームワークが KMDF bus ドライバーのイベントコールバック関数を呼び出す順序を示しています。

![バスドライバーの電源投入シーケンス](images/pdo-powerup.png)

フレームワークは、対応するデバイスがシステムから物理的に削除されるまで、PDO を物理的には削除しません。 たとえば、ユーザーがデバイスマネージャーでデバイスを無効にしても、物理的には削除しない場合、フレームワークはそのデバイスオブジェクトを保持します。 このため、図の下部にある3つの手順はプラグアンドプレイ列挙中にのみ発生します。つまり、最初の起動時またはユーザーが新しいデバイスを挿入したときに発生します。 デバイスが既に無効になっていて物理的に削除されていない場合、フレームワークは[*Evtdevicepreparehardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバックを呼び出すことによって起動します。

 

 





