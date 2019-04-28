---
title: パラレル デバイスの開始と使用
description: パラレル デバイスの開始と使用
ms.assetid: ca58b1c3-9ecf-4ebe-8f08-a2f78ae17921
keywords:
- 並列デバイス WDK を開く
- デバイス、WDK の並列の共有
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ec96fea6c345c57e33f11bf3f34c207999160bb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374548"
---
# <a name="opening-and-using-a-parallel-device"></a>パラレル デバイスの開始と使用





パラレル ポートのシステム提供のバス ドライバーでは、パラレル ポートに接続されている並列デバイスへの排他アクセスを適用します。 並列デバイスが開いている場合は、パラレル ポート バス ドライバーがその後で失敗した[ **IRP\_MJ\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff544131)まで、デバイスが閉じられているデバイスを要求します。 デバイスまたは呼び出しに他の I/O 要求を送信する前に、クライアントは並列のデバイスを開く必要があります、[デバイス コールバック ルーチンを並列](https://msdn.microsoft.com/library/windows/hardware/ff544275)します。 クライアントは、クライアントがデバイスにそのファイルを閉じた後に、並列のデバイスと通信する必要があります試行しません。 クライアントは、デバイスにアクセスするには、他のクライアントを実行できるように、デバイスを閉じる必要があります。

通常、クライアントは、次は。

-   並列のデバイスを開きます

-   並列デバイス − を参照する接続[並列デバイスへの接続](connecting-to-a-parallel-device.md)

-   並列デバイス − 参照に関する情報を取得[並列デバイスに関する情報を取得します。](obtaining-information-about-a-parallel-device.md)

-   デバイス: この参照がロック[ロックおよび並列のデバイスで使用するためのパラレル ポートのロックを解除](locking-and-unlocking-a-parallel-port-for-use-by-a-parallel-device.md)

-   一連のデバイスの操作には

-   並列デバイス − 参照から切断[並列デバイスへの接続](connecting-to-a-parallel-device.md)

-   デバイス: この参照のロックを解除[ロックおよび並列のデバイスで使用するためのパラレル ポートのロックを解除](locking-and-unlocking-a-parallel-port-for-use-by-a-parallel-device.md)

-   デバイスを閉じる

プラグ アンド プレイ環境でデバイスを削除したり、上、開いているファイルがないときに追加されるに注意してください。 一般に、並列のデバイスが追加されるたびにプラグ アンド プレイが別の場所とリソースを割り当てます。

 

 




