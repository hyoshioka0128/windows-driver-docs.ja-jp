---
title: SpbCx オブジェクト ハンドル
description: このトピックでは、SPB framework extension (SpbCx) ライブラリに対して定義されているオブジェクトハンドルについて説明します。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6cbae1f27683bffd5844fd52275f2487f4f62b68
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839623"
---
# <a name="spbcx-object-handles"></a>SpbCx オブジェクト ハンドル

このトピックでは、SPB framework extension (SpbCx) ライブラリに対して定義されているオブジェクトハンドルについて説明します。

さらに、SerCx2 DDI では、カーネルモードドライバーフレームワーク (KMDF) によって定義されている、WDFDEVICE と WDFDEVICE の2つのジェネリックオブジェクトハンドル型を使用します。
フレームワークのハンドル型の詳細については、「[フレームワークオブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/wdf/summary-of-framework-objects)」を参照してください。

このトピックでは、次のオブジェクトハンドルについて説明します。

* [SPBREQUEST オブジェクトハンドル](#spbrequest-object-handle)
* [SPBTARGET オブジェクトハンドル](#spbtarget-object-handle)

ヘッダー: Spbcx .h

## <a name="spbrequest-object-handle"></a>SPBREQUEST オブジェクトハンドル

**Spbrequest**オブジェクトハンドルは、バス上のターゲットデバイスに対して発行された i/o 要求を表します。

```cpp
DECLARE_HANDLE(SPBREQUEST)
```

**Spbrequest**オブジェクトクラスは、 **wdfrequest**オブジェクトクラスから派生します。このクラスは、i/o マネージャーによってディスパッチされる i/o 要求を表します。
したがって、 **Wdfrequestxxx**メソッドは、パラメーターとして**wdfrequest**ハンドル値を受け取るメソッドで、 **spbrequest**ハンドルの値を有効なパラメーター値として受け入れます。
これらのメソッドの詳細については、「[フレームワーク要求オブジェクト](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-request-objects)」を参照してください。

ただし、一部の SpbCx メソッドとコールバック関数では、パラメーターとして**Spbcx**ハンドルが必要です。
このようなパラメーターの場合、 **Spbrequest**ハンドルでもない**wdfrequest**ハンドルを置き換えると、エラーになります。

たとえば、 [Spbrequestgettransferparameters](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbrequestgettransferparameters)メソッドは、パラメーターとして**spbrequest**ハンドルを受け取ります。
このパラメーターにを指定するために、 **Spbrequest**ハンドルでもない**wdfrequest**ハンドルはエラーになります。
この要件の理由は、 [i/o 転送シーケンス](https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences)をサポートするために、sp 固有の追加の状態情報を**spbrequest**オブジェクトに格納する必要があるためです。
**Wdfrequest**基本オブジェクトクラスでは、このサポートは提供されません。

デバイスの初期化中に、SPB コントローラードライバーは、 [Spbrequest Setrequestattributes](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbcontrollersetrequestattributes)メソッドを呼び出すことによって、 **spbrequest**ハンドルに要求ごとのコンテキストを割り当てることができます。
  
## <a name="spbtarget-object-handle"></a>SPBTARGET オブジェクトハンドル

**Spbtarget**オブジェクトハンドルは、クライアント (周辺ドライバー) から、バス上のアドレス可能なポートまたは周辺機器への論理接続を識別します。

   ```cpp
   DECLARE_HANDLE(SPBTARGET)
   ```

I<sup>2</sup>C バスの場合、 **spbtarget**ハンドルは特定のデバイスアドレスに対応します。  
SPI バスの場合、 **Spbtarget**ハンドルはデバイスの選択行に対応します。

通常、 **spbtarget**オブジェクトは、対応する[Evtspbtargetconnect](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_target_disconnect)イベントコールバックの最後まで、 [Evtspbtargetconnect](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_target_connect)イベントコールバックの先頭から存在します。 ただし、SPB コントローラードライバーが**Spbtarget**オブジェクトに対して追加の参照を取得し、オブジェクトが予期せずに消えるのを防ぐために、 **spbtarget**オブジェクトの有効期間が2番目のコールバックを超えている可能性があります。ターゲットの i/o 要求の処理。

SPB コントローラードライバーは、SPB コントローラーデバイスに対してハードウェア固有のすべての操作を実行します。
クライアントがバス上のターゲットへの接続を開くために[IRP_MJ_CREATE](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)要求を送信すると、コントローラードライバーの i/o キューを管理する spb framework Extension (SpbCx) が、このドライバーのを呼び出して、この要求を SPB コントローラードライバーに渡します。[Evtspbtargetconnect](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_target_connect)コールバック関数。
この関数の_ターゲット_パラメーターは、 **spbtarget**ハンドルです。
関数は、このハンドルを使用して、PnP マネージャーから接続固有のリソース情報 (デバイスアドレスなど) を取得できます。
クライアントが[IRP_MJ_CLOSE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)要求を送信して接続を閉じると、この要求は SPB コントローラードライバーの[Evtspbtargetdisconnect](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_target_disconnect)コールバック関数に渡され、これらのリソースが解放されます。

### <a name="exclusive-mode-access"></a>排他モードアクセス

クライアントには、ターゲットデバイスにアクセスするための排他モードがあります。 一度に特定のターゲットデバイスに接続できるのは、1つのクライアントだけです。
SpbCx では、バス上のターゲットデバイスアドレスに対して**Spbcx**ハンドルが1つだけ存在することが保証されます。
この制限が必要な理由は、SpbCx では、2つ以上のクライアントからターゲットデバイスに送信される i/o 要求のインターリーブがサポートされていないためです。
ターゲットデバイスが複数のクライアントからの要求を受信できる必要がある場合、このデバイスには、要求された操作を適切にインターリーブできる MUX ドライバー (コントローラードライバーとは別のもの) が必要です。

### <a name="interoperability-with-kmdf"></a>KMDF との相互運用性

SpbCx で定義されている[SerCx2 Driver Support メソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)と[Spbcx イベントコールバック関数](https://docs.microsoft.com/previous-versions/hh450911(v=vs.85))は、 **spbcx**ハンドルを使用して、バス上のターゲットデバイスへの開いている接続を表します。
ただし、コントローラードライバーは、通常、ターゲットデバイスを指定するために、 **Spbtarget**ハンドルではなく WDFFILEOBJECT ハンドルを必要とする kmdf メソッドを呼び出す必要があります。

**Spbtarget**オブジェクトは、WDFFILEOBJECT オブジェクトに似ています。 ただし、 **Spbtarget**オブジェクトには、SPB 固有の追加情報が含まれています。
たとえば、 [IOCTL_SPB_EXECUTE_SEQUENCE](https://msdn.microsoft.com/library/windows/hardware/hh450857) i/o 制御要求の処理中に、ターゲットデバイスの**spbtarget**オブジェクトによって、 [i/o 転送シーケンス](https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences)の転送の状態が追跡されます。

ターゲットへの WDFFILEOBJECT ハンドルを取得するために、SPB コントローラードライバーは[Spbtargetgetfileobject](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbtargetgetfileobject)メソッドを呼び出します。
このメソッドは、入力パラメーターとして、開いているターゲットデバイスへの**Spbtarget**ハンドルを受け入れ、このターゲットに対応する WDFFILEOBJECT ハンドルを返します。

KMDF 規則に従って、SPB コントローラードライバーは、ターゲットデバイスの**Spbtarget**オブジェクトに独自のコンテキストをアタッチできます。また、このコンテキストには、関連付けられた[Evtcleanupcallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)および[evtcleanupcallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)コールバックを含めることができます。関数.
SPB コントローラードライバーは、コントローラードライバーおよびターゲットデバイスに固有の情報を追跡するために、このコンテキストを使用します。
さらに、このドライバーは、タイマー、Dpc、または必要に応じて i/o 要求や i/o キューなど、 **Spbtarget**オブジェクトの子オブジェクトを作成できます。

## <a name="related-topics"></a>関連トピック

[EvtCleanupCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)

[EvtDestroyCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)

[EvtSpbTargetConnect](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_target_connect)

[EvtSpbTargetDisconnect](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_target_disconnect)

[フレームワークの要求オブジェクト](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-request-objects)

[I/o 転送シーケンス](https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences)

[IOCTL_SPB_EXECUTE_SEQUENCE](https://msdn.microsoft.com/library/windows/hardware/hh450857)

[IRP_MJ_CLOSE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)

[IRP_MJ_CREATE](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)

[SerCx2 ドライバーのサポート方法](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[Spbコントローラーの Setrequestattributes](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbcontrollersetrequestattributes)

[SpbCx イベントコールバック関数](https://docs.microsoft.com/previous-versions/hh450911(v=vs.85))

[SpbRequestGetTransferParameters](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbrequestgettransferparameters)

[SpbTargetGetFileObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbtargetgetfileobject)

[フレームワークオブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/wdf/summary-of-framework-objects)
