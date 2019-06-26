---
title: UMDF ドライバーでのカーネルモード クライアントのサポート
description: このトピックでは、ユーザー モード ドライバー フレームワーク (UMDF) ドライバーが UMDF バージョン 2 以降、カーネル モードのクライアントをサポートする方法について説明します。
ms.assetid: 5C0180BF-F0C7-4225-8388-C3315C282516
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f07439199ff0d88df69d6a6736181baaa1c1597
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368083"
---
# <a name="supporting-kernel-mode-clients-in-umdf-drivers"></a>UMDF ドライバーでのカーネルモード クライアントのサポート


このトピックでは、ユーザー モード ドライバー フレームワーク (UMDF) ドライバーをサポートする方法について説明します*カーネル モードのクライアント*、UMDF バージョン 2 で開始します。

A*カーネル モードのクライアント*は UMDF ドライバーに I/O 要求を送信するカーネル モード ドライバーです。 上で、同じデバイス スタック、UMDF ドライバー、カーネル モード ドライバーがあるか、別のデバイス スタックにする必要があります。

カーネル モード ドライバーことができます、ユーザー モード アプリケーションから受信した I/O 要求を転送または新しい I/O 要求を作成でき、ユーザー モード ドライバーに送信できます。

### <a href="" id="how-to-support-kernel-mode-clients-in-a-umdf-based-driver"></a>UMDF ドライバーでカーネル モードのクライアントをサポートする方法

カーネル モードのクライアントの UMDF ドライバーのサポートを有効にする UMDF ドライバーの INF ファイルを含める必要があります、 [UmdfKernelModeClientPolicy](specifying-wdf-directives-in-inf-files.md)ディレクティブ、INF で*DDInstall*.**WDF**セクション。

フレームワークは、カーネル モードのクライアントをサポートするドライバーに役立つ 2 つのメソッドを提供します。 ドライバーを呼び出すことができます、 [ **WdfRequestGetRequestorMode** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetrequestormode) I/O 要求がカーネル モードまたはユーザー モードからのものかどうかを判断するメソッド。 ドライバーを呼び出すことができる場合、I/O 要求は、ユーザー モードから付属していた、 [ **WdfRequestIsFromUserModeDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestisfromusermodedriver)を要求がアプリケーションまたは別のユーザー モード ドライバーからのものかどうかを判断します。

### <a name="restrictions-on-kernel-mode-drivers"></a>カーネル モード ドライバーに関する制限事項

カーネル モード ドライバーは、次の要件を満たす場合にのみ、UMDF ドライバーでは、カーネル モード ドライバーからの I/O 要求を処理できます。

-   IRQL では、カーネル モード ドライバーを実行する必要があります = パッシブ\_レベルの I/O 要求を送信するとき。

-   ドライバーが設定されていない限り、 **UmdfFileObjectPolicy** INF ディレクティブを**AllowNullAndUnknownFileObjects**、カーネル モード ドライバーがユーザー モード ドライバーに送信する I/O 要求ごとに、関連付けられている必要がありますファイル オブジェクト。 フレームワークする必要があります前に通知されました I/O マネージャーが、ファイル オブジェクトを作成します。 (このような通知が配信を呼び出して、ユーザー モード ドライバーのフレームワークが[ *EvtDeviceFileCreate* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)コールバック関数がコールバック関数はオプションです)。

-   I/O 要求を含めることはできません、 [ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)関数コード。

-   ユーザー モード ドライバーには、ポインターが逆参照できませんので、I/O 要求のバッファーは追加の情報へのポインターを含めないでください。

-   I/O 要求が含まれている場合、 [I/O 制御コード](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)「も」バッファーへのアクセス方法を指定する、カーネル モード ドライバーは、I/O 要求を作成したアプリケーションのプロセスのコンテキストで I/O 要求を送信する必要があります。 UMDF ドライバーで「も」メソッドをサポートする方法の詳細については、次を参照してください。 [UMDF ドライバーを使用したバッファー アクセス方法を管理する](managing-buffer-access-methods-in-umdf-drivers.md)します。

-   UMDF ドライバーでは、ユーザー モードでの I/O 要求の出力データを変更可能性があります。 そのため、カーネル モード ドライバーでは、ユーザー モード ドライバーから受信したすべての出力データを検証する必要があります。

-   カーネル モード クライアントは通常を検証する必要があります、*情報*UMDF ドライバーに渡す値[ **WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)します。 呼び出すことができます、クライアントが KMDF ドライバーの場合は、 [ **WdfRequestGetCompletionParams** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetcompletionparams) IO では、この情報を取得する\_状態\_ブロック構造体。

    通常、フレームワークが UMDF ドライバーからに渡される情報の値を検証しません[ **WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)します。 (このパラメーターは、通常の数を指定転送されたバイト。)フレームワークは、出力バッファーとのみの情報値を検証、 [I/O バッファーに格納](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers#direct)メソッドがデータにアクセスします。 (たとえば、フレームワークを確認転送されたバイト数が、読み取り操作の出力バッファーのサイズを超えていないこと、アクセスする方法がバッファリングされる場合 I/O)。

 

 





