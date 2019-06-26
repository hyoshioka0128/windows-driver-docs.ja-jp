---
Description: USB タイプ-c システムとハードウェア コンポーネントをサポートする Microsoft 提供のドライバーの一般的なハードウェア設計について説明します。
title: Windows システムの設計を USB 型-C# のアーキテクチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8e584929528c85dcb5002dea4dae9abfd3ba025
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384490"
---
# <a name="architecture-usb-type-c-design-for-a-windows-system"></a>アーキテクチャ:Windows システム向け USB Type-C デザイン


**Oem USB 型-C# のコネクタとシステムの開発に適用されます。**

-   USB 型-C# を使用した USB デュアル ロール機能
-   USB タイプ-C の現在のレベルと電源配信 2.0 を使用して高速な充電中
-   使用して表示アウト機能は、別のモードと、ドッキングのエクスペリエンスをワイヤード (有線) です。

**最終更新日**

-   2016 年 12 月

**Windows のバージョン**

-   Windows 10 デスクトップ エディション (Home、Pro、Enterprise、Education)
-   Windows 10 Mobile

USB タイプ-c システムとハードウェア コンポーネントをサポートする Microsoft 提供のドライバーの一般的なハードウェア設計について説明します。

## <a href="" id="drivers"></a>USB 型-C# のコンポーネントをサポートするためのドライバー


![usb タイプ c ソフトウェア コンポーネント](images/type-c-arch.png)

上の図

-   **デバイス側の USB ドライバー**

    [デバイス側の USB ドライバー](usb-device-side-drivers-in-windows.md)関数デバイス/周辺機器のサービスを提供します。 USB 関数コント ローラー クラスの拡張サポート MTP (Media Transfer Protocol) と充電 BC 1.2 を使用しています。 Microsoft では、Synopsys USB 3.0、および ChipIdea USB 2.0 コント ローラーの組み込みのクライアント ドライバーを提供します。 使用して、関数のコント ローラーのカスタム クライアント ドライバーを記述する[USB 関数コント ローラー クライアント ドライバーのプログラミング インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188010(v=vs.85))します。 詳細については、次を参照してください。 [usb ドライバーを Windows の開発機能のコント ローラー](developing-windows-drivers-for-usb-function-controllers.md)します。

    SoC ベンダー可能性があります関数下位の USB フィルター ドライバーとの提供レガシ独自充電器の検出。 独自のフィルター ドライバーを実装するには、関数のコント ローラーが Synopsys USB 3.0 または ChipIdea USB 2.0 コント ローラーの場合

-   **ホスト側の USB ドライバー**

    ホスト側の USB ドライバーでは、EHCI または XHCI 準拠の USB ホスト コント ローラーを使用するドライバーのセットです。 役割の交代ドライバー ホスト ロールを列挙する場合は、ドライバーが読み込まれます。 ホスト コント ローラーが仕様に準拠していないかどうかは、使用してカスタム ドライバーを記述する[USB ホスト コント ローラーの拡張機能 (UCX) プログラミング インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188009(v=vs.85))します。 詳しくは、次を参照してください。[開発 Windows ドライバーの USB ホスト コント ローラー](developing-windows-drivers-for-usb-host-controllers.md)します。

    **注**  いない[USB デバイスのすべてのクラス](supported-usb-classes.md)Windows 10 Mobile でサポートされます。

     

-   **役割の交代の USB ドライバー (URS)**

    デュアル ロールの USB ポートが Windows ホストまたは関数のいずれかのモードに構成する必要があるように、システムを設計できます。 これらの設計は、ロール スイッチ (URS) の USB ドライバー スタックを使用する必要があります。

    URS ドライバーでは、コネクタ、ホストまたは関数、および読み込みの現在のロールと、適切なデバイス側またはホスト側ドライバーのプラットフォームからハードウェア イベントに基づくアンロードを管理します。 Microsoft では、Synopsys USB 3.0、および ChipIdea USB 2.0 コント ローラーの組み込みのクライアント ドライバーを提供します。 使用して、役割の交代クライアント ドライバーを記述することができます、 [USB デュアル ロール コント ローラー ドライバーのプログラミング インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt628026(v=vs.85))します。 役割の交代ドライバーを有効にするには、ACPI テーブルに変更を加える必要があります。 詳細については、次を参照してください。 [USB デュアル ロール ドライバー スタック アーキテクチャ](usb-dual-role-driver-stack-architecture.md)します。

    システム USB マイクロ AB コネクタでは、このに基づいて決定されます、コネクタの ID のピンにします。 ID の暗証番号 (pin) の検出は、割り込みのリソース割り当てを使用して、クライアント ドライバーによって実行されます。

    システム型-C# の USB コネクタでは、上、に基づいて決定されます CC ピンにします。 コネクタのクライアント ドライバーでは、[cc] の検出を実行し、役割の交代ドライバーには、その情報を転送します。

