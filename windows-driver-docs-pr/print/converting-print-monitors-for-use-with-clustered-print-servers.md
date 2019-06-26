---
title: クラスター化された印刷サーバーで使用するために印刷モニターを変換する
description: クラスター化された印刷サーバーで使用するために印刷モニターを変換する
ms.assetid: 6b374d61-bb2b-42a4-9609-3cde9b82bb2b
keywords:
- 印刷モニター WDK、クラスター化されたプリント サーバー
- クラスター化されたプリント サーバー WDK
- プリント サーバーの WDK をクラスタ リング
- クラスター化されたプリント サーバーの印刷のモニターに変換します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 125a535936d85eef548c0bf48725166d72adab36
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372478"
---
# <a name="converting-print-monitors-for-use-with-clustered-print-servers"></a>クラスター化された印刷サーバーで使用するために印刷モニターを変換する





プリント サーバーのクラスタ リングは、Windows 2000 の新しい機能です。 複数のスプーラー インスタンス (ノードの spooler」および「クラスター スプーラー) から呼び出せるように、Windows 2000 (またはそれ以降) のクラスターで実行するためのものでは、すべてプリンター ポート モニターを変更する必要があります。 次の手順を実行する必要があります。

-   モニターの[ **InitializePrintMonitor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-initializeprintmonitor)関数を置換する必要がある、 [ **InitializePrintMonitor2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-initializeprintmonitor2)関数。 後者の関数は、モニターのインスタンス ハンドルを返します。

-   グローバルに格納された変数は、ローカルに割り当てられたメモリに移動する必要があり、このメモリは、によって返されたモニターのハンドルを関連付ける必要がある[ **InitializePrintMonitor2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-initializeprintmonitor2)します。

-   API は、スプーラーのレジストリ関数への呼び出しで置き換える必要がある Win32 のレジストリへの呼び出し、これのアドレスでモニターに渡される、 [ **MONITORREG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/ns-winsplp-_monitorreg)構造体。 (を参照してください[ポートの構成情報を格納する](storing-port-configuration-information.md))。

-   ポート モニター UI の DLL とポートの監視サーバー DLL には、ポート モニターを分割する必要があります。 UI の DLL は、スプーラーを呼び出すことによってサーバー DLL と通信する必要があります[ **XcvData** ](https://docs.microsoft.com/previous-versions/ff564255(v=vs.85))関数。

-   A [**シャット ダウン**](https://docs.microsoft.com/previous-versions/ff562646(v=vs.85))関数を追加する必要があります。

変換されません印刷のモニターは、非クラスター化環境でのみ使用できます。 これらは、クラスター化されたサーバーで使用できません。

したらプリンター ポートを Windows 2000 を実行するマシンのクラスター化されたノードで実行されているかを監視または以降では、(または、ネットワーク経由でローカルに)、接続を確立、ポート モニターが返されます一定の時間内で、スプーラーによって行われた呼び出しからです。 削除を行います (スプーラー リソースのタイムアウトの既定値は 180 秒です。 参照してください[ポートのタイムアウト値を設定](setting-port-time-out-values.md)詳細についてはします)。

1 つのクラスター ノードから別のフェールオーバーが発生したときに、スプーラーは現在のすべての印刷ジョブを完了または失敗を待つ必要があります。 保留中の印刷ジョブが、スプーラー リソースのタイムアウトより長くポート モニター保持されている場合、スプーラーがオンラインに戻ります不完全な状態でが一時的に不足しているプリンター。 これらの不足しているプリンターへの接続を持つユーザーに影響を与える可能性があります。

 

 




