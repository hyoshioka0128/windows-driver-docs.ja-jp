---
title: KMDF 拡張機能とドライバー トリプル
description: このトピックでは、カーネル モード ドライバー フレームワーク (KMDF) に対するクラス ベースの拡張機能について説明します。
ms.assetid: 49207485-AFDF-4E84-B39C-A14FC7E2CF60
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a08581620dad4b82d279c93e26f1ad682e227d7
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "63371298"
---
# <a name="kmdf-extensions-and-driver-triples"></a>KMDF 拡張機能とドライバー トリプル


このトピックでは、カーネル モード ドライバー フレームワーク (KMDF) に対するクラス ベースの拡張機能について説明します。 このトピックを読む前にまず、「[ミニドライバーとドライバーのペア](minidrivers-and-driver-pairs.md)」と「[汎用ドライバー ペア モデルとしての KMDF](kmdf-as-a-generic-pair-model.md)」で説明する概念について理解しておく必要があります。

一部のデバイス クラスについては、KMDF ドライバーで実行する必要のある処理量の低減を図るために、Microsoft が KMDF 拡張機能を提供しています。 クラス ベースの KMDF 拡張機能を使うドライバーは、3 つの部分で構成されます。この部分を*ドライバー トリプル*と呼んでいます。

-   大部分のドライバーに共通するタスクを処理するフレームワーク
-   特定クラスのデバイスに固有のタスクを処理クラス ベースのフレームワーク拡張機能
-   特定のデバイスに固有のタスクを処理する KMDF ドライバー

ドライバー トリプル (KMDF ドライバー、デバイス クラス KMDF 拡張機能、フレームワーク) の 3 つのドライバーを組み合わせることにより、単一の WDM ドライバーが形成されます。

デバイス クラスの KMDF 拡張機能の例として SpbCx.sys があります。これは、SPB (Simple Peripheral Bus) デバイス クラスの KMDF 拡張機能です。 SPB クラスには、I2C や SPI などの同期シリアル バスが含まれます。 I2C バス コントローラーのドライバー トリプルは次のようになります。

-   フレームワークは、大部分のドライバーに共通する汎用タスクを処理します。
-   SpbCx.sys は、SPB バス クラスに固有のタスクを処理します。 これらはいずれも、すべての SPB バスに共通するタスクです。
-   KMDF ドライバーは、I2C バスに固有のタスクを処理します。 このドライバーを MyI2CBusDriver.sys と呼ぶことにします。

![KMDF ドライバー トリプル拡張機能](images/kmdfdrivertriple.png)

ドライバー トリプル (MyI2CBusDriver.sys、SpbCx.sys、Wdf01000.sys) の 3 つのドライバーを組み合わせることにより、単一の WDM ドライバーが形成されます。WDM ドライバーは、I2C バス コントローラーのファンクション ドライバーとして機能します。 Wdf01000.sys (フレームワーク) には、このドライバーのディスパッチ テーブルが存在するため、だれかがドライバー トリプルに IRP を送ると、IRP は wdf01000.sys に送信されます。 wdf01000.sys が単独で IRP を処理できる場合は、SpbCx.sys と MyI2CBusDriver.sys は関与しません。 wdf01000.sys が単独で IRP を処理できない場合は、SbpCx.sys のイベント ハンドラーを呼び出すことにより、支援を利用します。

以下に、MyI2CBusDriver.sys で実装できるイベント ハンドラーの例をいくつか示します。

-   EvtSpbControllerLock
-   EvtSpbIoRead
-   EvtSpbIoSequence

以下に、SpbCx.sys で実装できるイベント ハンドラーの例をいくつか示します。

-   EvtIoRead

 

 





