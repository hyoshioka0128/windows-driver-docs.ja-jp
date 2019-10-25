---
title: SpbCx インターフェイス
description: SPB framework extension (SpbCx) には、2つのインターフェイスがあります。
ms.assetid: 2449BB88-1912-43F9-97E6-B56158D92E55
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 857ed210558c1da8bc1b20879b43aa1f2c5139ca
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839625"
---
# <a name="spbcx-interfaces"></a>SpbCx インターフェイス


SPB framework extension (SpbCx) には、2つのインターフェイスがあります。 1つは、SPB コントローラーのクライアント (周辺ドライバー) がバスに接続されている周辺機器に送信する i/o 要求を SpbCx が受け入れる i/o 要求インターフェイスです。 2番目のインターフェイスは、SpbCx が SPB コントローラードライバーと通信するデバイスドライバーインターフェイス (DDI) です。

2つの SpbCx インターフェイスは、Spbcx および Spb .h ヘッダーファイルで定義されています。 Spbcx は、SpbCx と SPB コントローラードライバーの間の DDI を定義します。 Spb は、SpbCx i/o 要求インターフェイスによってサポートされる SPB 固有の i/o 制御コードを定義します。

-   [SpbCx Device Driver Interface (DDI)](#spbcx-device-driver-interface-ddi)
-   [SPB i/o 要求インターフェイス](#spb-io-request-interface)

## <a name="spbcx-device-driver-interface-ddi"></a>SpbCx Device Driver Interface (DDI)


SpbCx device driver interface (DDI) は、spb コントローラードライバーが実装する、SPB フレームワーク拡張モジュール、Spbcx .sys、およびイベントコールバック関数によって実装されるメソッドで構成されます。 SPB コントローラードライバーは、DDI の初期化中に、そのコールバック関数を SpbCx に登録します。

SpbCx からサービスを要求するために、SPB コントローラードライバーは[spbcx ドライバーのサポートメソッド](https://docs.microsoft.com/previous-versions/hh450910(v=vs.85))を呼び出します。 たとえば、SPB コントローラードライバーは、SPB コントローラーのドライバー構成オプションを設定したり、i/o 要求に関する追加情報を取得したりするために、これらのメソッドを呼び出します。

クライアントからの i/o 要求の到着など、イベントの SPB コントローラードライバーに通知するために、SpbCx は SPB コントローラードライバーによって実装される[イベントコールバック関数](https://docs.microsoft.com/previous-versions/hh450911(v=vs.85))を呼び出します。

SpbCx からのコールバック中に、SPB コントローラードライバーコードは任意のスレッドコンテキストで実行されます。 SPB コントローラードライバーによる処理を必要とする i/o 要求を受信した後、spbcx は、要求された操作を実行するために*Evtspb*Xxx 関数を呼び出す前に、要求の必須のプリプロセスを実行します。 たとえば、コールバック関数でユーザーモードバッファーを使用できるようにするには、i/o 要求を発信したスレッドのコンテキストで SpbCx を実行しなければならないことがあります。 ( [*Evtioincallercontext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)関数は、SpbCx を使用して要求を前処理することができない唯一のコールバック関数です)。

*Evtspb*Xxx コールバック関数のセットを登録するために、SPB コントローラードライバーは[**Spbdeviceinitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbdeviceinitialize)メソッドを呼び出します。 このドライバーは、 [**Spbコントローラー Setioofunctions コール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nf-spbcx-spbcontrollersetioothercallback)バックメソッドを呼び出して、 *Evtioincallercontext*コールバック関数を登録します。

SpbCx DDI は、WDFDEVICE オブジェクトハンドル型を使用して、SPB コントローラーのデバイスオブジェクトを表します。 Wdf ヘッダーファイルをインクルードして、WDFDEVICE およびその他の KMDF オブジェクトハンドル型を定義します。 さらに、DDI は、SP 固有の2つのオブジェクトハンドル型である[**Spbrequest**](https://docs.microsoft.com/windows-hardware/drivers/spb/spbcx-object-handles)と[**spbrequest**](https://docs.microsoft.com/windows-hardware/drivers/spb/spbcx-object-handles)を使用します。これは、kmdf によって定義される WDFREQUEST および wdfrequest オブジェクトハンドル型に似ています。 SPBREQUEST ハンドルは、i/o 要求を表します。 SPBTARGET ハンドルは、i/o 操作用に開かれているバス上の周辺機器への論理接続を表します。

I ² C や SPI などの単純な周辺機器は、通常、システムによって使用されます。これは、低 pin のカウントが重要なチップ (SoC) モジュールで使用されます。 SoC モジュールは、電力消費量が少ないハンドヘルドデバイスのプロセッサとして頻繁に使用されます。 SPB コントローラー回線の電力消費は比較的少ないため、SpbCx の電源管理コードは比較的単純なものにすることができます。 既定では、SpbCx は、spb コントローラードライバー内のイベントコールバックメソッドを呼び出す前に、SPB コントローラーの電源がオンになっていることを保証します。 詳細については、 [**SPB\_CONTROLLER\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/ns-spbcx-_spb_controller_config)の**powermanaged**メンバーの説明を参照してください。

必要に応じて、SPB コントローラードライバーは、 [**Wdfdevicestopidle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicestopidle)メソッドと[**WdfDeviceResumeIdle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceresumeidle)メソッドを呼び出すことによって、コントローラーの電源を明示的にオンおよびオフにすることができます。

SPB コントローラードライバーはカーネルモードドライバーであるため、適切なセキュリティ記述子をそのファイルオブジェクトに割り当てる必要があります。 この記述子は、SPB 上の周辺機器へのユーザーモードからの不正アクセスを防止します。 たとえば、WDK のサンプルの SPB コントローラードライバーは、次の SDDL 文字列を使用します。これは、一般的な SPB コントローラードライバーに適した既定のセキュリティレベルを提供します。

"D: P (A;;GA、;、SY) (A;;GA、;、BA) (A;;GA、;、UD) "

この SDDL 文字列を使用すると、オペレーティングシステム (およびそのユーザーモードコンポーネント)、Administrators グループのメンバー、および[ユーザーモードドライバーフレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/overview-of-the-umdf)(UMDF) ドライバーへのアクセスが制限されます。 SDDL 文字列の詳細については、「[デバイスオブジェクトの sddl](https://docs.microsoft.com/windows-hardware/drivers/kernel/sddl-for-device-objects)」を参照してください。

さらに、 [*EvtSpbControllerIoOther*](https://docs.microsoft.com/windows-hardware/drivers/ddi/spbcx/nc-spbcx-evt_spb_controller_other)関数は、ユーザーモードクライアントから受信するカスタム i/o 制御要求のすべてのパラメーターを検証する必要があります。 その他のすべての*Evtspb*Xxx 関数では、これらのパラメーターが SPB コントローラードライバーに渡される前に、SpbCx がユーザーモードクライアントからの i/o 要求のパラメーターを検証します。 デバイスのセキュリティの詳細については、「[デバイスオブジェクト](https://docs.microsoft.com/windows-hardware/drivers/kernel/securing-device-objects)のセキュリティ保護」を参照してください。

ステータスコードを返す SpbCx DDI 内のすべてのメソッドとコールバック関数は、NTSTATUS 値を返します。 この DDI のドライバーサポートメソッドは、KMDF インターフェイスの通常の規則に従います。また、SpbCx で使用されるすべてのオブジェクトは、KMDF オブジェクトの通常の規則に従います。 詳細については、「[フレームワークオブジェクトの概要](https://docs.microsoft.com/windows-hardware/drivers/wdf/introduction-to-framework-objects)」を参照してください。

## <a name="spb-io-request-interface"></a>SPB i/o 要求インターフェイス


I/o 要求インターフェイスを実装するために、SpbCx は SPB コントローラーの i/o キューを管理し、このキューで SPB コントローラーのクライアントからの i/o 要求を監視します。 これらのクライアントは、SPB に接続されている周辺機器のユーザーモードとカーネルモードのドライバーです。 アプリケーションは、spb i/o 要求インターフェイスを介して、SPB に接続されている周辺機器と直接通信することはできません。

SpbCx は、これらの i/o 要求の一部に対してすべての処理を実行し、要求が SPB コントローラードライバーに渡される前に他の要求の前処理を行う場合があります。 SPB コントローラードライバーは、SpbCx から受信した要求を完了する役割を担います。

クライアントは、SPB に接続されている周辺機器に読み取り/書き込み要求を送信できます。 SP 1 コントローラーは、 [**IRP\_MJ\_読み取り**](https://docs.microsoft.com/previous-versions/ff546883(v=vs.85))要求に応答して、指定されたバイト数を周辺機器からクライアントバッファーに転送します。 SP 1 コントローラーは、 [**IRP\_MJ\_書き込み**](https://docs.microsoft.com/previous-versions/ff546904(v=vs.85))要求に応答して、指定されたバイト数をクライアントバッファーから周辺機器に転送します。

単純な読み取りおよび書き込み操作に加え、SpbCx i/o 要求インターフェイスは、1つ以上の単純な転送 (つまり、読み取りと書き込み) を1つのアトミックバス操作に結合する i/o 転送シーケンスをサポートしています。 この操作では、バスはターゲット周辺機器との間の転送にのみ使用され、バス上の他のターゲットへのアクセスは、操作が完了するまで一時的にロックアウトされます。 SpbCx では、\_シーケンス I/o 制御コードを[**実行\_IOCTL\_SPB**](https://msdn.microsoft.com/library/windows/hardware/hh450857)がサポートされています。これは、1つの i/o 要求で、ターゲットデバイスとの間で固定長転送シーケンスを指定するためにクライアントが使用します。 この i/o 制御要求により、コントローラードライバーは、パフォーマンスを向上させるためにバス転送のシーケンスを最適化できます。

SpbCx i/o 要求インターフェイスでは、 [**ioctl\_spb\_ロック\_コントローラー**](https://msdn.microsoft.com/library/windows/hardware/hh450858)と[**ioctl\_SPB\_ロック解除\_コントローラー**](https://msdn.microsoft.com/library/windows/hardware/hh450859) i/o 制御コードをロックして、spb コントローラーをロックおよびロック解除することがサポートされています。 これらのロック要求とロック解除要求は、クライアントが i/o 転送シーケンスを実行するための別の方法を提供します。 この場合、シーケンス内の各読み取り操作または書き込み操作は、個別の読み取り要求または書き込み要求によって指定されます。 クライアントにコントローラーがロックされている間、他のクライアントはバス上のデバイスにアクセスできません。 バスで i/o 操作を実行できるのは、ロックを保持しているクライアントだけです。 このため、クライアントは、短い期間だけコントローラーをロックする必要があります。 クライアントは、転送シーケンスの完了後にコントローラーをロックしたままにしないでください。 詳細については、「 [I/o 転送シーケンス](https://docs.microsoft.com/windows-hardware/drivers/spb/i-o-transfer-sequences)」を参照してください。

SpbCx でサポートされている i/o 制御 (IOCTL) コードに加えて、SPB コントローラードライバーはカスタム Ioctl をサポートできます。 クライアントは、バス上のターゲットデバイスを表すファイルオブジェクトに IOCTL 要求を送信できます。これらの要求は、SpbCx で管理されている i/o 要求キューに到着します。 サポートされていない IOCTL コードを含む要求を SpbCx が受信した場合、SpbCx は要求をコントローラードライバーに直接渡します。これにより、要求のすべての処理が実行されます。

SpbCx i/o 要求インターフェイスのカーネルモードクライアントは、パッシブ\_レベルまたはディスパッチ\_レベルの割り込み要求レベル (IRQL) で i/o 要求を送信できます。 ユーザーモードのクライアントは、パッシブ\_レベルでのみ i/o 要求を送信できます。 I/o の完了は、パッシブ\_レベルまたはディスパッチ\_レベルで発生する可能性があります。 すべての i/o 要求は、状態\_保留中として返すことができます。

 

 




