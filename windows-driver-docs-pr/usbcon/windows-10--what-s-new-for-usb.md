---
Description: Highlights the new features and improvements for Universal Serial Bus (USB) in Windows 10.
title: Windows 10 - 新機能については、usb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f319c777e662059ee146d02321d15b73e11b2fa
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548644"
---
# <a name="windows-10-whats-new-for-usb"></a>Windows 10:USB の新機能については


このトピックでは、新機能と機能強化のユニバーサル シリアル バス (USB) Windows 10 で強調表示されます。

-  **UCSI ドライバーの拡張機能**以降では、Windows 10、バージョンは 1809、UCSI (UcmUcsiCx.sys) の新しいクラスの拡張機能が追加されました、UCSI 仕様を実装するトランスポートに依存しない方法。 最小限のコードで、ドライバーが UcmUcsiCx をクライアントでは、非 ACPI トランスポート経由で USB 型-C# のハードウェアと通信できます。 このトピックでは、UCSI クラスの拡張機能と、クライアント ドライバーの想定される動作が提供するサービスについて説明します。

-   **コント ローラー インターフェイスの型から C の USB ポート** 

    Windows 10 バージョン 1703 では、クラスの拡張 (UcmTcpciCx.sys) 仕様をサポートするユニバーサル シリアル バスの種類 C ポート コント ローラー インターフェイスを提供します。 USB タイプ-c コネクタ ドライバーは、内部 PD/型の C 状態を管理する必要はありません。 
    USB タイプ-c コネクタと USB 電力配信 (PD) ステート マシンの管理の複雑さは、システムによって処理されます。 のみ、クラスの拡張機能を介してシステムにハードウェアのイベントを通信するクライアント ドライバーを作成する必要があります。 

    [USB タイプ C ポート コント ローラー インターフェイス ドライバー クラスの拡張機能のリファレンス](https://msdn.microsoft.com/library/windows/hardware/mt805826)

-   **USB デュアル ロールのサポート。**

    Windows では、2 つのロールを USB コント ローラーはサポートされています。 Windows には、ChipIdea および Synopsys コント ローラーの組み込みのクライアント ドライバーが含まれています。 他のコント ローラーは、Microsoft は、一連のプログラミング インターフェイスがデュアル role クラスの拡張機能 (UrsCx) とデュアル ロール コント ローラーの役割の交代機能を処理するために互いに通信するには、そのクライアント ドライバーを提供します。

    この機能の詳細についてを参照してください。

    [USB ドライバー スタック アーキテクチャがデュアル ロール](usb-dual-role-driver-stack-architecture.md)

    [USB コント ローラーのデュアル ロール ドライバーのプログラミング リファレンス](https://msdn.microsoft.com/library/windows/hardware/mt628026)

-   **USB タイプ-c コネクタのドライバーを開発するためのプログラミング インターフェイスの新しいセットします。**

    このバージョンは、USB 3.1 仕様で定義されている USB 型-C# 用のネイティブ サポートについて説明します。 機能は、元に戻すことのコネクタ、充電が高速化、対称のケーブル、USB ケーブルを実行している別のモードを使用するデバイスを使用できます。 これらのプログラミング インターフェイスでは、Microsoft から提供されたクラスの拡張機能モジュールと通信するコネクタ (このセクションでは、クライアント ドライバーと呼ばれます) のドライバーを作成できます。シナリオに対応する UcmCx コネクタに関連する種類 C など、どのポートがどの電源に提供するサポートのポートの種類 C をサポートします。

    [USB タイプ-c コネクタの Windows ドライバーの開発](developing-windows-drivers-for-usb-type-c-connectors.md)

    [USB コネクタ マネージャー クラスの拡張機能 (UcmCx)](https://msdn.microsoft.com/library/windows/hardware/mt188011)

-   **プログラミング インターフェイス、エミュレートされたホストのコント ローラーと接続されている仮想デバイスを開発するための新しいセットします。**

    Windows 10 には、エミュレートされたデバイスのサポートが導入されています。 これでエミュレートされたユニバーサル シリアル バス (USB) ホスト コント ローラー ドライバーと、接続された仮想の USB デバイスを開発できます。 両方のコンポーネントは、Microsoft 提供の USB デバイスのエミュレーション クラス拡張 (UdeCx) と通信する 1 つの KMDF ドライバーに結合されます。

    [エミュレートされた USB デバイス (UDE) の Windows ドライバーの開発](developing-windows-drivers-for-emulated-usb-host-controllers-and-devices.md)

    [エミュレートされた USB ホスト コント ローラー ドライバー プログラミング リファレンス](https://msdn.microsoft.com/library/windows/hardware/mt628025)

-   **新しい USB ホスト コント ローラー ドライバーを開発するためのプログラミング インターフェイスのセットします。**

    ホスト コント ローラーを開発するには、xHCI の仕様に準拠していませんか中である、ハードウェアがない場合、デバイスに接続されている周辺機器への TCP 接続経由で USB のトラフィックをルーティングするコント ローラーなどの仮想ホスト コント ローラーを作成します。 ホスト コント ローラーのドライバーは、framework クラスの拡張機能モデルを次のシステム提供のドライバーである USB ホスト コント ローラー拡張にクライアントです。 内で、 [Microsoft USB 3.0 ドライバー スタック](https://msdn.microsoft.com/library/windows/hardware/hh406256.aspx#usb-3-0-driver-stack)UCX は USB ホスト コント ローラー デバイスの管理コント ローラー用ドライバーのホストを支援する機能を提供します。

    [USB ホスト コント ローラーの Windows ドライバーの開発](developing-windows-drivers-for-usb-host-controllers.md)

    [USB ホスト コント ローラーの拡張機能 (UCX) リファレンス](https://msdn.microsoft.com/library/windows/hardware/mt188009)

-   **新しい USB 関数のコント ローラーのドライバーを開発するためのプログラミング インターフェイスのセットします。**

    USB の関数クラスの拡張機能 (UFX) と通信し、コント ローラーに固有の操作を実装するクライアント ドライバーを記述することができます。 UFX は、USB 関数のすべてのコント ローラーに共通する USB 関数のロジックを処理します。

    [Windows での USB デバイス側のドライバー](usb-device-side-drivers-in-windows.md)

    [UFX オブジェクトと関数の USB クライアント ドライバーによって使用されるハンドル](ufx-objects-and-handles-used-by-a-usb-function-controller.md)

    [関数のコント ローラーのクライアント ドライバーのタスク](function-client-driver.md)

    [ユーザー モード サービス UFX プログラミング リファレンス](https://msdn.microsoft.com/library/windows/hardware/mt188014)

    [USB クラス ドライバーを関数 UFX プログラミング リファレンスを](https://msdn.microsoft.com/library/windows/hardware/mt188008)

    [USB 関数コント ローラー クライアント ドライバーのプログラミング リファレンス](https://msdn.microsoft.com/library/windows/hardware/mt188010)

    [独自の充電器をサポートするための USB フィルター ドライバー](https://msdn.microsoft.com/library/windows/hardware/mt188012)

-   **USB の CDC (シリアル) デバイスのエクスペリエンスも向上します。**

    USB 通信デバイス クラスに対応しているデバイスを許可 (クラス\_02 & サブクラス\_02) Usbser.sys ドライバーを使用して Windows 10 を使用します。 デバイスの製造元は、そのドライバーをインストールするカスタム INF を記述する必要はなくなります。

    [USB シリアル ドライバー (Usbser.sys)](usb-driver-installation-based-on-compatible-ids.md)

 

 




