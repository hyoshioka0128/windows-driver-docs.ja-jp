---
Description: このセクションでは、高度な概念とドライバーの開発をホストするためのタスクを紹介します。
title: USB ホスト コント ローラーの拡張機能 (UCX) のアーキテクチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d53d333bc749b6a99394d55ec9adac3eed17d617
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383028"
---
# <a name="architecture-usb-host-controller-extension-ucx"></a>アーキテクチャ:USB ホスト コントローラー拡張 (UCX)


このセクションでは、高度な概念とドライバーの開発をホストするためのタスクを紹介します。 Microsoft 提供の USB ホスト コント ローラー拡張機能ドライバー (Ucx01000.sys) を使用したコント ローラー ドライバーと通信する新しいホストを作成する場合に、セクションが適用されます。

次の図に示すように変更したバージョンに示します[Windows での USB ホスト側ドライバー](usb-3-0-driver-stack-architecture.md)します。 このバージョンでは、ホスト コント ローラーのドライバーの開発に関連するではない USB クライアント ドライバーのレイヤーの詳細を非表示にします。

![ucx アーキテクチャ](images/ucx.png)

上の図

-   **USB ハブのドライバー (Usbhub3.sys)** KMDF ドライバーします。 USB ハブおよびそのポートを管理するため、ハブのドライバーは、列挙型と物理デバイス オブジェクト (Pdo) の USB デバイスやその他のハブを作成、ダウン ストリームのポートに接続できます。
-   **USB ホスト コント ローラーの拡張機能 (Ucx01000.sys)** スタックでは、ハブのドライバーの上に抽象化レイヤーは、ジェネリック、基になるホスト コント ローラー ドライバーへの要求をキュー メカニズムを提供します。
-   **USB ホスト コント ローラー ドライバー**ハードウェアを管理します。 Usbxhci.sys は、具体的には、そのターゲット xHCI 仕様準拠 USB コント ローラーのハードウェア、Microsoft によって提供されるこのような 1 つのドライバーです。 独立系ハードウェア開発者 Usbxhci.sys 受信トレイを使用するのではなく、独自のホスト コント ローラーのドライバーを記述する必要がある場合があります。 たとえば、したがって Usbxhci.sys は使用できませんが、仕様に完全に準拠していないを XHCI ハードウェアや XHCI 以外のハードウェアには、TCP 接続経由での USB など。

コント ローラー ドライバー UCX とホスト間では、双方向通信を使用して行わ[USB ホスト コント ローラーの拡張機能 (UCX) プログラミング インターフェイス](https://msdn.microsoft.com/library/windows/hardware/mt188009)します。 ドライバーはコンパイル時に、各ドライバーは、Microsoft 提供のスタブ ライブラリ (Ucx01000.lib) 内のエントリ ポイントに静的にリンクします。

ホスト コント ローラーのドライバーの読み込み、デバイス スタックを次に示します。

![ucx デバイス スタック](images/ucx-device-stack.png)

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB) ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff538930)  
[USB ドライバー開発ガイド](usb-driver-development-guide.md)  



