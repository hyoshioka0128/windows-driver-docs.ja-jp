---
Description: USB 関数のスタックのアーキテクチャについて説明します。
title: Windows の USB デバイス側ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 58fabc40be1d6ca019b64572d71102730b647151
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380584"
---
# <a name="usb-device-side-drivers-in-windows"></a>Windows の USB デバイス側ドライバー


USB 関数のスタックのアーキテクチャについて説明します。




USB デバイス、USB 関数のスタックは ACPI は、USB デバイスの物理デバイス オブジェクト (PDO) を作成するときに、プラグ アンド プレイ マネージャーによってに列挙されているドライバーのグループを表します。

1 つの構成のデバイスで USB デバイスが 1 つまたは複数のインターフェイスを定義できます。 たとえば、メディア転送プロトコル (MTP) デバイスからファイルを転送するためです。 複合 USB デバイスは、1 つの構成で複数のインターフェイスをサポートできます。 USB 関数のスタックは、各インターフェイスの Pdo を作成し、PnP マネージャーがそのインターフェイスの関数 (FDO) デバイス オブジェクトを作成するクラス ドライバーを読み込みます。

USB 関数のスタックは、このイメージで概念化します。

![usb 関数のスタック](images/usb-fn.png)

**アプリケーションとサービス**

- ユーザー モードのすべての要求は、Microsoft から提供されたカーネル モード クラス ドライバー GenericUSBFn.sys に送信されます。 定義されている I/O 制御コード (Ioctl) を送信することによって、GenericUSBFn.sys と通信するユーザー モード サービスを作成できます[genericusbfnioctl.h](https://docs.microsoft.com/windows/desktop/api/genericusbfnioctl/)します。 これらの Ioctl の詳細については、次を参照してください[GenericUSBFn.sys とユーザー モード サービスからの通信。](https://docs.microsoft.com/windows-hardware/drivers/usbcon/user-mode-services-ufx)

**関数の USB クラス ドライバー**

USB の関数クラス ドライバーは、USB デバイスに特定のインターフェイス (またはインターフェイスのグループ) の機能を実装します。 MTP と IpOverUsb は、システム指定のクラス ドライバーの例を示します。 カーネル モード ドライバーでは、単なるとしてクラス ドライバーを実装することがあります。 またはユーザー モード サービスがシステム指定のクラス ドライバー GenericUSBFn.sys とペアになっている場合があります。

関数のクラス ドライバーを使用して、コント ローラーに要求を送信します[USB クラス ドライバーを関数 UFX プログラミング インターフェイスを](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188008(v=vs.85))します。

**USB 関数クラスの拡張機能 (UFX)**

USB の関数クラスの拡張機能 (UFX) するシステム提供の拡張機能は、[カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-debugging)(KMDF)。 USB は標準バスといくつか必要な機能と機能します。 UFX は USB 関数のすべてのコント ローラーに共通する USB 関数のロジックを実装して処理や USB クラス ドライバーが関数からの要求をディスパッチします。 具体的には、UFX は、デバイスを列挙して、標準のコントロールの転送を処理するプロセスを処理します。 これらの操作を実行するのには、UFX をバスの機能について知っておく必要があります。 これらの機能は、クラス拡張機能インターフェイスが確立されたときに、UFX に報告されます。

UFX では、上位層 (USB 関数クラスと、ドライバーとユーザー モード サービス) を使用してコント ローラーに要求を送信する標準の Ioctl を公開します。 さらに、UFX ホストから受信した標準の要求についての上位の層に通知します。

**USB 関数クライアント ドライバー**

UFX は、異なるコント ローラー間で一貫して機能する抽象化されたインターフェイスを提供します。 ただし、コント ローラーには、エンドポイントの数、エンドポイント、省電力、リモート ウェイク アップの種類などの制限事項と、さまざまな機能があります。 たとえば、特定のコント ローラーは、そうでないときに、DMA をサポートします。 一部のコント ローラーは、他のコント ローラーにストリームを処理するために、ドライバーが予想されるときに、ハードウェアにストリームを実装します。 これらの理由から、共通の機能は、UFX で処理されます。 転送、電源管理、ストリームのサポート、およびコント ローラーからコント ローラーが異なるその他の機能は、クライアント ドライバーによって処理されます。

関数の USB クライアント ドライバーは、コント ローラーに固有の操作を実装する責任を負います。 エンドポイントのデータの実装が含まれます (リセット、中断、再開) に転送では、USB デバイスの状態の変更の検出、ポート/充電器検出のアタッチ/デタッチします。 クライアント ドライバーは電源管理、および PnP イベントを処理するためも担当します。

関数のクライアント ドライバーとして書き込まれます[カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/debugger/kernel-mode-driver-framework-debugging)(KMDF) ドライバーを使用して[USB クラス ドライバーを関数 UFX プログラミング インターフェイスを](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188008(v=vs.85))します。

Microsoft は、ChipIdea および Synopsys コント ローラーのクライアント ドライバー (UfxChipidea.sys、Ufxsynopsys.sys) ボックスに関数を提供します。

**下位のフィルター ドライバーを USB**

USB の低いフィルター ドライバーは、関数のコント ローラーは、インボックス Synopsys と ChipIdea のドライバーを使用している場合、充電器の検出をサポートしています。 フィルター ドライバーを USB 充電 USB ポートの検出から管理します。 t は、サポート各充電器の種類とその充電器のプロパティの一覧の GUID を発行する必要があります。 特定の充電器が構成可能な場合は、下位の USB フィルター ドライバーはサポートされているプロパティ Id と充電器を構成するには、送信できる、対応する値型の一覧を定義します。 ドライバーでは、課金を開始し、デバイスに描画できる現在の最大量と、バッテリのスタックも通知します。 Synopsys 以外のクライアント ドライバーと ChipIdea ドライバーは、ロジックの充電で実装できますクライアント ドライバー。

関数のクラス ドライバー UFX を使用して要求を送信する[独自の充電器をサポートするためのプログラミング インターフェイス](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt188012(v=vs.85))します。

## <a name="related-topics"></a>関連トピック
[ユニバーサル シリアル バス (USB)](https://docs.microsoft.com/windows-hardware/drivers/)  



