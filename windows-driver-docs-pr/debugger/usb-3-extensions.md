---
title: USB 3.0 の拡張機能
description: このセクションでは、USB 3.0 デバッガー拡張機能のコマンドについて説明します。
ms.assetid: 7CE2B9F8-50EF-41C0-B306-B7B7A6DA1636
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f847cd70475a111c3536201b17c8c26111f8a775
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531923"
---
# <a name="usb-30-extensions"></a>USB 3.0 の拡張機能


このセクションでは、USB 3.0 デバッガー拡張機能のコマンドについて説明します。 これらのコマンドは、USB 3.0 スタック内の 3 つのドライバーによって維持されるデータ構造から情報を表示します。 USB 3.0 ハブのドライバー、USB ホスト コント ローラーの拡張機能ドライバーと、USB 3.0 ホスト コント ローラー ドライバー。 これら 3 つのドライバーの詳細については、[USB ドライバー スタック アーキテクチャ](https://go.microsoft.com/fwlink/p?LinkId=251983)を参照してください。 USB 3.0 スタック内のドライバーで使用されるデータ構造の詳細については、次を参照してください。 [USB 3.0 データ構造](usb-3-0-data-structures.md)と第 2 部、 [Windows 8 の USB デバッグ イノベーション](https://go.microsoft.com/fwlink/p/?LinkID=249153)ビデオ。

USB 3.0 デバッガー拡張機能のコマンドは、Usb3kd.dll で実装されます。 Usb3kd コマンドを読み込むには、次のように入力します。 **.load usb3kd.dll**デバッガーでします。

## <a name="span-idusb-3-treespanspan-idusb3treespanusb-30-tree"></a><span id="usb-3-tree"></span><span id="USB_3_TREE"></span>USB 3.0 ツリー


USB 3.0 ツリーには、すべての USB 3.0 ホスト コント ローラーとすべてのハブと USB 3.0 ホスト コント ローラーに接続されているデバイスが含まれています。 次の図は、USB 3.0 ツリーの例を示します。

![usb 3.0 と usb 2.0 デバイス ルートとコント ローラーの両方を示す usb 3.0 ツリー](images/usb3tree01.png)

図に示すように、ツリーには、2 つの USB 3.0 ホスト コント ローラーがあります。 図に示したすべてのデバイスが USB 3.0 デバイスであることを確認します。 各デバイスが USB 3.0 ホスト コント ローラーで発生するブランチ上にあるため、USB 3.0 ツリーの一部であるすべてのデバイス (ハブを含む) を表示します。

図は、各ホスト コント ローラーに 1 つずつ、2 つのツリーとして考えることができます。 ただし、用語を使用しました*USB 3.0 ツリー*、すべての USB 3.0 ホスト コント ローラーと共に、接続されているハブとデバイスのセットについて言及しています。

## <a name="span-idgetting-started-with-usb-30-debuggingspanspan-idgettingstartedwithusb30debuggingspangetting-started-with-usb-30-debugging"></a><span id="getting-started-with-usb-3.0-debugging"></span><span id="GETTING_STARTED_WITH_USB_3.0_DEBUGGING"></span>USB 3.0 の概要のデバッグ


USB 3.0 問題のデバッグを開始するには、入力、 [ **! usb\_ツリー** ](-usb3kd-usb-tree.md)コマンド。 **! Usb\_ツリー**コマンドは、コマンドとホスト コント ローラー、ハブ、ポート、デバイス、エンドポイント、および USB 3.0 ツリーの他の要素を調査するために使用できるアドレスの一覧を表示します。

## <a name="span-idhub-commandsspanspan-idhubcommandsspanspan-idhubcommandsspanhub-commands"></a><span id="hub-commands"></span><span id="hub_commands"></span><span id="HUB_COMMANDS"></span>ハブ コマンド


次の拡張機能コマンドでは、USB 3.0 ハブ、デバイス、およびポートに関する情報を表示します。 表示される情報は、USB 3.0 ハブのドライバーによって管理されるデータ構造に基づきます。

-   [**!usb3kd.usb\_tree**](-usb3kd-usb-tree.md)
-   [**!usb3kd.hub\_info**](-usb3kd-hub-info.md)
-   [**!usb3kd.hub\_info\_from\_fdo**](-usb3kd-hub-info-from-fdo.md)
-   [**! usb3kd.device\_情報**](-usb3kd-device-info.md)
-   [**! usb3kd.device\_情報\_から\_pdo**](-usb3kd-device-info-from-pdo.md)
-   [**!usb3kd.port\_info**](-usb3kd-port-info.md)

## <a name="span-iducxcommandsspanspan-iducxcommandsspanspan-iducxcommandsspanucx-commands"></a><span id="UCX_commands"></span><span id="ucx_commands"></span><span id="UCX_COMMANDS"></span>UCX コマンド


次の拡張機能コマンドでは、USB 3.0 ホスト コント ローラー、デバイス、およびポートに関する情報を表示します。 表示される情報は、USB ホスト コント ローラーの拡張機能ドライバーによって管理されるデータ構造に基づきます。

-   [**! usb3kd.ucx\_コント ローラー\_一覧**](-usb3kd-ucx-controller-list.md)
-   [**!usb3kd.ucx\_controller**](-usb3kd-ucx-controller.md)
-   [**! usb3kd.ucx\_デバイス**](-usb3kd-ucx-device.md)
-   [**!usb3kd.ucx\_endpoint**](-usb3kd-ucx-endpoint.md)

## <a name="span-idhostcontrollercommandsspanspan-idhostcontrollercommandsspanspan-idhostcontrollercommandsspanhost-controller-commands"></a><span id="Host_controller_commands"></span><span id="host_controller_commands"></span><span id="HOST_CONTROLLER_COMMANDS"></span>ホスト コント ローラーのコマンド


次の拡張機能コマンドでは、USB 3.0 ホスト コント ローラーのドライバーによって維持されるデータ構造から情報を表示します。

-   [**! usb3kd.xhci\_dumpall**](-usb3kd-xhci-dumpall.md)
-   [**! usb3kd.xhci\_機能**](-usb3kd-xhci-capability.md)
-   [**! usb3kd.xhci\_commandring**](-usb3kd-xhci-commandring.md)
-   [**! usb3kd.xhci\_deviceslots**](-usb3kd-xhci-deviceslots.md)
-   [**!usb3kd.xhci\_eventring**](-usb3kd-xhci-eventring.md)
-   [**! usb3kd.xhci\_を登録します**](-usb3kd-xhci-registers.md)
-   [**! usb3kd.xhci\_resourceusage**](-usb3kd-xhci-resourceusage.md)
-   [**! usb3kd.xhci\_trb**](-usb3kd-xhci-trb.md)
-   [**! usb3kd.xhci\_を転送します。**](-usb3kd-xhci-transferring.md)
-   [**!usb3kd.xhci\_findowner**](-usb3kd-xhci-findowner.md)

## <a name="span-idmiscellaneouscommandsspanspan-idmiscellaneouscommandsspanspan-idmiscellaneouscommandsspanmiscellaneous-commands"></a><span id="Miscellaneous_commands"></span><span id="miscellaneous_commands"></span><span id="MISCELLANEOUS_COMMANDS"></span>その他のコマンド


-   [**!usb3kd.usbdstatus**](-usb3kd-usbdstatus.md)
-   [**!usb3kd.urb**](-usb3kd-urb.md)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[RCDRKD 拡張機能](rcdrkd-extensions.md)

 

 






