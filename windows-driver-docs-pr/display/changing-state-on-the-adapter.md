---
title: アダプターの状態を変更します。
description: アダプターの状態を変更します。
ms.assetid: bf503a42-ac32-4d68-9ad9-afec69c5fe2a
keywords:
- ビデオ アダプターの状態変更 WDK ビデオのミニポート
- WDK のビデオのミニポートを状態します。
- アダプター状態 WDK のビデオのミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a21732236d92de7125427ce57d136032fb7616e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536873"
---
# <a name="changing-state-on-the-adapter"></a>アダプターの状態を変更します。


## <span id="ddk_changing_state_on_the_adapter_gg"></span><span id="DDK_CHANGING_STATE_ON_THE_ADAPTER_GG"></span>


ミニポート ドライバーまでアダプターの状態を永続的に変更する必要がありますいないその[ *HwVidInitialize* ](https://msdn.microsoft.com/library/windows/hardware/ff567345)ルーチンが呼び出されます。 前に呼び出されるミニポート ドライバー ルーチン*HwVidInitialize*など[ *HwVidFindAdapter*](https://msdn.microsoft.com/library/windows/hardware/ff567332)不必要にすべてのビデオ アダプターの状態を変更しないでください、してはいけませんすべてのビデオ アダプターの状態を永続的に変更します。

中に[ *HwVidFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff567332)システムのブート プロセスの初期段階で、画面に情報を書き込むことがあるために、HAL の実行がビデオ アダプターを制御します。 場合*HwVidFindAdapter*を識別しようとは、そのアダプター、アダプターの状態の影響がから返すにするための直前に、このルーチンは、元の状態を復元する必要があります*HwVidFindAdapter* HAL できます続行すると、起動がメッセージを表示します。

たとえば、 [ *HwVidFindAdapter* ](https://msdn.microsoft.com/library/windows/hardware/ff567332)には、アダプターの DAC 型の決定を延期する必要があります、 [ *HwVidInitialize* ](https://msdn.microsoft.com/library/windows/hardware/ff567345)関数この決定を行うため、ミニポート ドライバーは読み込まれますが、アダプターの状態を永続的に変更があるかどうかは影響しません。

 

 





