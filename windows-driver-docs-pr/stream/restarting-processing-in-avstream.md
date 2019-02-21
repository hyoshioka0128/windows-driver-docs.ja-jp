---
title: AVStream で処理を再起動します。
description: AVStream で処理を再起動します。
ms.assetid: f60d4dbd-61e6-4ae2-aa43-9edc8f36c3ff
keywords:
- AVStream 処理を再起動します。
- WDK の再起動 AVStream プロセス
- WDK AVStream の処理を再開します。
- WDK AVStream の保留中の状態
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c37c47133e927627987a8a8f8b9840e41dd19792
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532324"
---
# <a name="restarting-processing-in-avstream"></a>AVStream で処理を再起動します。





AVStream は、次の条件のいずれかに該当する場合の処理を停止します。

-   暗証番号 (pin) を中心とした環境では、データは現在、pin で使用できるありません。

-   フィルターを中心とした環境では、少なくとも 1 つをピン留めする、**フラグ**のメンバー、 [ **KSPIN\_記述子\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff563534)構造はありませんKSPIN 設定\_フラグ\_フレーム\_いない\_REQUIRED\_の\_を処理すると、処理を待機しているデータが含まれない。 既定では、このフラグが設定されていません。

-   ミニドライバーの処理のディスパッチ コールバック ルーチンがステータスを返します\_フレームの可用性に関係なく、保留します。 処理のディスパッチを指定できるでいずれかに注意してください[ *AVStrMiniFilterProcess* ](https://msdn.microsoft.com/library/windows/hardware/ff556315)または[ *AVStrMiniPinProcess*](https://msdn.microsoft.com/library/windows/hardware/ff556351)かどうかに応じて、。ミニドライバー実装[暗証番号 (pin) を中心とした処理](pin-centric-processing.md)または[フィルターを中心とした処理](filter-centric-processing.md)します。

AVStream は、新しいデータは、空のキューに到着したときの処理を開始します。 そのため、ミニドライバーのディスパッチを処理している場合、状態を返します\_と関連付けられているキューがいっぱい、保留中のミニドライバーは呼び出されません再開処理にログオンします。 ミニドライバーの状態を設定する場合、\_、保留中で、ミニドライバーを呼び出す必要があります[ **KsPinAttemptProcessing** ](https://msdn.microsoft.com/library/windows/hardware/ff563494)または[ **KsFilterAttemptProcessing**](https://msdn.microsoft.com/library/windows/hardware/ff562527)処理を再開します。

状態が返されません\_ミニドライバーが実際にデータを処理する場合は、処理ディスパッチから成功します。 これにより、無限ループ AVStream と処理のディスパッチの間に結果を直ちに呼び出すようにミニドライバーをもう一度、AVStream します。

 

 




