---
title: SpbCx オブジェクト ハンドル
description: このトピックでは、SPB フレームワークの拡張機能 (SpbCx) ライブラリに対して定義されているオブジェクトのハンドルをについて説明します。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 69f089c704297894330dbdc82eecee2f0e99d577
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376896"
---
# <a name="spbcx-object-handles"></a>SpbCx オブジェクト ハンドル

このトピックでは、SPB フレームワークの拡張機能 (SpbCx) ライブラリに対して定義されているオブジェクトのハンドルをについて説明します。

さらに、SerCx2 DDI を使用して 2 つのジェネリック オブジェクト ハンドルの種類を WDFDEVICE と WDFREQUEST、カーネル モード ドライバー フレームワーク (KMDF) では定義されています。
フレームワークのハンドルの種類の詳細については、次を参照してください。 [Framework オブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/wdf/summary-of-framework-objects)します。

このトピックでは、次のオブジェクト ハンドルをについて説明します。

* [SPBREQUEST オブジェクト ハンドル](#spbrequest-object-handle)
* [SPBTARGET オブジェクト ハンドル](#spbtarget-object-handle)

ヘッダー:Spbcx.h

## <a name="spbrequest-object-handle"></a>SPBREQUEST オブジェクト ハンドル

**SPBREQUEST**オブジェクト ハンドルがバス上のターゲット デバイスに発行される I/O 要求を表します。

```cpp
DECLARE_HANDLE(SPBREQUEST)
```

**SPBREQUEST**から派生したオブジェクトのクラスは、 **WDFREQUEST**オブジェクト クラスは、I/O マネージャーによって送出される I/O 要求を表します。
したがって、 **WdfRequestXxx**取るメソッド**WDFREQUEST**値を処理するようにパラメーターを受け入れる**SPBREQUEST**有効なパラメーター値として値を処理します。
これらのメソッドの詳細については、次を参照してください。 [Framework 要求オブジェクト](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-request-objects)します。

ただし、一部の SpbCx メソッドとコールバック関数具体的には必要**SPBREQUEST**パラメーターとして処理します。
このようなパラメーターの場合の置換を**WDFREQUEST**ハンドルではない、 **SPBREQUEST**ハンドルは、エラーです。

たとえば、 [SpbRequestGetTransferParameters](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nf-spbcx-spbrequestgettransferparameters)メソッドは、 **SPBREQUEST**をパラメーターとして処理します。
このパラメーターを指定する、 **WDFREQUEST**ハンドルではない、 **SPBREQUEST**ハンドルがエラー。
この要件は、その理由は、 **SPBREQUEST**オブジェクトは、サポートするために、追加の SPB 固有の状態に関する情報を格納する必要があります[I/O 転送シーケンス](https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences)します。
**WDFREQUEST**ベース オブジェクトのクラスでは、このサポートは提供されません。

デバイスの初期化中に SPB コント ローラーのドライバーが要求ごとのコンテキストを割り当てることができます、 **SPBREQUEST**処理を呼び出すことによって、 [SpbControllerSetRequestAttributes](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nf-spbcx-spbcontrollersetrequestattributes)メソッド。
  
## <a name="spbtarget-object-handle"></a>SPBTARGET オブジェクト ハンドル

**SPBTARGET**オブジェクト ハンドルがクライアント (周辺ドライバー) から、アドレス指定可能なポートまたはバス上の周辺機器への論理接続を識別します。

   ```cpp
   DECLARE_HANDLE(SPBTARGET)
   ```

I の<sup>2</sup>C のバスを**SPBTARGET**ハンドルは、特定のデバイスのアドレスに対応します。  
SPI バスでは、 **SPBTARGET**ハンドルはデバイスの選択行に対応します。

通常、 **SPBTARGET**の先頭からオブジェクトが存在する、 [EvtSpbTargetConnect](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nc-spbcx-evt_spb_target_connect)末尾までの対応するイベントのコールバック[EvtSpbTargetDisconnect](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nc-spbcx-evt_spb_target_disconnect)イベントのコールバック。 ただしの有効期間、 **SPBTARGET** SPB コント ローラーのドライバーには、追加の参照の場合、2 番目のコールバックを超えるオブジェクトが長引く可能性がある、 **SPBTARGET**オブジェクトからオブジェクトを回避するには予期せず、ターゲットの I/O 要求の処理中に消失します。

SPB コント ローラーのドライバーは、SPB のコント ローラー デバイスのすべてのハードウェア固有の操作を実行します。
クライアントが送信すると、 [irp_mj_create 用](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)SPB フレームワーク拡張 (SpbCx) コント ローラーのドライバーの I/O キューを管理するには、バス上のターゲットへの接続を開く要求は、によって SPB コント ローラー ドライバーにこの要求を渡しますこのドライバーの呼び出す[EvtSpbTargetConnect](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nc-spbcx-evt_spb_target_connect)コールバック関数。
これは、_ターゲット_この関数のパラメーターは、 **SPBTARGET**を処理します。
関数は、PnP マネージャーから、接続固有のリソース情報 (たとえば、デバイスのアドレス) を取得するのにこのハンドルを使用できます。
クライアントが送信すると、[未完了](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)接続を閉じるには、SpbCx SPB コント ローラーのドライバーをこの要求を渡す[EvtSpbTargetDisconnect](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nc-spbcx-evt_spb_target_disconnect)コールバック関数は、これらのリリースリソース。

### <a name="exclusive-mode-access"></a>排他モードへのアクセス

クライアントでは、アクセス対象のデバイスを排他モードがあります。 1 つのみのクライアントには、特定のターゲット デバイスへの接続を一度にことができます。
SpbCx により、1 台のみと**SPBTARGET**バス上のターゲット デバイスのアドレスのハンドルが存在します。
SpbCx がターゲット デバイスに 2 つまたは複数のクライアントによって送信される I/O 要求のインターリーブをサポートしていないために、この制限する必要があります。
ターゲット デバイスは、複数のクライアントから要求を受信できる必要があります場合、このデバイスに MUX ドライバーが必要です: コント ローラーのドライバーとは別、要求された操作を正しくインターリーブすることができます。

### <a name="interoperability-with-kmdf"></a>KMDF との相互運用

[SerCx2 ドライバー サポート メソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)と[SpbCx イベント コールバック関数](https://docs.microsoft.com/previous-versions/hh450911(v=vs.85))定義されている SpbCx を使用して**SPBTARGET**を対象に開いている接続を表すハンドルバス上のデバイス。
ただし、コント ローラーのドライバーである必要がありますの代わりに、WDFFILEOBJECT ハンドルを必要とする KMDF メソッドを呼び出す通常**SPBTARGET**ハンドルは、ターゲット デバイスを指定します。

**SPBTARGET**オブジェクトは WDFFILEOBJECT オブジェクトに似ています。 ただし、 **SPBTARGET**オブジェクトには SPB 固有の追加情報が含まれています。
処理中など、 [IOCTL_SPB_EXECUTE_SEQUENCE](https://msdn.microsoft.com/library/windows/hardware/hh450857) I/O 制御の要求、 **SPBTARGET**オブジェクトのターゲット デバイスで、転送の状態を追跡する、 [I/O転送シーケンス](https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences)します。

ドライバーの呼び出しのターゲット、SPB コント ローラーに WDFFILEOBJECT ハンドルを取得する、 [SpbTargetGetFileObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nf-spbcx-spbtargetgetfileobject)メソッド。
このメソッドは、入力パラメーターとして、 **SPBTARGET**ハンドルを開く対象デバイスでは、このターゲットへの対応する WDFFILEOBJECT ハンドルを返す。

KMDF の規則に従って、SPB コント ローラーのドライバーは独自のコンテキストにアタッチできます、 **SPBTARGET**対象デバイス、およびこのコンテキストを含めることができますの関連付けられたオブジェクト[EvtCleanupCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)と[EvtDestroyCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)コールバック関数。
SPB コント ローラーのドライバーでは、このコンテキストを使用して、コント ローラーのドライバーとターゲット デバイスに固有の情報を追跡します。
さらに、このドライバーは子のオブジェクトを作成、 **SPBTARGET**タイマー、Dpc などのオブジェクトまたは、必要に応じて、I/O 要求の I/O キュー。

## <a name="related-topics"></a>関連トピック

[EvtCleanupCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup)

[EvtDestroyCallback](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/nc-wdfobject-evt_wdf_object_context_destroy)

[EvtSpbTargetConnect](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nc-spbcx-evt_spb_target_connect)

[EvtSpbTargetDisconnect](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nc-spbcx-evt_spb_target_disconnect)

[フレームワークの要求オブジェクト](https://docs.microsoft.com/windows-hardware/drivers/wdf/framework-request-objects)

[I/O 転送シーケンス](https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences)

[IOCTL_SPB_EXECUTE_SEQUENCE](https://msdn.microsoft.com/library/windows/hardware/hh450857)

[IRP_MJ_CLOSE](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close)

[IRP_MJ_CREATE](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)

[SerCx2 ドライバー サポート メソッド](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

[SpbControllerSetRequestAttributes](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nf-spbcx-spbcontrollersetrequestattributes)

[SpbCx イベント コールバック関数](https://docs.microsoft.com/previous-versions/hh450911(v=vs.85))

[SpbRequestGetTransferParameters](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nf-spbcx-spbrequestgettransferparameters)

[SpbTargetGetFileObject](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/spbcx/nf-spbcx-spbtargetgetfileobject)

[Framework のオブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/wdf/summary-of-framework-objects)
