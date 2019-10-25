---
title: UMDF ドライバーでのカーネルモード クライアントのサポート
description: このトピックでは、ユーザーモードドライバーフレームワーク (UMDF) ドライバーでカーネルモードクライアントがどのようにサポートされるかについて説明します。これは、UMDF バージョン2から始まります。
ms.assetid: 5C0180BF-F0C7-4225-8388-C3315C282516
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a4f309a5f9f1f902de04fa300538f01ac660921
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831763"
---
# <a name="supporting-kernel-mode-clients-in-umdf-drivers"></a>UMDF ドライバーでのカーネルモード クライアントのサポート


このトピックでは、ユーザーモードドライバーフレームワーク (UMDF) ドライバーで*カーネルモードクライアント*がどのようにサポートされるかについて説明します。これは、umdf バージョン2から始まります。

*カーネルモードクライアント*は、UMDF ドライバーに i/o 要求を送信するカーネルモードドライバーです。 カーネルモードドライバーが、同じデバイススタック内の UMDF ドライバーの上にあるか、または別のデバイススタックにある可能性があります。

カーネルモードドライバーは、ユーザーモードアプリケーションから受信した i/o 要求を転送したり、新しい i/o 要求を作成してユーザーモードドライバーに送信したりすることができます。

### <a href="" id="how-to-support-kernel-mode-clients-in-a-umdf-based-driver"></a>UMDF ドライバーでカーネルモードクライアントをサポートする方法

UMDF ドライバーによるカーネルモードクライアントのサポートを有効にするには、UMDF ドライバーの INF ファイルに、その INF *Ddinstall*に[Umdfkernel Modeclientpolicy](specifying-wdf-directives-in-inf-files.md)ディレクティブが含まれている必要があります。**WDF**セクション。

このフレームワークには、カーネルモードクライアントをサポートするドライバーに役立つ2つのメソッドが用意されています。 ドライバーは、 [**WdfRequestGetRequestorMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetrequestormode)メソッドを呼び出して、i/o 要求がカーネルモードとユーザーモードのどちらであるかを判断できます。 I/o 要求がユーザーモードから送信された場合、ドライバーは[**WdfRequestIsFromUserModeDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestisfromusermodedriver)を呼び出して、要求がアプリケーションまたは別のユーザーモードドライバーから送信されたかどうかを判断できます。

### <a name="restrictions-on-kernel-mode-drivers"></a>カーネルモードドライバーに関する制限事項

UMDF ドライバーは、カーネルモードドライバーが次の要件を満たしている場合にのみ、カーネルモードドライバーからの i/o 要求を処理できます。

-   カーネルモードドライバーは、i/o 要求を送信するときに、IRQL = パッシブ\_レベルで実行されている必要があります。

-   ドライバーによって**Umdffileobjectpolicy** INF ディレクティブが**AllowNullAndUnknownFileObjects**に設定されていない限り、カーネルモードドライバーに送信される各 i/o 要求には、関連付けられたファイルオブジェクトが必要です。 このフレームワークには、i/o マネージャーによってファイルオブジェクトが作成されたことがあらかじめ通知されている必要があります。 (この通知により、フレームワークはユーザーモードドライバーの[*EvtDeviceFileCreate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create)コールバック関数を呼び出しますが、そのコールバック関数は省略可能です)。

-   I/o 要求には、 [**IRP\_MJ\_内部\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)関数コードを含めることはできません。

-   ユーザーモードドライバーはポインターを逆参照できないため、i/o 要求のバッファーに追加情報へのポインターを含めることはできません。

-   I/o 要求に "両方" のバッファーアクセス方法を指定する[i/o 制御コード](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)が含まれている場合、カーネルモードドライバーは、i/o 要求を作成したアプリケーションのプロセスコンテキストで i/o 要求を送信する必要があります。 UMDF ドライバーで "どちらの" メソッドをサポートする方法の詳細については、「 [Umdf ドライバーでのバッファーアクセスメソッドの管理](managing-buffer-access-methods-in-umdf-drivers.md)」を参照してください。

-   UMDF ドライバーによって、i/o 要求の出力データがユーザーモードで変更される場合があります。 そのため、カーネルモードドライバーは、ユーザーモードドライバーから受け取った出力データを検証する必要があります。

-   通常、カーネルモードクライアントは、UMDF ドライバーが[**Wdfrequestcompletewithinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)に渡す*情報*の値を検証する必要があります。 クライアントが KMDF ドライバーの場合、 [**Wdfrequestgetreference params**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetcompletionparams)を呼び出して、この情報を IO\_状態\_ブロック構造で取得できます。

    通常、フレームワークでは、UMDF ドライバーが[**Wdfrequestcompletewithinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)に渡す情報値は検証されません。 (このパラメーターは、通常、転送されるバイト数を指定します。)フレームワークは、バッファー内の[i/o](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-wdf-drivers#direct)データアクセスメソッドに対してのみ、出力バッファーの情報値を検証します。 (たとえば、アクセスメソッドがバッファリングされている場合、フレームワークは、転送されたバイト数が読み取り操作の出力バッファーサイズを超えていないことを確認します)。

 

 





