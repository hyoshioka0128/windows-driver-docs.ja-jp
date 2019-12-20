---
title: UMDF 1.x ドライバーでのカーネルモード クライアントのサポート
description: UMDF 1.x ドライバーでのカーネルモード クライアントのサポート
ms.assetid: 933dc761-2616-4bee-8357-dbb6644596c2
keywords:
- カーネルモードクライアント WDK UMDF
- UMDF ドライバー WDK UMDF、カーネルモードクライアント
- ユーザーモードドライバー WDK UMDF、カーネルモードクライアント
- UMDF WDK、カーネルモードクライアント
- ユーザーモードドライバーフレームワーク WDK、カーネルモードクライアント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 590fbd04a9ec26df8dab1a1992acdac1df3bc90d
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210820"
---
# <a name="supporting-kernel-mode-clients-in-umdf-1x-drivers"></a>UMDF 1.x ドライバーでのカーネルモード クライアントのサポート

[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

>[!WARNING]
>「 [UMDF 2.x でのカーネルモードクライアントのサポート](supporting-kernel-mode-clients-in-umdf-drivers.md)」も参照してください。

UMDF バージョン1.9 以降では、UMDF ドライバーで*カーネルモードクライアント*をサポートできるようになります。 カーネルモードクライアントは、次のいずれかになります。

-   デバイスのドライバースタック内の UMDF ドライバーの上に存在するカーネルモードドライバー。

-   1つのデバイスをサポートする1つのデバイススタックのカーネルモードドライバーがあり、別のデバイスへのハンドルを開きます。後者のデバイスのドライバースタックには、UMDF ドライバーが含まれています。

つまり、カーネルモードのクライアントをサポートする UMDF ドライバーは、カーネルモードドライバーから i/o 要求を受け取ることができます。 カーネルモードドライバーは、ユーザーモードアプリケーションから受信した i/o 要求を転送したり、新しい i/o 要求を作成してユーザーモードドライバーに送信したりすることができます。

UMDF ドライバーでカーネルモードクライアントがサポートされている必要があるかどうかを判断するには、ドライバーを追加するドライバースタックと、そのスタック内でドライバーが存在する場所を理解する必要があります。 また、別のスタックのドライバーがドライバーのデバイスに i/o 要求を送信するかどうかも決定する必要があります。

次の場合、ドライバーはカーネルモードクライアントをサポートする必要があります。

-   カーネルモードドライバーは、UMDF ドライバーのすぐ上にあるドライバースタックに配置できます。 たとえば、カーネルモードフィルタードライバーは、UMDF ベースの関数ドライバーのすぐ上に存在する場合があります。

-   別のスタックからのカーネルモードドライバーは、ドライバーのデバイスに i/o 要求を送信できます。 たとえば、ドライバーがシンボリックリンクを作成し、別のスタックのカーネルモードドライバーがドライバーのデバイスへのハンドルを開くために使用できます。 カーネルモードドライバーは、デバイスに i/o 要求を送信できます。

### <a href="" id="how-to-support-kernel-mode-clients-in-a-umdf-based-driver"></a>UMDF ドライバーでカーネルモードクライアントをサポートする方法

Umdf ドライバーでは、カーネルモードのクライアントのサポートが有効になっている場合にのみ、カーネルモードドライバーから i/o 要求を受信できます。 さらに、デバイスのインストール時に、デバイスのドライバースタックにある UMDF ドライバーの上にカーネルモードドライバーを読み込もうとすると、UMDF ドライバーでカーネルモードクライアントのサポートが有効になっている場合にのみ、このフレームワークによってドライバーが読み込まれるようになります。

UMDF ドライバーによるカーネルモードクライアントのサポートを有効にするには、UMDF ドライバーの INF ファイルに、その INF *Ddinstall*に[Umdfkernel Modeclientpolicy](specifying-wdf-directives-in-inf-files.md)ディレクティブが含まれている必要があります。**WDF**セクション。 UMDF ドライバーの INF ファイルにこのディレクティブが含まれていない場合、umdf は、UMDF ドライバーの上にインストールされているカーネルモードドライバーの実行を許可しません。

このフレームワークには、カーネルモードクライアントをサポートするドライバーに役立つ2つのメソッドが用意されています。 ドライバーは、 [**IWDFIoRequest2:: GetRequestorMode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-getrequestormode)メソッドを呼び出して、i/o 要求がカーネルモードとユーザーモードのどちらであるかを判断できます。 I/o 要求がユーザーモードから送信された場合、ドライバーは[**IWDFIoRequest2:: IsFromUserModeDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest2-isfromusermodedriver)を呼び出して、要求がアプリケーションまたは別のユーザーモードドライバーから送信されたかどうかを判断できます。

### <a name="restrictions-on-kernel-mode-drivers"></a>カーネルモードドライバーに関する制限事項

UMDF ドライバーは、カーネルモードドライバーが次の要件を満たしている場合にのみ、カーネルモードドライバーからの i/o 要求を処理できます。

-   カーネルモードドライバーは、i/o 要求を送信するときに、IRQL = パッシブ\_レベルで実行されている必要があります。

-   ドライバーによって**Umdffileobjectpolicy** INF ディレクティブが**AllowNullAndUnknownFileObjects**に設定されていない限り、カーネルモードドライバーに送信される各 i/o 要求には、関連付けられたファイルオブジェクトが必要です。 このフレームワークには、i/o マネージャーによってファイルオブジェクトが作成されたことがあらかじめ通知されている必要があります。 (この通知により、フレームワークはユーザーモードドライバーの[**Iqueuecallbackcreate:: OnCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackcreate-oncreatefile)コールバック関数を呼び出しますが、そのコールバック関数は省略可能です)。

-   I/o 要求には、 [**IRP\_MJ\_内部\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)関数コードを含めることはできません。

-   ユーザーモードドライバーはポインターを逆参照できないため、i/o 要求のバッファーに追加情報へのポインターを含めることはできません。

-   I/o 要求に "両方" のバッファーアクセス方法を指定する[i/o 制御コード](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-i-o-control-codes)が含まれている場合、カーネルモードドライバーは、i/o 要求を作成したアプリケーションのプロセスコンテキストで i/o 要求を送信する必要があります。 UMDF ベースのドライバーで "どちらの" メソッドをサポートする方法の詳細については、「 [Umdf ドライバーでのバッファー i/o と直接 i/o の両方を使用](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-umdf-1-x-drivers#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)する」を参照してください。

-   UMDF ドライバーによって、i/o 要求の出力データがユーザーモードで変更される場合があります。 そのため、カーネルモードドライバーは、ユーザーモードドライバーから受け取った出力データを検証する必要があります。

-   通常、カーネルモードクライアントは、UMDF ドライバーが[**IWDFIoRequest:: CompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation)に渡す*情報*の値を検証する必要があります。 クライアントが KMDF ドライバーの場合、 [**Wdfrequestgetreference params**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetcompletionparams)を呼び出して、この情報を IO\_状態\_ブロック構造で取得できます。

    通常、フレームワークでは、UMDF ドライバーが[**IWDFIoRequest:: CompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation)に渡す情報値は検証されません。 (このパラメーターは、通常、転送されるバイト数を指定します。)フレームワークは、バッファー内の[i/o](https://docs.microsoft.com/windows-hardware/drivers/wdf/accessing-data-buffers-in-umdf-1-x-drivers#using-buffered-i-o-in-umdf-drivers)データアクセスメソッドに対してのみ、出力バッファーの情報値を検証します。 (たとえば、アクセスメソッドがバッファリングされている場合、フレームワークは、転送されたバイト数が読み取り操作の出力バッファーサイズを超えていないことを確認します)。

### <a href="" id="handling-return-status-values"></a>UMDF 1.x ドライバーでの戻り値の状態の値の処理

戻り値の状態の値をユーザーモードからカーネルモードに渡すには、次のように特別な注意が必要です。

-   通常、UMDF version 1 のドライバーは HRESULT で型指定された戻り値を受け取りますが、KMDF および WDM ベースのカーネルモードドライバーは通常、NTSTATUS で型指定された値を受け取ります。 UMDF 1 の場合。*x*ドライバーは i/o 要求を完了し、ドライバーにカーネルモードクライアントがある場合は、ドライバーが[**IWDFIoRequest:: Complete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete)または[**IWDFIoRequest:: completewithinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation)を呼び出したときに、ドライバーが NTSTATUS 値から生成する HRESULT 値を指定する必要があります。 一般に、UMDF 1 です。*x*ドライバーは、( *winerror.h*で定義されている)\_NT マクロからの HRESULT\_を使用して、カーネルモードのクライアントに状態を返す必要があります。 次の例は、要求の完了時にこのマクロを使用する方法を示しています。

    ```cpp
    hr = HRESULT_FROM_NT(STATUS_BUFFER_OVERFLOW)
    request->Complete(HRESULT_FROM_NT(STATUS_BUFFER_OVERFLOW);
    return hr;
    ```

    カーネルモードクライアントに特定の HRESULT 値を返すには、次のコールバックで\_NT マクロからの HRESULT\_を使用する必要があります。

    -   [**IPnpCallback::OnQueryRemove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-onqueryremove)
    -   [**IPnpCallback::OnQueryStop**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-onquerystop)
    -   [**IPnpCallbackHardware:: On Hardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)
    -   [**IPnpCallbackHardware:: OnReleaseHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onreleasehardware)

    *Ntstatus*で定義されている ntstatus 値を使用するには、UMDF 1 を使用します。*x*ドライバーは、追加のヘッダーを含める前に、これらの2行を含める必要があります。

    ```cpp
    #define UMDF_USING_NTSTATUS
    #include <ntstatus.h>
    ```

    \_NT マクロから HRESULT\_を使用して、\_の正常な状態を NTSTATUS 値から HRESULT 値に変換しないでください。 次の例に示すように、S\_OK を返すだけです。

    ```cpp
    request->Complete(S_OK);
    ```

-   フレームワークは、UMDF ドライバーに代わっていくつかの i/o 要求を完了します。 場合によっては、フレームワークが HRESULT 型の戻り値を等価の NTSTATUS 値に変換することはないため、フレームワークは、HRESULT 型の完了状態をカーネルモードクライアントに渡すことがあります。

    このような状況により、カーネルモードのクライアントは、i/o 要求の完了状態をテストするときに NT\_ERROR マクロを使用しないようにする必要があります。これは、NT\_のエラーマクロから HRESULT エラー値に対して**TRUE**が返されないためです。 カーネルモードドライバーは、i/o 要求の完了状態をテストするときに NT\_SUCCESS マクロを使用する必要があります。

### <a href="" id="kernel-mode-client-support-in-earlier-umdf-versions"></a>以前のバージョンの UMDF でのカーネルモードクライアントのサポート

バージョン1.9 より前の UMDF バージョンでは、ドライバーの INF ファイルに[**Inf AddReg ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)を含めて、デバイスの[ハードウェアキー](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-the-registry-in-umdf-1-x-drivers)の**wudf**サブキーの下に REG\_DWORD サイズの**UpperDriverOk**レジストリ値を作成することができます。

**UpperDriverOk**レジストリ値が0以外の値に設定されている場合、フレームワークはカーネルモードドライバーをユーザーモードドライバーの上に読み込むことを許可します。 カーネルモードドライバーは、ユーザーモードアプリケーションから UMDF ドライバーに i/o 要求を転送できますが、カーネルモードドライバーは、カーネルモードで作成された i/o 要求を、UMDF ドライバーに送信することはできません。

UMDF バージョン1.9 以降では、 **UpperDriverOk**レジストリ値は互換性のために残されており、既存のドライバーに対してのみサポートされています。 新しいドライバーでは、 [Umdfカーネル Modeclientpolicy](specifying-wdf-directives-in-inf-files.md)ディレクティブを使用する必要があります。

 

 





