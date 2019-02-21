---
title: バス ドライバーの電源投入シーケンス
description: バス ドライバーの電源投入シーケンス
ms.assetid: 689746F4-E1A5-40BA-9FC4-29B0702D6E3E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27d2919a7aae5b8058417308fd5bd8ad85a1581c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551211"
---
# <a name="power-up-sequence-for-a-bus-driver"></a>バス ドライバーの電源投入シーケンス


次の図は、図の下部にあるデバイスが挿入された状態から開始、完全に operational 状態へのデバイスの追加時に、フレームワーク KMDF バス ドライバーのイベントのコールバック関数を呼び出す順序を示します。

![バス ドライバーの電源投入シーケンス](images/pdo-powerup.png)

フレームワークは、PDO が対応するデバイスは、システムから物理的に削除されるまで物理的に削除していません。 たとえば、ユーザーは、デバイス マネージャーでデバイスを無効にしますが、物理的に削除されません、フレームワークは、デバイス オブジェクトを保持します。 したがって、図の下部にある 3 つの手順はプラグ アンド プレイの列挙中にのみ発生: は、初期ブートまたはユーザーが新しいデバイスを挿入するときの中にします。 デバイスが以前無効になっていますが、物理的に削除、フレームワークが呼び出すことで起動、 [ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)コールバック。

 

 





