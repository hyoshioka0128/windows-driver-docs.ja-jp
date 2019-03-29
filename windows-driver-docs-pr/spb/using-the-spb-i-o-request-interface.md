---
title: SPB I/O 要求インターフェイスの使用
description: 以降では、Windows 8、SPB フレームワークの拡張機能 (SpbCx) は、SPB の I/O 要求インターフェイスをサポートするシステム提供のコンポーネントです。
ms.assetid: 0A752413-FA0B-4C26-BF6D-19033E07095E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91ebce26adba414e14a4685b2f664248c99bfe23
ms.sourcegitcommit: a5cbd86f3019a54ba6425999b651d6ef8bd29937
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/09/2019
ms.locfileid: "57693051"
---
# <a name="using-the-spb-io-request-interface"></a>SPB I/O 要求インターフェイスの使用

Windows 8 では、以降では、 [SPB フレームワーク拡張](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-framework-extension)(SpbCx) がサポートするシステム提供のコンポーネント、 [SPB の I/O 要求インターフェイス](https://docs.microsoft.com/previous-versions//hh698224(v=vs.85))。 SPB 周辺機器のデバイス ドライバーを I²C、SPI、およびその他に接続されているデバイスの I/O 要求を送信するこのインターフェイスを使用して[単純な周辺機器のバス](https://docs.microsoft.com/previous-versions//hh450903(v=vs.85))(SPBs)。 SpbCx によってさまざまな種類のバスの間で標準化された I/O 要求インターフェイスを使用できるようにするには、さまざまなハードウェア プラットフォームや別のハードウェアから SPB のコント ローラーの周辺機器のファミリをドライバーのサポートを提供するためのタスクを簡略化します。ベンダー。

次の条件が満たされた場合、SPB に接続されている周辺機器デバイスのハードウェア ベンダーは複数のバスの種類で動作する 1 つのデバイス ドライバーを開発できます。

- 周辺機器のデバイスはハードウェアと互換性のあるである必要がありますこのバスにします。
- ドライバーは、すべてのバスの種類の間で同じデバイス制御プロトコルを使用できます。

周辺機器のドライバーから bus 固有のコードを排除することでは、SPB フレームワークの拡張機能は、これらのドライバーの開発時間を短縮し、サポートされているバスの種類より一貫性のある動作ことができます。

SPBs に接続されている周辺機器がメモリ マップトでなく、これらのデバイス ドライバーは、これらのデバイスのハードウェア レジスタに直接アクセスできません。 代わりに、SPB の周辺機器のデバイス ドライバーは、逐次的にして、デバイスからデータを転送する、SPB コント ローラーに依存する必要があります。 このような転送を要求するには、ドライバーは、デバイスに、I/O 要求を送信する必要があります。 この I/O 要求は、SpbCx によって管理されているキューに送信されます。

ドライバーからの I/O 要求を処理する SPB コント ローラーのドライバーを使用する SpbCx と連携します。 SPB コント ローラーのハードウェア ベンダーには、コント ローラーのハードウェアに固有のタスクを実行する SPB コント ローラー ドライバーが用意されています。

ドライバーだけでは、SPB のコント ローラーの I/O 要求インターフェイスに、I/O 要求を送信できます。 アプリケーションでは、SPB コント ローラーに I/O 要求を直接送信することはできません。 代わりに、アプリケーションは、SPB 接続の周辺機器デバイスのドライバーに I/O 要求を送信し、SPB コント ローラーに、またはデバイスからデータを転送する必要がありますすべての I/O 要求を送信するドライバーに依存します。

ドライバー、ドライバーは、sp B に接続されている周辺機器に I/O 要求を送信できるようにを開きますが、デバイスへの接続を論理的に開く必要があります。 この接続を開くには、ドライバーは、プラグ アンド プレイ マネージャからのハードウェア リソースとして受信した接続 ID を使用します。 詳細については、次を参照してください。 [SPB の周辺機器の接続 Id](https://docs.microsoft.com/windows-hardware/drivers/spb/connection-ids-for-spb-connected-peripheral-devices)します。

SpbCx と SPB コント ローラーのドライバーは共同で読み取りを処理し、周辺機器の SPB 接続要求を記述します。 応答、 [ **IRP\_MJ\_読み取り**](https://docs.microsoft.com/previous-versions//ff546883(v=vs.85)) SPB コント ローラーは、指定したバイト数を周辺機器からドライバーによって提供されるバッファーに転送を要求します。 応答、 [ **IRP\_MJ\_書き込み**](https://docs.microsoft.com/en-us/previous-versions//ff546904(v=vs.85)) SPB コント ローラーは、ドライバーによって提供されるバッファーから指定したバイト数を周辺機器のデバイスに転送を要求します。

**IRP\_MJ\_読み取り**または**IRP\_MJ\_書き込み**0 バイトの転送を要求、SpbCx状態要求が完了すると\_成功の状態コードが操作を実行しません。

SpbCx と SPB コント ローラー ドライバーもこれらの SPB 固有 I/O 制御コード (Ioctl) を処理します。

- [**IOCTL\_SPB\_EXECUTE\_シーケンス**](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-ioctls#ioctl-spb-execute-sequence)
- [**IOCTL\_SPB\_ロック\_コント ローラー**](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-ioctls#ioctl-spb-lock-controller)
- [**IOCTL\_SPB\_UNLOCK\_コント ローラー**](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-ioctls#ioctl_spb_unlock_controller-control-code)

SPB 周辺のドライバーでは、これらの Ioctl を使用して、実行する*I/O 転送シーケンス*します。 I/O の転送シーケンスは、バスの転送 (読み取りし、書き込み操作) の順序付けされたセットがバスの単一のアトミック操作として実行します。 これらの Ioctl の詳細については、次を参照してください。 [I/O 転送シーケンス](https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences)します。

SPB コント ローラーの特定の SPB コント ローラーのドライバーには、ハードウェア固有機能を実行するカスタムの Ioctl をサポート可能性があります。 これらは、Ioctl SpbCx が処理しないこと、およびハードウェアに固有の操作を実行する必要がある SPB 周辺機器のデバイス ドライバーのため SPB コント ローラーのハードウェア ベンダーがサポートしています。 操作は実行されません SPB の周辺機器のデバイス ドライバーは、IOCTL SpbCx も SPB のコント ローラー ドライバーが認識するを送信する場合と、I/O 要求が完了状態のエラー状態の値を持つ\_いない\_サポートされています。

Sp B に接続されている周辺機器デバイスのドライバーは、いずれかでは通常、[ユーザー モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/overview-of-the-umdf)(UMDF) ドライバーまたは[カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/en-us/windows-hardware/drivers/wdf/index)(KMDF) ドライバー。 Sp B に接続されている周辺機器を読み取り、書き込み、または IOCTL 要求を送信する UMDF ドライバー メソッドを呼び出すよう[ **IWDFIoRequest::Send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)します。 KMDF ドライバーなどのメソッドの呼び出し[ **WdfIoTargetSendReadSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously)、 [ **WdfIoTargetSendWriteSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendwritesynchronously)、または[**WdfIoTargetSendIoctlSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously)します。

Sp B に接続されている周辺機器に I/O 要求を送信する方法を示すコード例では、これらのトピックを参照してください。

[ユーザー モード SPB の周辺機器のドライバーのハードウェア リソース](https://docs.microsoft.com/windows-hardware/drivers/spb/hardware-resources-for-user-mode-spb-peripheral-drivers)

[カーネル モード SPB の周辺機器のドライバーのハードウェア リソース](https://docs.microsoft.com/windows-hardware/drivers/spb/hardware-resources-for-kernel-mode-spb-peripheral-drivers)
