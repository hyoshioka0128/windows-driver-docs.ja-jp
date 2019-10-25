---
Description: Windows 10 のユニバーサルシリアルバス (USB) の新機能と機能強化について紹介します。
title: Windows 10-USB の新機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 350ca79e1e23c2ad0be68f04d9df57ca2eebd5ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843582"
---
# <a name="windows-10-whats-new-for-usb"></a>Windows 10: USB の新機能


このトピックでは、Windows 10 での Universal Serial Bus (USB) の新機能と機能強化について説明します。

-  **Ucsi ドライバーの拡張機能**Windows 10 バージョン1809以降では、UCSI (UcmUcsiCx) の新しいクラス拡張が追加されました。これにより、トランスポートに依存しない方法で UCSI 仕様が実装されます。 最小限のコードで、UcmUcsiCx へのクライアントであるドライバーが非 ACPI トランスポート経由で USB Type-C ハードウェアと通信できます。 このトピックでは、UCSI クラス拡張機能で提供されるサービスと、クライアント ドライバーの想定される動作について説明します。

-   **USB タイプ-C ポートコントローラーインターフェイス** 

    Windows 10 バージョン1703では、ユニバーサルシリアルバスタイプ C ポートコントローラーインターフェイス仕様をサポートするクラス拡張 (UcmTcpciCx .sys) が提供されます。 USB Type-C コネクタ ドライバーで内部の PD/Type-C 状態を保持しておく必要はありません。 
    USB Type-C コネクタと USB 電源供給 (PD) ステート マシンの複雑な管理はシステムによって処理されます。 必要なのは、クラス拡張機能を介してハードウェアのイベントをシステムに通信するクライアント ドライバーを作成することだけです。 

    [USB タイプ-C ポートコントローラーインターフェイスドライバークラス拡張のリファレンス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt805826(v=vs.85))

-   **USB デュアルロールのサポート。**

    Windows で USB デュアルロールコントローラーがサポートされるようになりました。 Windows には、ChipIdea コントローラーと Synopsys コントローラーのためのインボックス クライアント ドライバーが含まれています。 その他のコントローラーの場合、デュアルロール クラス拡張 (UrsCx) とそのクライアント ドライバーが互いに通信し、デュアルロール コントローラーのロール切り替え機能を処理できるようにする一連のプログラミング インターフェイスが Microsoft から提供されます。

    この機能の詳細については、以下を参照してください。

    [USB デュアル ロール ドライバー スタック アーキテクチャ](usb-dual-role-driver-stack-architecture.md)

    [USB デュアルロール コントローラー ドライバーのプログラミング参照](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt628026(v=vs.85))

-   **USB タイプ C コネクタドライバーを開発するための新しいプログラミングインターフェイスのセット。**

    このバージョンでは、USB 3.1 仕様で定義されている USB タイプ C のネイティブサポートが導入されています。 この機能により、デバイスは、USB ケーブルを介して実行される、元に戻せるコネクタ、対称ケーブル、高速充電、および代替モードを使用できます。 これらのプログラミングインターフェイスを使用すると、Microsoft 提供のクラス拡張モジュール: UcmCx と通信するコネクタ (このセクションのクライアントドライバーと呼ばれる) のドライバーを記述し、などのタイプ C コネクタに関連するシナリオを処理できます。サポートタイプ-C。電力の配信をサポートするポートです。

    [USB Type-C コネクタ用 Windows ドライバーの開発](developing-windows-drivers-for-usb-type-c-connectors.md)

    [USB コネクタ マネージャー クラス拡張 (UcmCx)](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188011(v=vs.85))

-   **エミュレートされたホストコントローラーと接続された仮想デバイスを開発するための新しいプログラミングインターフェイスのセット。**

    Windows 10 では、エミュレートされたデバイスのサポートが導入されました。 エミュレートされた Universal Serial Bus (USB) ホスト コントローラー ドライバーと接続された仮想 USB デバイスを開発できるようになりました。 いずれのコンポーネントも、Microsoft 提供の USB デバイス エミュレーション クラス拡張 (UdeCx) と通信する 1 つの KMDF ドライバーに統合されます。

    [列挙された USB デバイス (UDE) 用 Windows ドライバーの開発](developing-windows-drivers-for-emulated-usb-host-controllers-and-devices.md)

    [エミュレートされた USB ホスト コントローラー ドライバーのプログラミング参照](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt628025(v=vs.85))

-   **USB ホストコントローラードライバーを開発するための新しいプログラミングインターフェイスのセット。**

    ハードウェアが xHCI 仕様に準拠していない場合、または、TCP 接続を介して USB トラフィックをデバイスに接続されている周辺機器にルーティングするコントローラーなどの仮想ホストコントローラーを作成している場合は、ホストコントローラーを開発できます。 ホストコントローラードライバーは、USB ホストコントローラー拡張機能のクライアントです。これは、フレームワーククラス拡張モデルに従ったシステム提供のドライバーです。 [MICROSOFT usb 3.0 ドライバースタック](https://docs.microsoft.com/windows-hardware/drivers/ddi/index#usb-3-0-driver-stack)内では、ucx は、usb ホストコントローラーデバイスを管理するためのホストコントローラードライバーを支援する機能を提供します。

    [USB ホスト コントローラー用 Windows ドライバーの開発](developing-windows-drivers-for-usb-host-controllers.md)

    [USB ホスト コントローラー拡張 (UCX) 参照](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188009(v=vs.85))

-   **USB 関数コントローラードライバーを開発するための新しいプログラミングインターフェイスのセット。**

    USB 関数クラス拡張 (UFX) と通信し、コントローラー固有の操作を実装するクライアントドライバーを作成できます。 UFX は、すべての USB 関数コントローラーに共通の USB 関数ロジックを処理します。

    [Windows の USB デバイス側ドライバー](usb-device-side-drivers-in-windows.md)

    [USB 関数クライアントドライバーで使用される UFX オブジェクトとハンドル](ufx-objects-and-handles-used-by-a-usb-function-controller.md)

    [関数コントローラークライアントドライバーのタスク](function-client-driver.md)

    [ユーザーモードサービスから UFX プログラミングリファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

    [USB 関数クラスドライバーから UFX プログラミングリファレンス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188008(v=vs.85))

    [USB 関数コントローラークライアントドライバーのプログラミングリファレンス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188010(v=vs.85))

    [独自の充電器をサポートするための USB フィルタードライバー](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188012(v=vs.85))

-   **USB CDC (シリアル) デバイスのエクスペリエンスが向上しました。**

    USB 通信デバイスクラス (クラス\_02 & サブクラス\_02) に準拠しているデバイスが、Usbser ドライバーを使用して Windows 10 を操作できるようにします。 デバイスの製造元は、そのドライバーをインストールするためのカスタム INF を作成する必要がなくなりました。

    [USB シリアルドライバー (Usbser)](usb-driver-installation-based-on-compatible-ids.md)

 

 




