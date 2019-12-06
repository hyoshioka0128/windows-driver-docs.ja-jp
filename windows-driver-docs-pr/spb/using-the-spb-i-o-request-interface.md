---
title: SPB I/O 要求インターフェイスの使用
description: Windows 8 以降では、SPB フレームワーク拡張 (SpbCx) は、SPB i/o 要求インターフェイスをサポートするシステム提供のコンポーネントです。
ms.assetid: 0A752413-FA0B-4C26-BF6D-19033E07095E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd69866107e540e7267ba65375d2f20e3bc8a5b9
ms.sourcegitcommit: ba3199328ea5d80119eafc399dc989e11e7ae1d6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2019
ms.locfileid: "74862886"
---
# <a name="using-the-spb-io-request-interface"></a>SPB I/O 要求インターフェイスの使用

Windows 8 以降では、 [spb フレームワーク拡張](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-framework-extension)(spbcx) は、 [spb i/o 要求インターフェイス](https://docs.microsoft.com/previous-versions/hh698224(v=vs.85))をサポートするシステム提供のコンポーネントです。 SPB 周辺機器ドライバーは、このインターフェイスを使用して、i ² C、SPI、およびその他の[単純な周辺機器](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))(spbs) に接続されているデバイスに i/o 要求を送信します。 さまざまな種類のバスで標準化された i/o 要求インターフェイスを使用できるようにすることで、SpbCx は、さまざまなハードウェアプラットフォームや、異なるハードウェアベンダーの SPB コントローラーを介して、周辺機器のファミリにドライバーサポートを提供するタスクを簡略化します。

次の条件が満たされている場合は、SPB に接続されている周辺機器のハードウェアベンダーが、複数の種類のバスで動作する1つのデバイスドライバーを開発できます。

- 周辺機器は、これらのバスとハードウェアとの互換性がある必要があります。
- ドライバーは、これらのすべての種類のバスで同じデバイス制御プロトコルを使用できます。

周辺機器ドライバーからバス固有のコードを排除することにより、SPB フレームワーク拡張機能によってこれらのドライバーの開発時間が短縮され、サポートされるバスの種類全体でより一貫した動作が確保されます。

Spa に接続されている周辺機器はメモリにマップされていません。これらのデバイスのドライバーは、これらのデバイスのハードウェアレジスタに直接アクセスすることはできません。 代わりに、SPB 周辺機器ドライバーは、デバイスとの間でデータを直列に転送するために、SPB コントローラーに依存している必要があります。 このような転送を要求するには、ドライバーはデバイスに i/o 要求を送信する必要があります。 この i/o 要求は、SpbCx によって管理されるキューに送信されます。

Spbcx と連携し、ドライバーからの i/o 要求を処理するために、SPB コントローラードライバーを使用して動作します。 SPB コントローラーのハードウェアベンダは、コントローラーハードウェアに固有のタスクを実行するために SPB コントローラードライバーを提供します。

ドライバーのみが、SPB コントローラーの i/o 要求インターフェイスに i/o 要求を送信できます。 アプリケーションは、SPB コントローラーに i/o 要求を直接送信することはできません。 代わりに、アプリケーションは、SPB に接続されている周辺機器のドライバーに i/o 要求を送信し、そのドライバーを使用して、デバイスとの間でデータを転送するために必要となる可能性のある i/o 要求を、そのドライバーに任せることができます。

ドライバーは、SPB に接続されている周辺機器に i/o 要求を送信する前に、デバイスへの論理接続を開く必要があります。 この接続を開くために、ドライバーは、プラグアンドプレイ manager からハードウェアリソースとして受け取った接続 ID を使用します。 詳細については、「 [SPB 周辺機器の接続 id](https://docs.microsoft.com/windows-hardware/drivers/spb/connection-ids-for-spb-connected-peripheral-devices)」を参照してください。

SpbCx と SPB コントローラードライバーは、SPB 接続周辺機器の読み取り要求と書き込み要求を共同で処理します。 SP は、 [**IRP\_MJ\_読み取り**](https://docs.microsoft.com/previous-versions/ff546883(v=vs.85))要求に応答して、指定されたバイト数を周辺機器からドライバーが提供するバッファーに転送します。 SP 1 コントローラーは、 [**IRP\_MJ\_書き込み**](https://docs.microsoft.com/previous-versions//ff546904(v=vs.85))要求に応答して、指定されたバイト数をドライバーが提供するバッファーから周辺機器に転送します。

**Irp\_MJ\_READ**または**IRP\_\_MJ**の場合、0バイトを転送する書き込み要求では、spbcx はステータス\_成功状態コードで要求を完了しますが、操作は実行されません。

SpbCx と SPB コントローラードライバーは、これらの SPB 固有の i/o 制御コード (Ioctl) も処理します。

- [ **\_シーケンスを実行\_IOCTL\_SPB**](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-ioctls#ioctl-spb-execute-sequence)
- [**IOCTL\_SPB\_ロック\_コントローラー**](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-ioctls#ioctl-spb-lock-controller)
- [**IOCTL\_SPB\_\_コントローラーのロックを解除します**](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-ioctls#ioctl_spb_unlock_controller-control-code)

SPB 周辺ドライバーは、これらの Ioctl を使用して*i/o 転送シーケンス*を実行します。 I/o 転送シーケンスは、単一のアトミックバス操作として実行される、順序付けされたバス転送 (読み取りおよび書き込み操作) のセットです。 これらの Ioctl の詳細については、「 [I/o 転送シーケンス](https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences)」を参照してください。

特定の SPB コントローラーの SPB コントローラードライバーは、ハードウェア固有の機能を実行するカスタム Ioctl をサポートする場合があります。 これらは、SpbCx が処理しない Ioctl であり、SPB コントローラーのハードウェアベンダーが、ハードウェア固有の操作を実行する必要がある SPB 周辺デバイスドライバーの利点をサポートしています。 SPB 周辺機器ドライバーが、SpbCx でも SPB コントローラードライバーも認識しない IOCTL を送信した場合、操作は実行されず、i/o 要求はエラー状態の値\_[サポートされていませ\_ん] の状態で完了します。

SPB に接続されている周辺機器のドライバーは、通常、[ユーザーモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/overview-of-the-umdf)(UMDF) ドライバーまたは[カーネルモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/index)(kmdf) ドライバーのいずれかです。 SPB 接続の周辺機器に読み取り、書き込み、または IOCTL 要求を送信するために、UMDF ドライバーは[**IWDFIoRequest:: send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)などのメソッドを呼び出します。 KMDF ドライバーは、 [**Wdfiotargetsendreadsynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendreadsynchronously)、 [**WdfIoTargetSendWriteSynchronously**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendwritesynchronously)、または[**Wdfiotargetsendioctlなど**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendioctlsynchronously)のメソッドを同期的に呼び出します。

SPB に接続されている周辺機器に i/o 要求を送信する方法を示すコード例については、次のトピックを参照してください。

[ユーザーモード SPB 周辺機器ドライバーのハードウェアリソース](https://docs.microsoft.com/windows-hardware/drivers/spb/hardware-resources-for-user-mode-spb-peripheral-drivers)

[カーネルモード SPB 周辺機器ドライバーのハードウェアリソース](https://docs.microsoft.com/windows-hardware/drivers/spb/hardware-resources-for-kernel-mode-spb-peripheral-drivers)
