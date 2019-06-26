---
Description: このセクションでは、高度な概念とドライバーの開発をホストするためのタスクを紹介します。
title: USB ホスト コント ローラーの拡張機能 (UCX) のアーキテクチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51ad026cd95f0d3ee838145e9020f4d5c2c99e98
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378342"
---
# <a name="architecture-usb-host-controller-extension-ucx"></a>アーキテクチャ:USB ホスト コントローラー拡張 (UCX)


このセクションでは、高度な概念とドライバーの開発をホストするためのタスクを紹介します。 Microsoft 提供の USB ホスト コント ローラー拡張機能ドライバー (Ucx01000.sys) を使用したコント ローラー ドライバーと通信する新しいホストを作成する場合に、セクションが適用されます。

次の図に示すように変更したバージョンに示します[Windows での USB ホスト側ドライバー](usb-3-0-driver-stack-architecture.md)します。 このバージョンでは、ホスト コント ローラーのドライバーの開発に関連するではない USB クライアント ドライバーのレイヤーの詳細を非表示にします。

![ucx アーキテクチャ](images/ucx.png)

上の図

-   **USB ハブのドライバー (Usbhub3.sys)** KMDF ドライバーします。 USB ハブおよびそのポートを管理するため、ハブのドライバーは、列挙型と物理デバイス オブジェクト (Pdo) の USB デバイスやその他のハブを作成、ダウン ストリームのポートに接続できます。
-   **USB ホスト コント ローラーの拡張機能 (Ucx01000.sys)** スタックでは、ハブのドライバーの上に抽象化レイヤーは、ジェネリック、基になるホスト コント ローラー ドライバーへの要求をキュー メカニズムを提供します。
-   **USB ホスト コント ローラー ドライバー**ハードウェアを管理します。 Usbxhci.sys は、具体的には、そのターゲット xHCI 仕様準拠 USB コント ローラーのハードウェア、Microsoft によって提供されるこのような 1 つのドライバーです。 独立系ハードウェア開発者 Usbxhci.sys 受信トレイを使用するのではなく、独自のホスト コント ローラーのドライバーを記述する必要がある場合があります。 たとえば、したがって Usbxhci.sys は使用できませんが、仕様に完全に準拠していないを XHCI ハードウェアや XHCI 以外のハードウェアには、TCP 接続経由での USB など。

コント ローラー ドライバー UCX とホスト間では、双方向通信を使用して行わ[USB ホスト コント ローラーの拡張機能 (UCX) プログラミング インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188009(v=vs.85))します。 ドライバーはコンパイル時に、各ドライバーは、Microsoft 提供のスタブ ライブラリ (Ucx01000.lib) 内のエントリ ポイントに静的にリンクします。

ホスト コント ローラーのドライバーの読み込み、デバイス スタックを次に示します。

![ucx デバイス スタック](images/ucx-device-stack.png)

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/)  
[USB ドライバー開発ガイド](usb-driver-development-guide.md)  



