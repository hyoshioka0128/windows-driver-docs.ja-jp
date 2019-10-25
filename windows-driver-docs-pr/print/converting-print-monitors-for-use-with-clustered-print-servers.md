---
title: クラスター化された印刷サーバーで使用するために印刷モニターを変換する
description: クラスター化された印刷サーバーで使用するために印刷モニターを変換する
ms.assetid: 6b374d61-bb2b-42a4-9609-3cde9b82bb2b
keywords:
- 印刷モニター WDK、クラスター化されたプリントサーバー
- クラスター化されたプリントサーバー WDK
- プリントサーバークラスタリング WDK
- クラスター化されたプリントサーバーの印刷モニターの変換
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef7f277ed59fad3b148b7c628d2cc0551b6ca51e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831817"
---
# <a name="converting-print-monitors-for-use-with-clustered-print-servers"></a>クラスター化された印刷サーバーで使用するために印刷モニターを変換する





プリントサーバーのクラスタリングは、Windows 2000 の新機能です。 Windows 2000 (またはそれ以降) のクラスターで実行するように設計されているすべてのプリンターポートモニターは、複数のスプーラインスタンス (ノードのスプーラおよびクラスタースプーラ) から呼び出すことができるように変更する必要があります。 次の手順を実行する必要があります。

-   モニターの[**Initializeprintmonitor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintmonitor)関数は、 [**InitializePrintMonitor2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintmonitor2)関数に置き換える必要があります。 後者の関数は、モニターインスタンスハンドルを返します。

-   グローバルに格納された変数は、ローカルに割り当てられたメモリに移動する必要があり、このメモリは[**InitializePrintMonitor2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-initializeprintmonitor2)によって返されるモニターハンドルに関連付けられている必要があります。

-   Win32 registry API の呼び出しは、スプーラのレジストリ関数の呼び出しに置き換える必要があります。これらのアドレスは、 [**Monitorreg**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/ns-winsplp-_monitorreg)構造でモニタに渡されます。 (「[ポート構成情報の格納](storing-port-configuration-information.md)」を参照してください)。

-   ポートモニターは、ポートモニターの UI DLL とポートモニターのサーバー DLL に分割する必要があります。 UI DLL は、スプーラの[**XcvData**](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))関数を呼び出すことによって、サーバー DLL と通信する必要があります。

-   [**シャットダウン**](https://docs.microsoft.com/previous-versions/ff562646(v=vs.85))関数を追加する必要があります。

変換されていない印刷モニターは、非クラスター環境でのみ使用できます。 クラスター化されたサーバーでは使用できません。

Windows 2000 以降を実行しているコンピューターのクラスターノードで実行されているプリンターポートモニターが (ネットワーク経由またはローカルで) 接続を確立すると、ポートモニターはスプーラによって行われた呼び出しから、適度な時間内にを返す必要があります。 (スプーラリソースのタイムアウトの既定値は180秒です。 詳細については、「ポートのタイムアウト[値の設定](setting-port-time-out-values.md)」を参照してください。)

あるクラスターノードから別のクラスターノードへのフェールオーバーが発生した場合、スプーラは現在のすべての印刷ジョブが完了するか失敗するまで待機する必要があります。 保留中の印刷ジョブがスプーラリソースのタイムアウトよりも長い速度でポートモニターに保持されている場合、スプーラーは一時的に状態が "未完了" になっている可能性があります。 これは、不足しているプリンターに接続しているユーザーに影響を与える可能性があります。

 

 




