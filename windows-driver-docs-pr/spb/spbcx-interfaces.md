---
title: SpbCx インターフェイス
description: SPB フレームワーク拡張機能 (SpbCx) は、2 つのインターフェイスです。
ms.assetid: 2449BB88-1912-43F9-97E6-B56158D92E55
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 774fa08bc5ad47325732488524df68ee5d2a06f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552104"
---
# <a name="spbcx-interfaces"></a>SpbCx インターフェイス


SPB フレームワーク拡張機能 (SpbCx) は、2 つのインターフェイスです。 最初は、SpbCx がバスに接続されている周辺機器に SPB コント ローラーのクライアント (周辺ドライバー) を送信する I/O の要求を受け入れる、I/O 要求インターフェイスです。 2 番目のインターフェイスは、SpbCx が SPB コント ローラーのドライバーとの通信に使用するデバイス ドライバー インターフェイス (DDI) です。

2 つの SpbCx インターフェイスは、Spbcx.h と Spb.h ヘッダー ファイルで定義されます。 Spbcx.h は、SpbCx と SPB のコント ローラー ドライバー間 DDI を定義します。 Spb.h は、SpbCx I/O 要求のインターフェイスでサポートされている SPB 固有 I/O 制御コードを定義します。

-   [SpbCx デバイス ドライバー インターフェイス (DDI)](#spbcx-device-driver-interface-ddi)
-   [SPB の I/O 要求インターフェイス](#spb-io-request-interface)

## <a name="spbcx-device-driver-interface-ddi"></a>SpbCx デバイス ドライバー インターフェイス (DDI)


SPB フレームワーク拡張機能モジュール、Spbcx.sys、およびイベント コールバック関数、SPB コント ローラー用ドライバーを実装するによって実装されるメソッドの SpbCx デバイス ドライバー インターフェイス (DDI) で構成されます。 SPB コント ローラーのドライバーは、SpbCx で DDI の初期化中にそのコールバック関数を登録します。

SpbCx、SPB コント ローラーのドライバーの呼び出しからサービスを要求する、 [SpbCx ドライバー サポート メソッド](https://msdn.microsoft.com/library/windows/hardware/hh450910)します。 たとえば、SPB コント ローラーのドライバーでは、SPB コント ローラー用ドライバーの構成オプションを設定するか、I/O 要求に関する追加情報を取得するメソッドが呼び出されます。

SpbCx 呼び出し (たとえば、クライアントからの I/O 要求の到着)、イベントの SPB コント ローラーのドライバーに通知する、[イベント コールバック関数](https://msdn.microsoft.com/library/windows/hardware/hh450911)SPB コント ローラーのドライバーによって実装されます。

SpbCx からのコールバック中には、SPB コント ローラーのドライバーのコードは、任意のスレッド コンテキストで実行されます。 SpbCx では、SPB コント ローラー ドライバーによって処理が必要な I/O 要求を受信した後は SpbCx 呼び出される前に、要求の前処理が必要な*EvtSpb*Xxx 関数は、要求された操作を実行します。 たとえば、ユーザー モード バッファーをコールバック関数を使用できるようにには、SpbCx が I/O 要求を生成したスレッドのコンテキストで実行する必要があります。 (、 [ *EvtIoInCallerContext* ](https://msdn.microsoft.com/library/windows/hardware/ff541764) SpbCx 要求プリプロセスを実行するには依存できませんある唯一のコールバック関数です)。

セットを登録する*EvtSpb*Xxx コールバック関数では、SPB コント ローラーのドライバーの呼び出し、 [ **SpbDeviceInitialize** ](https://msdn.microsoft.com/library/windows/hardware/hh450919)メソッド。 このドライバーは呼び出し、 [ **SpbControllerSetIoOtherCallback** ](https://msdn.microsoft.com/library/windows/hardware/hh450907)を登録するメソッド、 *EvtIoInCallerContext*コールバック関数。

SpbCx DDI SPB コント ローラーのデバイス オブジェクトを表す WDFDEVICE オブジェクトのハンドル型を使用します。 WDFDEVICE と他の KMDF オブジェクト ハンドル型を定義する Wdf.h ヘッダー ファイルが含まれます。 DDI が 2 つの SPB 固有オブジェクト ハンドル型を使用してさらに、 [ **SPBREQUEST** ](https://msdn.microsoft.com/library/windows/hardware/hh450925)と[ **SPBTARGET**](https://msdn.microsoft.com/library/windows/hardware/hh406201)に似ていますが、WDFREQUEST と WDFTARGET オブジェクトは、KMDF によって定義されている型を処理します。 SPBREQUEST ハンドルは、I/O 要求を表します。 SPBTARGET ハンドルでは、開かれたバス上の I/O 操作の周辺機器への論理接続を表します。

単純な周辺機器のバス I²C および SPI は通常、システムで使用されるチップ (SoC) モジュールでは、上でなど、どの低暗証番号 (pin) をカウントするは重要です。 SoC のモジュールは、低電力消費量を必要とするハンドヘルド デバイスでプロセッサとして頻繁に使用します。 SPB コント ローラーの回線は、比較的小さな電力を消費するため、SpbCx で電源管理のコードを比較的シンプルにすることができます。 既定では、SpbCx により、SPB コント ローラーのドライバーでコールバック メソッドをイベントのいずれかの呼び出す前に、SPB コント ローラーの電源が有効であります。 詳細については、の説明を参照して、 **PowerManaged**メンバー [ **SPB\_コント ローラー\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/hh406206)します。

必要に応じて、SPB コント ローラーのドライバーを明示的に電源オンとオフをコント ローラーを呼び出すことによって、 [ **WdfDeviceStopIdle** ](https://msdn.microsoft.com/library/windows/hardware/ff546921)と[ **WdfDeviceResumeIdle**](https://msdn.microsoft.com/library/windows/hardware/ff546838)メソッド。

SPB コント ローラーのドライバーは、カーネル モード ドライバーであるため、ファイル オブジェクトに、適切なセキュリティ記述子を割り当てる、必要があります。 この記述子には、ユーザー モードから SPB の周辺機器への不正アクセスができないようにします。 たとえば、サンプル SPB のコント ローラー ドライバー WDK に含まれてはセキュリティに適した一般的な SPB コント ローラーのドライバーの既定のレベルを提供します。 次の SDDL 文字列を使用します。

"D:P(A;;GA;;;SY)(A;;GA;;;BA)(A;;GA;;;UD)"

この SDDL 文字列がオペレーティング システム (およびそのユーザー モード コンポーネント) では、Administrators グループのメンバーへのアクセスを制限し、[ユーザー モード ドライバー フレームワーク](https://msdn.microsoft.com/library/windows/hardware/ff560442)(UMDF) ドライバー。 SDDL 文字列の詳細については、次を参照してください。[デバイス オブジェクトの SDDL](https://msdn.microsoft.com/library/windows/hardware/ff563667)します。

さらに、 [ *EvtSpbControllerIoOther* ](https://msdn.microsoft.com/library/windows/hardware/hh450805)関数は、ユーザー モードのクライアントから受信した、カスタム コントロールの I/O 要求のすべてのパラメーターを検証する必要があります。 他のすべての*EvtSpb*Xxx 関数、SpbCx パラメーターを検証、ユーザー モードのクライアントからの I/O 要求で SPB コント ローラーのドライバーにこれらのパラメーターが渡される前にします。 デバイスのセキュリティの詳細については、次を参照してください。[デバイス オブジェクトのセキュリティで保護する](https://msdn.microsoft.com/library/windows/hardware/ff563688)します。

すべてのメソッドと状態コードを返す SpbCx DDI でコールバック関数は、NTSTATUS 値を返します。 この DDI のドライバー サポート メソッドは、KMDF インターフェイスでは、一般的な規則に従うし、SpbCx によって使用されているすべてのオブジェクトが KMDF オブジェクトの通常の規則に従ってください。 詳細については、次を参照してください。 [Framework オブジェクトの概要](https://msdn.microsoft.com/library/windows/hardware/ff544249)します。

## <a name="spb-io-request-interface"></a>SPB の I/O 要求インターフェイス


I/O 要求インターフェイスを実装するには、SpbCx は SPB コント ローラーの I/O キューを管理し、SPB コント ローラーのクライアントからの I/O 要求をこのキューを監視します。 これらのクライアントは、sp B に接続されている周辺機器のユーザー モードとカーネル モードのドライバーです。 アプリケーションは、SPB の I/O 要求インターフェイスを通じて SPB 接続の周辺機器と直接通信できません。

SpbCx は、可能性があります、これらの I/O 要求の一部のすべての処理を実行し、要求が SPB コント ローラーのドライバーに渡される前に、他の要求の前処理を実行します。 SPB コント ローラーのドライバーは SpbCx から受信した要求を完了します。

クライアントでは、読み取りを送信でき、SPB に接続されている周辺機器に要求を記述することができます。 応答、 [ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff546883) SPB コント ローラーは、指定したバイト数を周辺機器のデバイスからクライアント バッファーに転送を要求します。 応答、 [ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff546904)要求、SPB コント ローラーは、周辺機器のデバイスにクライアント バッファーから指定したバイト数を転送します。

単純な読み取りおよび書き込み操作では、に加えては、SpbCx I/O 要求インターフェイスは、I/O 転送シーケンスは、1 つ以上単純な転送 (は、読み取りし、書き込み) にバスの単一のアトミック操作の結合をサポートします。 この操作中に、バスは、ターゲットの周辺機器と転送専用に使用し、バス上の他のターゲットのアクセスが一時的にロックアウト、操作が完了するまでします。 SpbCx をサポートしています、 [ **IOCTL\_SPB\_EXECUTE\_シーケンス**](https://msdn.microsoft.com/library/windows/hardware/hh450857) I/O 制御コードは、クライアントを使用して、の間に固定長の転送の順序を指定します。1 つの I/O 要求内のターゲット デバイス。 この I/O 制御要求には、一連のパフォーマンスを向上させるためにバスの転送を最適化するために、コント ローラー ドライバーができます。

SpbCx I/O 要求インターフェイスをサポートしています、 [ **IOCTL\_SPB\_ロック\_コント ローラー** ](https://msdn.microsoft.com/library/windows/hardware/hh450858)と[ **IOCTL\_SPB\_UNLOCK\_コント ローラー** ](https://msdn.microsoft.com/library/windows/hardware/hh450859) I/O 制御コード、ロックおよび SPB コント ローラーのロックを解除します。 これらのロックおよびロック解除要求 I/O の転送シーケンスを実行するクライアントを別の方法を提供します。 ここでは、各読み取りまたはシーケンスの書き込み操作は個別の読み取りまたは書き込み要求で指定します。 クライアントは、ロックされているコント ローラーには、他のクライアントは、バス上のデバイスにアクセスできません。 ロックを保持して、クライアントは、バス上の I/O 操作を実行できます。 このため、クライアントは短い期間にのみ、コント ローラーをロックする必要があります。 クライアントには、転送シーケンスの完了後にロックされているコント ローラーしないままにしてください。 詳細については、次を参照してください。 [I/O 転送シーケンス](https://msdn.microsoft.com/library/windows/hardware/hh450890)します。

SpbCx でサポートされている I/O 制御 (IOCTL) のコードだけでなく SPB コント ローラーのドライバーは、カスタムの Ioctl をサポートできます。 クライアントは、バス上のターゲット デバイスを表すファイル オブジェクトに IOCTL 要求を送信することができ、SpbCx によって管理されている I/O 要求キュー内でこれらの要求が到着します。 サポートされていない IOCTL コードが要求を受け取った SpbCx SpbCx は要求のすべての処理を実行するコント ローラー ドライバーに直接要求を渡します。

SpbCx I/O のカーネル モードのクライアント要求インターフェイスは、いずれかパッシブの割り込み要求レベル (IRQL) I/O 要求を送信できる\_レベルまたはディスパッチ\_レベル。 ユーザー モードのクライアントはパッシブでのみ I/O 要求を送信できる\_レベル。 パッシブで発生することが I/O 完了\_レベルまたはディスパッチ\_レベル。 すべての I/O 要求が状態を返せる\_保留します。

 

 




