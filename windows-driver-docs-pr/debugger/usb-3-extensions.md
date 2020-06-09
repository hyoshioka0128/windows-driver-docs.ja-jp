---
title: USB 3.0 拡張機能
description: ここでは、USB 3.0 デバッガー拡張機能のコマンドについて説明します。
ms.assetid: 7CE2B9F8-50EF-41C0-B306-B7B7A6DA1636
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9765e2d4d45df8ff4d2b362d9b06943cba41481
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84533835"
---
# <a name="usb-30-extensions"></a>USB 3.0 拡張機能

ここでは、USB 3.0 デバッガー拡張機能のコマンドについて説明します。 これらのコマンドは、usb 3.0 スタック内の3つのドライバーによって管理されているデータ構造の情報を表示します。 usb 3.0 hub ドライバー、USB ホストコントローラー拡張機能ドライバー、および USB 3.0 ホストコントローラードライバー。 これら3つのドライバーの詳細については、「 [Windows の USB ホスト側ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/usb-3-0-driver-stack-architecture)」を参照してください。 USB 3.0 スタックのドライバーで使用されるデータ構造の詳細については、「 [usb 3.0 データ構造](usb-3-0-data-structures.md)」と、 [Windows 8 ビデオの usb デバッグイノベーション](https://channel9.msdn.com/Events/BUILD/BUILD2011/HW-258P)のパート2を参照してください。

USB 3.0 デバッガー拡張コマンドは、Usb3kd に実装されています。 Usb3kd コマンドを読み込むには、デバッガーに「 **load Usb3kd** 」と入力します。

## <a name="span-idusb-3-treespan-usb-30-tree"></a><span id="usb-3-tree"></span>USB 3.0 ツリー

Usb 3.0 ツリーには、すべての USB 3.0 ホストコントローラーと、USB 3.0 ホストコントローラーに接続されているすべてのハブとデバイスが含まれます。 次の図は、USB 3.0 ツリーの例を示しています。

![usb 3.0 と usb 2.0 デバイスのルートとコントローラーの組み合わせを示す usb 3.0 ツリー](images/usb3tree01.png)

図に示されているツリーには、2つの USB 3.0 ホストコントローラーがあります。 図に示されているすべてのデバイスが USB 3.0 デバイスではないことに注意してください。 ただし、表示されているデバイス (ハブを含む) はすべて USB 3.0 ツリーに含まれています。これは、各デバイスが USB 3.0 ホストコントローラーから発信されたブランチ上にあるためです。

この図は、ホストコントローラーごとに1つずつ、2つのツリーであると考えることができます。 ただし、 *usb 3.0 ツリー*という用語を使用する場合は、すべての usb 3.0 ホストコントローラーと、接続されているハブおよびデバイスのセットを参照します。

## <a name="getting-started-with-usb-30-debugging"></a>USB 3.0 デバッグの概要

USB 3.0 の問題のデバッグを開始するには、 [**! usb \_ ツリー**](-usb3kd-usb-tree.md)コマンドを入力します。 **! Usb \_ tree**コマンドは、ホストコントローラー、ハブ、ポート、デバイス、エンドポイント、および usb 3.0 ツリーのその他の要素を調査するために使用できるコマンドとアドレスの一覧を表示します。

## <a name="hub-commands"></a>ハブコマンド

次の拡張コマンドでは、USB 3.0 ハブ、デバイス、およびポートに関する情報が表示されます。 表示される情報は、USB 3.0 hub ドライバーによって管理されるデータ構造に基づいています。

-   [**! usb3kd \_ ツリー**](-usb3kd-usb-tree.md)
-   [**! usb3kd \_ 情報**](-usb3kd-hub-info.md)
-   [**! \_ \_ fdo からの usb3kd 情報 \_**](-usb3kd-hub-info-from-fdo.md)
-   [**! usb3kd. デバイス \_ 情報**](-usb3kd-device-info.md)
-   [**! usb3kd \_ \_ pdo からのデバイス \_ 情報**](-usb3kd-device-info-from-pdo.md)
-   [**! usb3kd \_ 情報**](-usb3kd-port-info.md)

## <a name="ucx-commands"></a>UCX コマンド


次の拡張コマンドでは、USB 3.0 ホストコントローラー、デバイス、およびポートに関する情報が表示されます。 表示される情報は、USB ホストコントローラー拡張機能ドライバーによって管理されるデータ構造に基づいています。

-   [**! usb3kd \_ コントローラーの \_ 一覧**](-usb3kd-ucx-controller-list.md)
-   [**! usb3kd \_ コントローラー**](-usb3kd-ucx-controller.md)
-   [**! usb3kd \_ デバイス**](-usb3kd-ucx-device.md)
-   [**! usb3kd \_ エンドポイント**](-usb3kd-ucx-endpoint.md)

## <a name="host-controller-commands"></a>ホストコントローラーのコマンド


次の拡張コマンドは、USB 3.0 ホストコントローラードライバーによって保持されているデータ構造の情報を表示します。

-   [**! usb3kd xhci \_ dumpall**](-usb3kd-xhci-dumpall.md)
-   [**! usb3kd. xhci \_ 機能**](-usb3kd-xhci-capability.md)
-   [**! usb3kd \_ . xhci**](-usb3kd-xhci-commandring.md)
-   [**! usb3kd. xhci の大 \_ 多数のデバイス**](-usb3kd-xhci-deviceslots.md)
-   [**! usb3kd. xhci \_ eventring**](-usb3kd-xhci-eventring.md)
-   [**! usb3kd. xhci \_ レジスタ**](-usb3kd-xhci-registers.md)
-   [**! usb3kd. xhci \_ resourceusage**](-usb3kd-xhci-resourceusage.md)
-   [**! usb3kd. xhci \_ trb**](-usb3kd-xhci-trb.md)
-   [**! usb3kd. xhci \_ 転送**](-usb3kd-xhci-transferring.md)
-   [**! usb3kd. xhci \_ findowner**](-usb3kd-xhci-findowner.md)

## <a name="miscellaneous-commands"></a>その他のコマンド

-   [**!usb3kd.usbdstatus**](-usb3kd-usbdstatus.md)
-   [**!usb3kd.urb**](-usb3kd-urb.md)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[RCDRKD 拡張機能](rcdrkd-extensions.md)
