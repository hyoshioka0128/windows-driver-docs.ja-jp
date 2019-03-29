---
Description: The section describes architecture of USB Device Emulation(UDE) that emulates the behavior of a USB host controller and a connected device.
title: USB デバイスのエミュレーション (UDE) のアーキテクチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 737b1f29ef5d9006c5f3b70ae090e15d33d88a8a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579683"
---
# <a name="architecture-usb-device-emulation-ude"></a>アーキテクチャ:USB デバイス エミュレーション (UDE)


USB デバイス Emulation(UDE) USB ホスト コント ローラーの動作をエミュレートして、接続されたデバイスのアーキテクチャについて説明します。 UDE を使用して、使用して、USB 以外のハードウェアが上位の層と通信できる、 [Windows での USB ホスト側ドライバー](usb-device-side-drivers-in-windows.md)します。

## <a name="ude-drivers"></a>UDE ドライバー


![usb デバイスのエミュレーション (ude)](images/ude-arch.png)

上の図

-   **USB ハブのドライバー (Usbhub3.sys)** KMDF ドライバーします。 USB ハブおよびそのポートを管理するため、ハブのドライバーは、列挙型と物理デバイス オブジェクト (Pdo) の USB デバイスやその他のハブを作成、ダウン ストリームのポートに接続できます。
-   **USB ホスト コント ローラーの拡張機能 (Ucx01000.sys)** スタックでは、ハブのドライバーの上に抽象化レイヤーは、ジェネリック、基になるホスト コント ローラー ドライバーへの要求をキュー メカニズムを提供します。
-   **クラスの拡張機能を UDE** (UdeCx) は、UDE クライアント ドライバーはクライアントで実装されたコールバック関数への呼び出し。 クラスの拡張機能は、UDE オブジェクトを作成し、それらを管理するクライアント ドライバーのルーチンを提供します。
-   **クライアント ドライバーの UDE** WDF と UDE Api と対話する、ハードウェアを管理します。 上端は、USB コンストラクトを使用してクラス拡張は、WDF と UDE の両方と通信します。 下端は、ハードウェアのインターフェイスを使用して、ハードウェアと通信します。
-   カスタム ハードウェアは:たとえば、USB デバイスとして動作する PCI ハードウェアをエミュレートできます。

## <a name="ude-device-nodes"></a>UDE デバイス ノード


UDE クライアント ドライバーの読み込み、デバイス スタックを次に示します。

![usb デバイスのエミュレーション (ude) デバイス ノード](images/ude-dev-nodes.png)

 

 




