---
title: デバイスのインストール時の自動構成
description: デバイスのインストール時の自動構成
ms.assetid: 04b53767-4b5e-450d-96ab-b029cdf62b36
keywords:
- デバイスのインストール中に、自動構成の WDK プリンター
- デバイスのインストール中に、プリンターの自動構成の WDK プリンター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0f8c037304e99e45e7e7814b3acc196264d3778
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370487"
---
# <a name="autoconfiguration-during-device-installation"></a>デバイスのインストール時の自動構成


次の図は、デバイスがインストールされている場合、自動構成で、データ フローを示します。

![デバイスがインストールされている場合は、自動構成内のデータ フローを示す図](images/autocfginstall.png)

1.  プリンターがインストールされている、スプーラーを呼び出すことによって、ドライバーが初期化します`DrvPrinterEvent`プリンターを渡すと\_イベント\_呼び出しで初期化します。

2.  ドライバーを使用して[双方向の通信インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_print/index)などのインストール可能なオプションの値を含む、関心のあるデータを取得する\\Printer.Configuration.DuplexUnit:Installed と\\Printer.Configuration.HardDisk:Installed します。

3.  双方向の通信インターフェイスは、これらの属性の値が、ポート モニターを照会します。 ポート モニターは、いくつかのキャッシュで要求されたデータのがあります。 例示を目的として、次の手順で、仮定の値は、 \\Printer.Configuration.HardDisk:Installed がの値が、ポート モニターのキャッシュ、 \\Printer.Configuration.DuplexUnit:Installed でないです。

4.  ポート モニターには、キャッシュがあり、これで、要求された値の 1 つ以上が保存された場合、ポート モニターは、双方向の通信インターフェイスにこれらの値を返します。 そのキャッシュにない任意の値では、ポート モニターにエラーが返されます。\_いいえ\_データ。 Bidi クエリは、ポート モニターには、キャッシュが実装されていますが、キャッシュが空である場合が失敗することに注意してください。 この問題を回避するには、そのキャッシュの内容が表示されたら、ポート モニターで双方向の通信インターフェイスを通知する必要があります。

5.  双方向の通信インターフェイスは、ドライバー、ポート モニターから受信した情報を渡します。 双方向の通信インターフェイスから、ポート モニターへの呼び出しの結果エラー何らかの理由で、ドライバーはこれらの属性の既定値を設定する必要があります。 ポート モニターは、要求された属性に関する情報を受け取る、すぐに双方向の通信インターフェイスには、この情報を含む通知を送信する必要があります。

    ドライバーの値で、レジストリを更新する\\Printer.Configuration.HardDisk:Installed (ポート モニターのキャッシュから取得した) と、既定値\\Printer.Configuration.DuplexUnit:Installed します。

6.  ポート モニタ両方の値は、キャッシュに保存された値を含むデバイスを照会する (\\Printer.Configuration.HardDisk:Installed)。

7.  デバイスは、クエリ対象の属性の値をポート モニターに送信します。 値を持つが、キャッシュ内に存在しないか、キャッシュ内の 1 つからの値が異なる任意の属性は、ポート モニターは、キャッシュに新しい値を配置します。

8.  ポート モニターは、スプーラーに以前ではなく、キャッシュまたは変更されたすべての値を含む通知を送信します。 この例で、ポート モニターは、スプーラーの新しい値に関するに通知を送信\\Printer.Configuration.DuplexUnit:Installed します。 キャッシュされた値が、デバイスから受信した新しい値と同じ場合は、ポート モニターは、スプーラーに通知をいないに送信するに注意してください。

9.  スプーラーは通知に応答のポート モニターから呼び出すことによって`DrvPrinterEvent`、プリンターを渡すこと\_イベント\_構成\_呼び出しで変更されたすべての値に関する情報だけでなく更新します。 このアクションには 2 つの目的が機能します: 値を持つが、最初に、キャッシュに格納された、または値が変更されたすべての属性の値のドライバーに通知する (\\Printer.Configuration.DuplexUnit:Installed、この例では) はレジストリを更新します。 各プリンターについて、スプーラーはへの呼び出しをシリアル化`DrvPrinterEvent`ドライバーはスレッド セーフである必要はありません。

    レジストリにデバイス情報が格納されている、ため、ドライバーは物理デバイスと直接通信する必要はありません、UI またはデバイスの機能情報を更新する呼び出しを満たすことができます。 ドライバーは変更通知デバイスを照会し、デバイスの構成状態を更新するドライバーがトリガーされるため、レジストリに格納されている情報が正しいことを確信できます。

10. ドライバーは、最新の構成に合わせて UI を更新します。

    通知メッセージは変更された値を保持するため、デバイスのインストール中に変更が発生するとが、ドライバーに判断できます。 ただし、通知が大きすぎて通知メカニズムを経由して送信する場合、通知はそれぞれのデバイスの特性が変更されたことを示しますが、その新しい値の詳細なし、1 つ以上の ReducedSchema インスタンスがあります。

 

 




