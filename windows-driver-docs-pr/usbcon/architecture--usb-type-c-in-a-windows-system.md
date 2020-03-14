---
Description: USB タイプ C システムの一般的なハードウェア設計と、ハードウェアコンポーネントをサポートする Microsoft 提供のドライバーについて説明します。
title: Windows システムの USB タイプ C 設計のアーキテクチャ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8e584929528c85dcb5002dea4dae9abfd3ba025
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242743"
---
# <a name="architecture-usb-type-c-design-for-a-windows-system"></a>アーキテクチャ: Windows システム向けの USB タイプ C 設計


**USB タイプ C コネクタを使用してシステムを開発する Oem に適用されます**

-   Usb タイプ-C を使用した USB デュアルロール機能
-   USB タイプ-C の現在のレベルと電力配信2.0 を使用した課金の高速化
-   代替モードとワイヤード (有線) ドッキングエクスペリエンスを使用して、出力機能を表示します。

**最終更新日時**

-   2016 年 12 月

**Windows のバージョン**

-   Windows 10 デスクトップ エディション (Home、Pro、Enterprise、Education)
-   Windows 10 Mobile

USB タイプ C システムの一般的なハードウェア設計と、ハードウェアコンポーネントをサポートする Microsoft 提供のドライバーについて説明します。

## <a href="" id="drivers"></a>USB タイプ C コンポーネントをサポートするためのドライバー


![usb タイプ-c ソフトウェアコンポーネント](images/type-c-arch.png)

上の図では、

-   **USB デバイス側ドライバー**

    [USB デバイス側ドライバー](usb-device-side-drivers-in-windows.md)は、機能/デバイス/周辺機器を処理します。 USB 関数コントローラークラス拡張は、MTP (メディア転送プロトコル) をサポートし、BC 1.2 充電器を使用して課金します。 Microsoft には、Synopsys USB 3.0 および ChipIdea USB 2.0 コントローラー用のインボックスクライアントドライバーが用意されています。 関数コントローラー用のカスタムクライアントドライバーは、 [USB 関数コントローラークライアントドライバーのプログラミングインターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188010(v=vs.85))を使用して作成できます。 詳細については、「 [USB 機能コントローラー用の Windows ドライバーの開発](developing-windows-drivers-for-usb-function-controllers.md)」を参照してください。

    SoC ベンダは、従来の専用チャージャー検出用に USB 関数の下位フィルタードライバーを提供する場合があります。 関数コントローラーが Synopsys USB 3.0 または ChipIdea USB 2.0 コントローラーの場合は、独自のフィルタードライバーを実装できます。

-   **USB ホスト側ドライバー**

    USB ホスト側ドライバーは、EHCI または XHCI 準拠の USB ホストコントローラーで動作するドライバーのセットです。 ドライバーは、役割スイッチドライバーがホストの役割を列挙した場合に読み込まれます。 ホストコントローラーが仕様に準拠していない場合は、 [USB ホストコントローラー拡張 (UCX) プログラミングインターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188009(v=vs.85))を使用してカスタムドライバーを作成できます。 詳細については、「 [USB ホストコントローラー用の Windows ドライバーの開発](developing-windows-drivers-for-usb-host-controllers.md)」を参照してください。

    **注**  Windows 10 Mobile では、[一部の USB デバイスクラス](supported-usb-classes.md)がサポートされていないことに注意してください。

     

-   **USB 役割-スイッチドライバー (URS)**

    システムは、デュアルロールの USB ポートに Windows が必要であり、ホストモードまたは機能モードに構成できるように設計できます。 これらの設計では、USB 役割スイッチ (URS) ドライバースタックを使用する必要があります。

    URS ドライバーは、コネクタ、ホスト、または機能の現在の役割、およびプラットフォームからのハードウェアイベントに基づく、適切なデバイス側またはホスト側ドライバーの読み込みとアンロードを管理します。 Microsoft には、Synopsys USB 3.0 および ChipIdea USB 2.0 コントローラー用のインボックスクライアントドライバーが用意されています。 [USB デュアルロールコントローラードライバーのプログラミングインターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt628026(v=vs.85))を使用して、ロールスイッチクライアントドライバーを作成できます。 ロールスイッチドライバーをアクティブ化するには、ACPI テーブルに変更を加える必要があります。 詳細については、「 [USB デュアルロールドライバースタックアーキテクチャ](usb-dual-role-driver-stack-architecture.md)」を参照してください。

    USB micro AB コネクタを使用するシステムでは、この決定はコネクタの ID ピンに基づいて行われます。 ID pin の検出は、クライアントドライバーに割り当てられている割り込みリソースを使用して実行されます。

    USB タイプの C コネクタを使用するシステムでは、CC ピンに基づいて決定が行われます。 コネクタのクライアントドライバーは、CC 検出を実行し、その情報を役割スイッチドライバーに転送します。

