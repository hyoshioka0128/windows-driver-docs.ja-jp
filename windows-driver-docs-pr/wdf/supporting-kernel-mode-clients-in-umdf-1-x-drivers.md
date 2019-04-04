---
title: UMDF 1.x ドライバーでのカーネルモード クライアントのサポート
description: UMDF 1.x ドライバーでのカーネルモード クライアントのサポート
ms.assetid: 933dc761-2616-4bee-8357-dbb6644596c2
keywords:
- カーネル モードのクライアント WDK UMDF
- UMDF ドライバー WDK UMDF、カーネル モードのクライアント
- ユーザー モード ドライバー WDK UMDF、カーネル モードのクライアント
- UMDF WDK、カーネル モードのクライアント
- ユーザー モード ドライバー フレームワーク WDK、カーネル モードのクライアント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec32535a9052f82d50cc9ba0addba1b932623348
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571731"
---
# <a name="supporting-kernel-mode-clients-in-umdf-1x-drivers"></a>UMDF 1.x ドライバーでのカーネルモード クライアントのサポート

[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

>[!WARNING]
>参照してください[UMDF でカーネル モードのクライアントをサポートしている 2.x](supporting-kernel-mode-clients-in-umdf-drivers.md)します。

UMDF バージョン 1.9 以降をサポートする UMDF ドライバーを許可する*カーネル モードのクライアント*します。 カーネル モードのクライアントには、次のいずれかを指定できます。

-   デバイスのドライバー スタックで UMDF ドライバー上に存在するカーネル モード ドライバー。

-   1 つのデバイスをサポートしている 1 つのデバイス スタックのカーネル モード ドライバーは、別のデバイスを識別するハンドルを開き、後者のデバイスのドライバー スタックには UMDF ドライバーが含まれています。

つまり、カーネル モードのクライアントをサポートしている UMDF ドライバーでは、カーネル モード ドライバーからの I/O 要求を受信できます。 カーネル モード ドライバーことができます、ユーザー モード アプリケーションから受信した I/O 要求を転送または新しい I/O 要求を作成でき、ユーザー モード ドライバーに送信できます。

かどうかには、UMDF ドライバーはカーネル モードのクライアントをサポートする必要がありますを確認するのには、ドライバーを追加してそのスタックには、ドライバーが存在するドライバー スタックを理解しておく必要があります。 また、別のスタックからドライバーがドライバーのデバイスに I/O 要求を送信可能性があるかどうかを確認する必要があります。

場合、ドライバーはカーネル モードのクライアントをサポートする必要があります。

-   カーネル モード ドライバーはドライバー スタックで、UMDF ドライバーのすぐ上に配置できます。 たとえば、カーネル モードのフィルター ドライバーは可能性があります UMDF ベースの関数のドライバーのすぐ上に存在します。

-   別のスタックからカーネル モード ドライバーでは、ドライバーのデバイスに、I/O 要求を送信できます。 など、ドライバーは、別のスタックでのカーネル モード ドライバーがドライバーのデバイスを識別するハンドルを開くときに使用できますシンボリック リンクを作成する可能性があります。 カーネル モード ドライバーは、デバイスの I/O 要求を送信できます。

### <a href="" id="how-to-support-kernel-mode-clients-in-a-umdf-based-driver"></a>UMDF ドライバーでカーネル モードのクライアントをサポートする方法

UMDF ドライバーは、UMDF ドライバーには、カーネル モードのクライアントのサポートが有効にする場合にのみ、カーネル モード ドライバーからの I/O 要求を受信できます。 さらに、デバイスのインストールが、デバイスのドライバー スタックで UMDF ドライバーの上位のカーネル モード ドライバーをロードしようとすると、フレームワークは UMDF ドライバーには、カーネル モードのクライアントのサポートが有効になっている場合にのみ読み込むドライバーをできます。

カーネル モードのクライアントの UMDF ドライバーのサポートを有効にする UMDF ドライバーの INF ファイルを含める必要があります、 [UmdfKernelModeClientPolicy](specifying-wdf-directives-in-inf-files.md)ディレクティブ、INF で*DDInstall*.**WDF**セクション。 UMDF ドライバーの INF ファイルにこのディレクティブが含まれていない場合 UMDF には、UMDF ドライバーを実行する前にインストールされているカーネル モード ドライバーはできません。

フレームワークは、カーネル モードのクライアントをサポートするドライバーに役立つ 2 つのメソッドを提供します。 ドライバーを呼び出すことができます、 [ **IWDFIoRequest2::GetRequestorMode** ](https://msdn.microsoft.com/library/windows/hardware/ff559002) I/O 要求がカーネル モードまたはユーザー モードからのものかどうかを判断するメソッド。 ドライバーを呼び出すことができる場合、I/O 要求は、ユーザー モードから付属していた、 [ **IWDFIoRequest2::IsFromUserModeDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559021)を要求がアプリケーションまたは別のユーザー モード ドライバーからのものかどうかを判断します。

### <a name="restrictions-on-kernel-mode-drivers"></a>カーネル モード ドライバーに関する制限事項

カーネル モード ドライバーは、次の要件を満たす場合にのみ、UMDF ドライバーでは、カーネル モード ドライバーからの I/O 要求を処理できます。

-   IRQL では、カーネル モード ドライバーを実行する必要があります = パッシブ\_レベルの I/O 要求を送信するとき。

-   ドライバーが設定されていない限り、 **UmdfFileObjectPolicy** INF ディレクティブを**AllowNullAndUnknownFileObjects**、カーネル モード ドライバーがユーザー モード ドライバーに送信する I/O 要求ごとに、関連付けられている必要がありますファイル オブジェクト。 フレームワークする必要があります前に通知されました I/O マネージャーが、ファイル オブジェクトを作成します。 (このような通知が配信を呼び出して、ユーザー モード ドライバーのフレームワークが[ **IQueueCallbackCreate::OnCreateFile** ](https://msdn.microsoft.com/library/windows/hardware/ff556841)コールバック関数がコールバック関数はオプションです)。

-   I/O 要求を含めることはできません、 [ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)関数コード。

-   ユーザー モード ドライバーには、ポインターが逆参照できませんので、I/O 要求のバッファーは追加の情報へのポインターを含めないでください。

-   I/O 要求が含まれている場合、 [I/O 制御コード](https://msdn.microsoft.com/library/windows/hardware/ff565406)「も」バッファーへのアクセス方法を指定する、カーネル モード ドライバーは、I/O 要求を作成したアプリケーションのプロセスのコンテキストで I/O 要求を送信する必要があります。 ベース UMDF ドライバーで「も」メソッドをサポートする方法の詳細については、[I/O を使用していないバッファーも UMDF ドライバーでのダイレクト I/O](https://msdn.microsoft.com/library/windows/hardware/ff554413#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)を参照してください。

-   UMDF ドライバーでは、ユーザー モードでの I/O 要求の出力データを変更可能性があります。 そのため、カーネル モード ドライバーでは、ユーザー モード ドライバーから受信したすべての出力データを検証する必要があります。

-   カーネル モード クライアントは通常を検証する必要があります、*情報*UMDF ドライバーに渡す値[ **IWDFIoRequest::CompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff559074)します。 呼び出すことができます、クライアントが KMDF ドライバーの場合は、 [ **WdfRequestGetCompletionParams** ](https://msdn.microsoft.com/library/windows/hardware/ff549961) IO では、この情報を取得する\_状態\_ブロック構造体。

    通常、フレームワークが UMDF ドライバーからに渡される情報の値を検証しません[ **IWDFIoRequest::CompleteWithInformation**](https://msdn.microsoft.com/library/windows/hardware/ff559074)します。 (このパラメーターは、通常の数を指定転送されたバイト。)フレームワークは、出力バッファーとのみの情報値を検証、 [I/O バッファーに格納](https://msdn.microsoft.com/library/windows/hardware/ff554413#using-buffered-i-o-in-umdf-drivers)メソッドがデータにアクセスします。 (たとえば、フレームワークを確認転送されたバイト数が、読み取り操作の出力バッファーのサイズを超えていないこと、アクセスする方法がバッファリングされる場合 I/O)。

### <a href="" id="handling-return-status-values"></a>UMDF ドライバーでは 1.x の状態の戻り値の処理

カーネル モードへのユーザー モードの状態の戻り値を渡すことと、特別な注意には、次のように必要です。

-   UMDF ドライバーのバージョン 1 では、戻り値の HRESULT に型指定された通常表示される、KMDF 中および WDM ベース カーネル モード ドライバーが NTSTATUS 型の値を通常受信します。 UMDF 1 とします。*x*ドライバー、I/O 要求が完了すると、ドライバーには、カーネル モードのクライアントでは、ドライバーの呼び出しが含まれている場合と[ **IWDFIoRequest::Complete** ](https://msdn.microsoft.com/library/windows/hardware/ff559070)または[ **IWDFIoRequest::CompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559074) NTSTATUS 値からドライバーを生成する HRESULT 値を指定する必要があります。 一般に、UMDF 1。*x*ドライバーは、HRESULT を使用する必要があります\_FROM\_NT マクロ (で定義されている*Winerror.h*)、カーネル モードのクライアントに状態を返すにします。 次の例では、要求を完了するときに、このマクロを使用する方法を示します。

    ```cpp
    hr = HRESULT_FROM_NT(STATUS_BUFFER_OVERFLOW)
    request->Complete(HRESULT_FROM_NT(STATUS_BUFFER_OVERFLOW);
    return hr;
    ```

    カーネル モードのクライアントに特定の HRESULT 値を返す、次のコールバックは、HRESULT を使用する必要があります\_FROM\_NT マクロ。

    -   [**IPnpCallback::OnQueryRemove**](https://msdn.microsoft.com/library/windows/hardware/ff556808)
    -   [**IPnpCallback::OnQueryStop**](https://msdn.microsoft.com/library/windows/hardware/ff556811)
    -   [**IPnpCallbackHardware::OnPrepareHardware**](https://msdn.microsoft.com/library/windows/hardware/ff556766)
    -   [**IPnpCallbackHardware::OnReleaseHardware**](https://msdn.microsoft.com/library/windows/hardware/ff556768)

    定義されている NTSTATUS 値を使用する*ntstatus.h*、UMDF 1 *。x*ドライバーは、追加のヘッダーをインクルードする前に次の 2 行を含める必要があります。

    ```cpp
    #define UMDF_USING_NTSTATUS
    #include <ntstatus.h>
    ```

    HRESULT を使用しないでください\_FROM\_状態に変換する NT マクロ\_NTSTATUS 値からの成功 HRESULT 値。 戻り値の S\_確かに、次の例に示すようにします。

    ```cpp
    request->Complete(S_OK);
    ```

-   フレームワークは UMDF ドライバーの代わりには、いくつか I/O 要求を完了します。 場合があります、フレームワークに変換されません戻り値の HRESULT に型指定された同等の NTSTATUS 値ためフレームワークは、カーネル モードのクライアントに、HRESULT に型指定された完了状態を渡す可能性があります。

    このような状況が原因カーネル モードのクライアント使用しないでください、NT\_エラー マクロは、I/O 要求の完了の状態をテストしている場合、NT\_エラー マクロは返されません**TRUE** HRESULT エラー値。 カーネル モード ドライバーは、NT を使用する必要があります\_成功マクロは、I/O 要求の完了状態をテストするときにします。

### <a href="" id="kernel-mode-client-support-in-earlier-umdf-versions"></a> UMDF の以前のバージョンのカーネル モードのクライアントのサポート

UMDF バージョンより前のバージョン 1.9、ドライバーの INF ファイルを含めることが、 [ **INF AddReg ディレクティブ**](https://msdn.microsoft.com/library/windows/hardware/ff546320) 、レジストリを作成する\_DWORD 規模**UpperDriverOk**下のレジストリ値、 **WUDF**のデバイスのサブキー[ハードウェア キー](https://msdn.microsoft.com/library/windows/hardware/ff561381)します。

場合、 **UpperDriverOk**レジストリ値が 0 以外の数値に設定されて、フレームワークにより、カーネル モード ドライバーを読み込む前に、ユーザー モード ドライバー。 カーネル モード ドライバーは、UMDF ドライバーにカーネル モードで作成された I/O 要求を送信できない場合は、カーネル モード ドライバーは、UMDF ドライバーでは、ユーザー モード アプリケーションからの I/O 要求を転送できます。

UMDF バージョン 1.9 以降、 **UpperDriverOk**レジストリ値が廃止され、既存のドライバーでのみサポートされます。 新しいドライバーを使用する必要があります、 [UmdfKernelModeClientPolicy](specifying-wdf-directives-in-inf-files.md)ディレクティブ。

 

 