-   **USB コネクタ マネージャ (UCM)**

    この一連のドライバーでは、USB 型-c コネクタのすべての側面を管理します。 システムでは、ACPI に準拠 UCSI 埋め込みコント ローラーを実装する場合は、Microsoft を使用して[UCSI ドライバー](ucsi.md)します。 それ以外の場合[UCSI クライアント ドライバーを書く](write-a-ucsi-driver.md)非 ACPI トランスポート。

    ハードウェアが UCSI-準拠していないかどうかは、予想される[型-C# の USB コネクタ ドライバー](bring-up-a-usb-type-c-connector-on-a-windows-system.md) UCM クラスの拡張機能をクライアントには。 まとめて、USB 型-c コネクタとコネクタのドライバーの想定される動作を管理します。

    ドライバーを作成する場合、USB コネクタ マネージャー クラス拡張は、WDF クラスの拡張機能クライアント ドライバー モデルに従います。 ハードウェアと CC の検出、メッセージング、マルチプレキシング、PD などのタスクを処理するために、クラスの拡張と通信して、クライアント ドライバー VBus/VConn コントロール、および power 配信と代替のモードのポリシーを選択します。 クラスの拡張機能では、オペレーティング システムにクライアント ドライバーによって報告される情報と通信します。 役割の交代ドライバー; を構成する [cc] 検出結果を使用する例。システムを請求するレベルを決定する USB 型-C/PD 電源に関する情報が使用されます。 クライアント ドライバーでは、USB 型-c および PD のステート マシンを管理します。 クライアント ドライバーは、他のドライバーをいくつかのタスクを委任できます、たとえば、Mux 別のドライバーを使って制御できます。 クライアント ドライバーを作成するには、使用、[型-C# の USB コネクタ ドライバーのプログラミング インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188011(v=vs.85))します。

    **USB タイプ-c ポート コント ローラー**

    型 C ポートのコント ローラー インターフェイス クラス拡張 (UcmTcpciCx.sys) は、OS として、型 C ポート マネージャー (TCPM) PD のステート マシンを実装していないコネクタの動作には、Microsoft によって提供される USB コネクタ マネージャーに拡張機能です。 UcmTcpciCx クライアント ドライバーでは、ソフトウェア、ハードウェアを制御し、その状態をリアルタイムで入手 TCPM ができます。

    クライアント ドライバーの記述については、次を参照してください。[型-C# の USB ポート コント ローラー ドライバー](write-a-usb-type-c-port-controller-driver.md)します。

-   **充電調停ドライバー**

    このドライバーは、Windows 10 Mobile 用 Microsoft によって提供されます。 ドライバーは、課金の複数のソースのアービターとして機能します。 USB コネクタ マネージャは、USB 型-c および情報と BC1.2 充電器検出によって実行されたこと (該当する) 場合は、USB デバイス側のドライバーから選択する、CAD にソース情報を充電 PD を報告します。 CAD は、バッテリのサブシステムに使用する最も適切な充電ソースを報告します。

-   **バッテリのドライバー**

    クラス ドライバーはシステム内のバッテリの全体的な機能を定義し、電源マネージャーとやり取りします。 Miniclass ドライバーでは、デバイス固有の関数を追加して、バッテリの削除の容量と料金の追跡などを処理します。 Miniclass ドライバーでは、クラス ドライバーは制御デバイスに関する情報を取得するために呼び出すルーチンをエクスポートします。

 

 




