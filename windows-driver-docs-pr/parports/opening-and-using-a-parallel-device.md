---
title: パラレル デバイスの開始と使用
description: パラレル デバイスの開始と使用
ms.assetid: ca58b1c3-9ecf-4ebe-8f08-a2f78ae17921
keywords:
- 並列デバイス WDK、開く
- パラレルデバイス WDK、共有
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47f64f3963361036781a4f74c42d4ff54762951a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844492"
---
# <a name="opening-and-using-a-parallel-device"></a>パラレル デバイスの開始と使用





パラレルポートに対してシステム提供のバスドライバーを使用すると、パラレルポートに接続されているパラレルデバイスへの排他アクセスが強制されます。 パラレルデバイスが開いている場合、パラレルポートバスドライバーは、デバイスが閉じられるまでデバイスの要求を作成\_ために、後続の[**IRP\_MJ**](https://docs.microsoft.com/previous-versions/ff544131(v=vs.85))に失敗します。 クライアントは、デバイスに他の i/o 要求を送信する前に、または[並列デバイスコールバックルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)を呼び出すために、並列デバイスを開く必要があります。 クライアントがデバイス上のファイルを閉じた後に、デバイスとの通信を試行することはできません。 クライアントは、デバイスを閉じて、他のクライアントがデバイスにアクセスできるようにする必要があります。

クライアントは、通常、次のことを行います。

-   パラレルデバイスを開く

-   パラレルデバイスへの接続: 「[パラレルデバイスへの接続](connecting-to-a-parallel-device.md)」を参照してください。

-   パラレルデバイスに関する情報を取得します。「[パラレルデバイスに関する情報の取得」を](obtaining-information-about-a-parallel-device.md)参照してください。

-   デバイスをロックします。[パラレルデバイスで使用するためのパラレルポートのロックとロック解除](locking-and-unlocking-a-parallel-port-for-use-by-a-parallel-device.md)を参照してください。

-   デバイスで操作のシーケンスを実行します。

-   パラレルデバイスから切断する-「[パラレルデバイスへの接続」を](connecting-to-a-parallel-device.md)参照してください。

-   デバイスのロックを解除します。[パラレルデバイスで使用するためのパラレルポートのロックとロック解除](locking-and-unlocking-a-parallel-port-for-use-by-a-parallel-device.md)

-   デバイスを閉じます。

プラグアンドプレイ環境では、開いているファイルがないときは常にデバイスを削除または追加できます。 一般に、並列デバイスが追加されるたびに、プラグアンドプレイによって別の場所とリソースが割り当てられます。

 

 




