---
Description: 新機能と機能強化のユニバーサル シリアル バス (USB) Windows 10 で強調表示されます。
title: Windows 10 - 新機能については、usb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06c240bfc6217ddb96a343375e4645e283904d16
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356543"
---
# <a name="windows-10-whats-new-for-usb"></a>Windows 10:USB の新機能


このトピックでは、新機能と機能強化のユニバーサル シリアル バス (USB) Windows 10 で強調表示されます。

-  **UCSI ドライバーの拡張機能**以降では、Windows 10、バージョンは 1809、UCSI (UcmUcsiCx.sys) の新しいクラスの拡張機能が追加されました、UCSI 仕様を実装するトランスポートに依存しない方法。 最小限のコードで、UcmUcsiCx へのクライアントであるドライバーが非 ACPI トランスポート経由で USB Type-C ハードウェアと通信できます。 このトピックでは、UCSI クラス拡張機能で提供されるサービスと、クライアント ドライバーの想定される動作について説明します。

-   **コント ローラー インターフェイスの型から C の USB ポート** 

    Windows 10 バージョン 1703 では、クラスの拡張 (UcmTcpciCx.sys) 仕様をサポートするユニバーサル シリアル バスの種類 C ポート コント ローラー インターフェイスを提供します。 USB Type-C コネクタ ドライバーで内部の PD/Type-C 状態を保持しておく必要はありません。 
    USB Type-C コネクタと USB 電源供給 (PD) ステート マシンの複雑な管理はシステムによって処理されます。 必要なのは、クラス拡張機能を介してハードウェアのイベントをシステムに通信するクライアント ドライバーを作成することだけです。 

    [USB タイプ C ポート コント ローラー インターフェイス ドライバー クラスの拡張機能のリファレンス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt805826(v=vs.85))

-   **USB デュアル ロールのサポート。**

    Windows では、2 つのロールを USB コント ローラーはサポートされています。 Windows には、ChipIdea コントローラーと Synopsys コントローラーのためのインボックス クライアント ドライバーが含まれています。 その他のコントローラーの場合、デュアルロール クラス拡張 (UrsCx) とそのクライアント ドライバーが互いに通信し、デュアルロール コントローラーのロール切り替え機能を処理できるようにする一連のプログラミング インターフェイスが Microsoft から提供されます。

    この機能の詳細については、以下を参照してください。

    [USB デュアル ロール ドライバー スタック アーキテクチャ](usb-dual-role-driver-stack-architecture.md)

    [USB デュアルロール コントローラー ドライバーのプログラミング参照](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt628026(v=vs.85))

-   **USB タイプ-c コネクタのドライバーを開発するためのプログラミング インターフェイスの新しいセットします。**

    このバージョンは、USB 3.1 仕様で定義されている USB 型-C# 用のネイティブ サポートについて説明します。 機能は、元に戻すことのコネクタ、充電が高速化、対称のケーブル、USB ケーブルを実行している別のモードを使用するデバイスを使用できます。 これらのプログラミング インターフェイスでは、Microsoft から提供されたクラスの拡張機能モジュールと通信するコネクタ (このセクションでは、クライアント ドライバーと呼ばれます) のドライバーを作成できます。UcmCx は、どのポートで Type-C をサポートするか、どのポートで補助電源を与えるかなど、Type-C コネクタに関連するシナリオに対応します。

    [USB Type-C コネクタ用 Windows ドライバーの開発](developing-windows-drivers-for-usb-type-c-connectors.md)

    [USB コネクタ マネージャー クラス拡張 (UcmCx)](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188011(v=vs.85))

-   **プログラミング インターフェイス、エミュレートされたホストのコント ローラーと接続されている仮想デバイスを開発するための新しいセットします。**

    Windows 10 では、エミュレートされたデバイスのサポートが導入されました。 エミュレートされた Universal Serial Bus (USB) ホスト コントローラー ドライバーと接続された仮想 USB デバイスを開発できるようになりました。 いずれのコンポーネントも、Microsoft 提供の USB デバイス エミュレーション クラス拡張 (UdeCx) と通信する 1 つの KMDF ドライバーに統合されます。

    [列挙された USB デバイス (UDE) 用 Windows ドライバーの開発](developing-windows-drivers-for-emulated-usb-host-controllers-and-devices.md)

    [エミュレートされた USB ホスト コントローラー ドライバーのプログラミング参照](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt628025(v=vs.85))

-   **新しい USB ホスト コント ローラー ドライバーを開発するためのプログラミング インターフェイスのセットします。**

    ホスト コント ローラーを開発するには、xHCI の仕様に準拠していませんか中である、ハードウェアがない場合、デバイスに接続されている周辺機器への TCP 接続経由で USB のトラフィックをルーティングするコント ローラーなどの仮想ホスト コント ローラーを作成します。 ホスト コント ローラーのドライバーは、framework クラスの拡張機能モデルを次のシステム提供のドライバーである USB ホスト コント ローラー拡張にクライアントです。 内で、 [Microsoft USB 3.0 ドライバー スタック](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index#usb-3-0-driver-stack)UCX は USB ホスト コント ローラー デバイスの管理コント ローラー用ドライバーのホストを支援する機能を提供します。

    [USB ホスト コントローラー用 Windows ドライバーの開発](developing-windows-drivers-for-usb-host-controllers.md)

    [USB ホスト コントローラー拡張 (UCX) 参照](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188009(v=vs.85))

-   **新しい USB 関数のコント ローラーのドライバーを開発するためのプログラミング インターフェイスのセットします。**

    USB の関数クラスの拡張機能 (UFX) と通信し、コント ローラーに固有の操作を実装するクライアント ドライバーを記述することができます。 UFX は、USB 関数のすべてのコント ローラーに共通する USB 関数のロジックを処理します。

    [Windows での USB デバイス側のドライバー](usb-device-side-drivers-in-windows.md)

    [UFX オブジェクトと関数の USB クライアント ドライバーによって使用されるハンドル](ufx-objects-and-handles-used-by-a-usb-function-controller.md)

    [関数のコント ローラーのクライアント ドライバーのタスク](function-client-driver.md)

    [ユーザー モード サービス UFX プログラミング リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

    [USB クラス ドライバーを関数 UFX プログラミング リファレンスを](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188008(v=vs.85))

    [USB 関数コント ローラー クライアント ドライバーのプログラミング リファレンス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188010(v=vs.85))

    [独自の充電器をサポートするための USB フィルター ドライバー](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188012(v=vs.85))

-   **USB の CDC (シリアル) デバイスのエクスペリエンスも向上します。**

    USB 通信デバイス クラスに対応しているデバイスを許可 (クラス\_02 & サブクラス\_02) Usbser.sys ドライバーを使用して Windows 10 を使用します。 デバイスの製造元は、そのドライバーをインストールするカスタム INF を記述する必要はなくなります。

    [USB シリアル ドライバー (Usbser.sys)](usb-driver-installation-based-on-compatible-ids.md)

 

 




