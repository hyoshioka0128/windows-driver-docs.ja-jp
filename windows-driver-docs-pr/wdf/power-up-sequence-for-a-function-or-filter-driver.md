---
title: 関数またはフィルター ドライバーの電源投入シーケンス
description: 関数またはフィルター ドライバーの電源投入シーケンス
ms.assetid: 3E904641-A1E2-400C-A201-2D1D2D359657
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4d6093a9a544bf21eb829425f70374886985f41
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532599"
---
# <a name="power-up-sequence-for-a-function-or-filter-driver"></a>関数またはフィルター ドライバーの電源投入シーケンス


次の図は、図の下部にあるデバイスが挿入された状態から開始、完全に operational 状態へのデバイスの追加時に、フレームワーク、KMDF 関数またはフィルター ドライバーのイベントのコールバック関数を呼び出す順序を示します。

![関数またはフィルター ドライバーのデバイスの列挙と電源投入シーケンス](images/fdo-fido-powerup.png)

広範な水平の線は、デバイスの起動に関連するステップをマークします。 図の左側にある列について、手順を説明し、右側の列には、そのイベントのコールバックが一覧表示されます。

図の下部には、デバイスは、システムに存在しません。 フレームワークを呼び出してドライバーの開始、ユーザーがデバイスを挿入するとき[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック、ドライバーは、デバイスを表すデバイス オブジェクトを作成できるようにします。 フレームワークでは、ドライバーのコールバック ルーチンを呼び出すことによって、デバイスは稼働までのシーケンスを経由の進行が続行されます。 フレームワークは、ために下から順に順番の図に示すようにイベント コールバックを呼び出すことに注意してください[ *EvtDeviceFilterRemoveResourceRequirements* ](https://msdn.microsoft.com/library/windows/hardware/ff540872)前に呼び出されます[ *。EvtDeviceFilterAddResourceRequirements* ](https://msdn.microsoft.com/library/windows/hardware/ff540870)という具合です。 デバイスがリソースを再調整を停止したか、物理的に存在していた場合は、低電力状態にすべての手順は、図に示すように、必要です。

 

 