-   **USB コネクタマネージャー (UCM)**

    この一連のドライバーは、USB タイプ C コネクタのすべての側面を管理します。 システムが ACPI 経由で UCSI 準拠の埋め込みコントローラーを実装している場合は、Microsoft 提供の[ucsi ドライバー](ucsi.md)を使用します。 それ以外の場合は、非 ACPI トランスポート用の[UCSI クライアントドライバーを記述](write-a-ucsi-driver.md)します。

    ハードウェアが UCSI に準拠していない場合は、UCM クラス拡張に対するクライアントである[USB タイプ C コネクタドライバーを作成](bring-up-a-usb-type-c-connector-on-a-windows-system.md)する必要があります。 これらの組み合わせは、USB タイプ C コネクタと、コネクタドライバーの予期される動作を管理します。

    ドライバーを作成する場合、USB コネクタマネージャーのクラス拡張は、WDF クラスの拡張クライアントドライバーモデルに従います。 クライアントドライバーは、ハードウェアおよびクラス拡張と通信して、CC 検出、PD messaging、マルチプレキシング、VBus/Vbus コントロールなどのタスクを処理し、電力配信と代替モードのポリシーを選択します。 クラス拡張は、クライアントドライバーから報告された情報をオペレーティングシステムに伝えます。 たとえば、CC 検出の結果を使用して、ロールスイッチドライバーを構成します。USB タイプ-C/PD 電力情報は、システムが課金するレベルを決定するために使用されます。 クライアントドライバーは、USB タイプ C および PD ステートマシンを管理します。 クライアントドライバーは、一部のタスクを他のドライバーに委任できます。たとえば、Mux は別のドライバーによって制御される場合があります。 クライアントドライバーを作成するには、 [USB タイプの C コネクタドライバーのプログラミングインターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188011(v=vs.85))を使用します。

    **USB タイプ-C ポートコントローラー**

    C ポートコントローラーインターフェイスクラス拡張 (UcmTcpciCx .sys) は、Microsoft によって提供される USB コネクタマネージャーの拡張機能であり、この機能により、システムは、PD ステートマシンを実装していないコネクタのタイプ C ポートマネージャー (TCPM) として動作することができます。 UcmTcpciCx クライアントドライバーを使用すると、ソフトウェア TCPM はハードウェアを制御し、その状態をリアルタイムで取得できます。

    クライアントドライバーの作成の詳細については、「 [Write a USB Type-C port controller driver](write-a-usb-type-c-port-controller-driver.md)」を参照してください。

-   **調停ドライバーの課金**

    このドライバーは、Microsoft によって Windows 10 Mobile 用に提供されています。 このドライバーは、複数の課金ソースの監視として機能します。 Usb コネクタマネージャーは、usb タイプ C と PD の課金ソース情報を CAD に報告します。これにより、USB デバイス側ドライバー (該当する場合) によって実行される、その情報と BC 1.2 チャージャーの検出が選択されます。 次に、CAD は、バッテリサブシステムに使用する最も適切な課金ソースを報告します。

-   **バッテリドライバー**

    クラス ドライバーはシステム内のバッテリの全体的な機能を定義し、電源マネージャーとやり取りします。 Miniclass ドライバーは、バッテリの追加や取り外し、容量と料金の追跡などのデバイス固有の機能を処理します。 Miniclass ドライバーは、制御しているデバイスに関する情報を取得するために、クラスドライバーが呼び出すルーチンをエクスポートします。

 

 




