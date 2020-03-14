---
title: サービス アプリケーションのデバッグの準備
description: サービス アプリケーションのデバッグの準備
ms.assetid: 332b7bcf-22e4-4b98-bcb3-3646f8bd63fd
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2967f4b5d31b49adbfbf25f9f967948ffb761429
ms.sourcegitcommit: b316c97bafade8b76d5d3c30d48496915709a9df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79242789"
---
# <a name="preparing-to-debug-the-service-application"></a>サービス アプリケーションのデバッグの準備


このトピックでは、サービスアプリケーションをデバッグする前に必要になる可能性があるすべての準備手順を示します。 シナリオで必要な手順は、選択したアタッチオプションと選択したデバッグ構成によって異なります。 これらの選択肢の一覧については、「[最適な方法の選択](choosing-the-best-method.md)」を参照してください。

このトピックで説明する各準備手順では、必要な条件を指定します。 これらの手順は、任意の順序で実行できます。

### <a name="span-idenabling-the-debugging-of-the-initialization_codespanspan-idenabling_the_debugging_of_the_initialization_codespan-enabling-the-debugging-of-the-initialization-code"></a><span id="enabling-the-debugging-of-the-initialization_code"></span><span id="ENABLING_THE_DEBUGGING_OF_THE_INITIALIZATION_CODE"></span>初期化コードのデバッグを有効にする

初期化コードを含め、実行の開始時からサービスアプリケーションをデバッグする場合は、この準備手順が必要です。

次のレジストリキーを探して作成します。ここで、 *ProgramName*はサービスアプリケーションの実行可能ファイルの名前です。

```text
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\ProgramName 
```

*ProgramName*にはファイル名拡張子を含める必要がありますが、パスは含めないでください。 たとえば、 *ProgramName*は myservice .exe または .dll です。

このレジストリキーの下に、**デバッガー**という文字列データ値を作成します。 この文字列の値は、サービスアプリケーションにアタッチするデバッガーの完全なパスとファイル名に設定する必要があります。

-   ローカルでデバッグする場合は、次のような文字列を使用します。

    ```console
    c:\Debuggers\windbg.exe 
    ```

    Windows Vista 以降のバージョンの Windows を実行している場合は、このオプションを選択しないでください。

-   リモートデバッグを使用する場合は、-noio オプションを使用して NTSD を指定します。 これにより、リモート接続を介してのみアクセス可能な独自のコンソールなしに、NTSD が実行されます。 例 :

    ```console
    c:\Debuggers\ntsd.exe -server ServerTransport -noio -y SymbolPath 
    ```

    Windows が完全に読み込まれる前にデバッグセッションが開始された場合は、リモート共有からシンボルにアクセスできない可能性があります。このような場合は、ローカルシンボルを使用する必要があります。 *Servertransport*では、TCP や npipe などのユーザーモードサービスとやり取りせずに、Windows カーネルによって実装されるトランスポートプロトコルを指定する必要があります。 *Servertransport*の構文については、「[**デバッグサーバーのアクティブ化**](activating-a-debugging-server.md)」を参照してください。

-   カーネルモードのデバッガーからユーザーモードのデバッガーを制御する場合は、-d オプションを使用して NTSD を指定します。 例 :

    ```console
    c:\Debuggers\ntsd.exe -d -y SymbolPath 
    ```

    このメソッドを使用する予定があり、ユーザーモードシンボルにシンボルサーバーからアクセスする場合は、このメソッドとリモートデバッグを組み合わせる必要があります。 この場合は、-ddefer オプションを使用して NTSD を指定します。 Windows カーネルによって実装されるトランスポートプロトコルを選択します。このプロトコルは、TCP や NPIPE などのユーザーモードサービスとやり取りする必要はありません。 例 :

    ```console
    c:\Debuggers\ntsd.exe -server ServerTransport -ddefer -y SymbolPath 
    ```

    詳細については、「[カーネルデバッガーからのユーザーモードデバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)」を参照してください。

このレジストリの編集が完了すると、この名前のサービスが開始または再開されるたびにデバッガーが起動します。

### <a name="span-idenabling-the-service-application-to-break-into-the-debuggerspanspan-idenabling_the_service_application_to_break_into_the_debuggerspan-enabling-the-service-application-to-break-into-the-debugger"></a><span id="enabling-the-service-application-to-break-into-the-debugger"></span><span id="ENABLING_THE_SERVICE_APPLICATION_TO_BREAK_INTO_THE_DEBUGGER"></span>サービスアプリケーションがデバッガーに侵入するのを有効にする

サービスアプリケーションがクラッシュしたとき、または例外が発生したときにデバッガーを中断する場合は、この準備手順を実行する必要があります。 この手順は、 **DebugBreak**関数を呼び出してサービスアプリケーションをデバッガーに中断させる場合にも必要です。

**注**   初期化コードのデバッグを有効にした場合 (「初期化コードのデバッグを有効にする」で説明されている手順)、この手順を省略する必要があります。 初期化コードのデバッグが有効になっている場合、デバッガーは起動時にサービスアプリケーションにアタッチします。これにより、 **DebugBreak**のすべてのクラッシュ、例外、および呼び出しが、追加の準備を必要とせずにデバッガーにルーティングされます。

 

この準備手順では、選択したデバッガーを事後分析デバッガーとして登録します。 これを行うには、デバッガーのコマンドラインで-iae オプションまたは-iae オプションを使用します。 次のコマンドを使用することをお勧めしますが、これらを変更する場合は、「[事後分析のデバッグを有効](enabling-postmortem-debugging.md)にする」にある構文の詳細を参照してください。

-   ローカルでデバッグする場合は、次のようなコマンドを使用します。

    ```console
    windbg -iae 
    ```

    Windows Vista 以降のバージョンの Windows を実行している場合は、このオプションを選択しないでください。

-   リモートデバッグを使用する場合は、-noio オプションを使用して NTSD を指定します。 これにより、リモート接続を介してのみアクセス可能な独自のコンソールなしに、NTSD が実行されます。 -Server パラメーターを含む事後分析デバッガーをインストールするには、レジストリを手動で編集する必要があります。詳細については、「[事後分析デバッグの有効化](enabling-postmortem-debugging.md)」を参照してください。 たとえば、 **AeDebug**キーの**デバッガー**値は次のようになります。

    ```console
    ntsd -server npipe:pipe=myproc%x -noio -p %ld -e %ld -g -y SymbolPath 
    ```

    パイプの仕様では、 **% x**トークンは、デバッガーを起動するプロセスのプロセス ID に置き換えられます。 これにより、複数のプロセスが事後分析デバッガーを起動し、それぞれに一意のパイプ名があることが保証されます。 Windows が完全に読み込まれる前にデバッグセッションが開始された場合は、リモート共有からシンボルにアクセスできない可能性があります。このような場合は、ローカルシンボルを使用する必要があります。 *Servertransport*では、TCP や npipe などのユーザーモードサービスとやり取りせずに、Windows カーネルによって実装されるトランスポートプロトコルを指定する必要があります。 *Servertransport*の構文については、「[**デバッグサーバーのアクティブ化**](activating-a-debugging-server.md)」を参照してください。

-   カーネルモードのデバッガーからユーザーモードのデバッガーを制御する場合は、-d オプションを使用して NTSD を指定します。 例 :

    ```console
    ntsd -iaec -d -y SymbolPath 
    ```

    この方法を選択し、シンボルサーバーからユーザーモードシンボルにアクセスする場合は、このメソッドとリモートデバッグを組み合わせる必要があります。 この場合は、-ddefer オプションを使用して NTSD を指定します。 Windows カーネルによって実装されるトランスポートプロトコルを選択します。このプロトコルは、TCP や NPIPE などのユーザーモードサービスとやり取りする必要はありません。 -Server パラメーターを含む事後分析デバッガーをインストールするには、レジストリを手動で編集する必要があります。詳細については、「[事後分析デバッグの有効化](enabling-postmortem-debugging.md)」を参照してください。 たとえば、 **AeDebug**キーの**デバッガー**値は次のようになります。

    ```console
    ntsd -server npipe:pipe=myproc%x -ddefer -p %ld -e %ld -g -y SymbolPath 
    ```

    詳細については、「[カーネルデバッガーからのユーザーモードデバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)」を参照してください。

これらのコマンドのいずれかを実行すると、事後分析デバッガーが登録されます。 このデバッガーは、サービスアプリケーションを含むユーザーモードプログラムが例外を検出したとき、または**DebugBreak**関数を実行するたびに起動されます。

### <a name="span-idadjusting-the-service-application-timeoutspanspan-idadjusting_the_service_application_timeoutspan-adjusting-the-service-application-timeout"></a><span id="adjusting-the-service-application-timeout"></span><span id="ADJUSTING_THE_SERVICE_APPLICATION_TIMEOUT"></span>サービスアプリケーションタイムアウトの調整

(サービスの開始時または例外が発生したときに) デバッガーを自動的に起動する予定がある場合は、この準備手順が必要です。

次のレジストリ キーを探します。

```text
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control
```

このキーの下で、 **ServicesPipeTimeout**という名前の DWORD データ値を検索または作成します。 このエントリを、サービスがタイムアウトするまでの待機時間をミリ秒単位で設定します。たとえば、値6万は1分ですが、値8640万は24時間です。 このレジストリ値が設定されていない場合、既定のタイムアウトは約30秒です。

この値の意味は、各サービスが起動されたときにクロックが開始され、タイムアウト値に達すると、サービスにアタッチされているデバッガーがすべて終了されることです。 そのため、選択する値は、サービスの起動からデバッグセッションの完了までに経過した時間の合計を超えないようにする必要があります。

この設定は、レジストリの編集が完了した後に開始または再起動されたすべてのサービスに適用されます。 一部のサービスがクラッシュまたはハングしても、この設定が有効な場合は、Windows によって問題が検出されません。 したがって、この設定はデバッグ中にのみ使用し、デバッグが完了した後でレジストリキーを元の値に戻す必要があります。

### <a name="span-idisolating-the-servicespanspan-idisolating_the_servicespan-isolating-the-service"></a><span id="isolating-the-service"></span><span id="ISOLATING_THE_SERVICE"></span>サービスの分離

場合によっては、単一のサービスホスト (Svchost) プロセスで複数のサービスが結合されることがあります。 このようなサービスをデバッグする場合は、最初に別の Svchost プロセスに分離する必要があります。

サービスを分離するには、次の3つの方法があります。 Microsoft では、次のように、サービスを独自のグループメソッドに移行することをお勧めします。 代替の方法 (サービスの種類の変更と SvcHost バイナリの複製) は、デバッグのために一時的に使用できますが、サービスの実行方法が変更されるため、最初の方法ほど信頼性がありません。

**推奨される方法: サービスを独自のグループに移動する**

1.  次のサービス構成ツール (Sc.exe) コマンドを実行します。ここで、 *ServiceName*はサービスの名前です。

    ```console
    sc qc ServiceName 
    ```

    これにより、サービスの現在の構成値が表示されます。 対象の値は、サービスコントロールプログラムの起動に使用するコマンドラインを指定する、バイナリ\_PATH\_NAME です。 このシナリオでは、サービスがまだ分離されていないため、このコマンドラインにはディレクトリパス、Svchost.exe、および-k スイッチを含むいくつかの SvcHost パラメーターと、その後にグループ名が含まれています。 たとえば、次のようになります。

    ```console
    %SystemRoot%\System32\svchost.exe -k LocalServiceNoNetwork 
    ```

    このパスとグループ名を覚えておいてください。これらは、手順 5. および 6. で使用されます。

2.  次のレジストリ キーを探します。

    ```text
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\SvcHost 
    ```

    一意の名前 (たとえば、 **Tempgrp**) を使用して、新しい REG\_複数\_SZ 値を作成します。

3.  この新しい値を、分離するサービスの名前と同じに設定します。 ディレクトリパスまたはファイル名拡張子を含めないでください。 たとえば、新しい値**Tempgrp** Equal を**myservice**に設定できます。

4.  同じレジストリキーの下で、手順 2. で使用したものと同じ名前の新しいキーを作成します。 例 :

    ```text
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\SvcHost\TempGrp 
    ```

    これで、SvcHost キーに新しい名前の値が含まれています。また、同じ名前の下位キーもあります。

5.  Svchost.exe キーの下位に、手順 1. で見つかったグループと同じ名前を持つ別のキーがあるかどうかを確認します。 このようなキーが存在する場合は、その中のすべての値を確認し、手順 4. で作成した新しいキーにそれらの重複部分を作成します。

    たとえば、古いキーは次のように名前が付けられます。

    ```text
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\SvcHost\LocalServiceNoNetwork 
    ```

    また、 **CoInitializeSecurityParam**、 **authenticationcapabilities**、その他の値などの値が含まれている場合もあります。 新しく作成されたキーに移ります。

    ```text
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\SvcHost\TempGrp 
    ```

    とは、名前、型、およびデータと、古いキーの値とで同一の値を作成します。

    古いキーが存在しない場合は、新しいキーを作成する必要はありません。

6.  次のサービス構成ツールコマンドを使用して、手順1で確認したパスを変更します。

    ```console
    sc config ServiceName binPath= "RevisedPath" 
    ```

    このコマンドで、 *ServiceName*はサービスの名前です。 *REVISEDPATH*は、バイナリ\_パス\_名に指定する新しい値です。 *RevisedPath*の場合は、手順 1. で表示されたものとまったく同じパスを使用します。このパスは、その行に表示されるすべてのオプションを含み、1つの変更のみを行います。-k スイッチの後のパラメーターを、手順 2. で作成した新しいレジストリ値の名前に置き換えます。 *RevisedPath*を引用符で囲みます。 等号の後のスペースが必要です。

    たとえば、コマンドは次のようになります。

    ```console
    sc config MyService binPath= "%SystemRoot%\System32\svchost.exe -k TempGrp" 
    ```

    **Sc qc**コマンドをもう一度使用して、行った変更を確認することもできます。

これらの設定は、次回サービスが開始されたときに有効になります。 古いサービスの影響をクリアするには、サービスを再起動するのではなく、Windows を再起動することをお勧めします。

デバッグが完了したら、このサービスを共有サービスホストに返す場合は、 **sc config**コマンドをもう一度使用して、バイナリパスを元の値に戻し、作成した新しいレジストリキーと値を削除します。「」を検索します。

**代替方法: サービスの種類の変更**

1.  次のサービス構成ツール (Sc.exe) コマンドを実行します。ここで、 *ServiceName*はサービスの名前です。

    ```console
    sc config ServiceName type= own 
    ```

    等号の後のスペースが必要です。

2.  次のコマンドを使用して、サービスを再起動します。
    ```console
    net stop ServiceName 
    net start ServiceName 
    ```

この代替方法は、サービスの動作を変更できるため、推奨される方法ではありません。 この方法を使用する場合は、次のコマンドを使用して、デバッグの完了後に通常の動作に戻します。

```console
sc config ServiceName type= share 
```

**代替方法: SvcHost バイナリの複製**

1.  Svchost.exe 実行可能ファイルは、Windows の system32 ディレクトリにあります。 このファイルのコピーを作成し、svhost2 という名前を付けて、system32 ディレクトリにも配置します。

2.  次のサービス構成ツール (Sc.exe) コマンドを実行します。ここで、 *ServiceName*はサービスの名前です。

    ```console
    sc qc ServiceName 
    ```

    このコマンドは、サービスの現在の構成値を表示します。 対象の値は、サービスコントロールプログラムの起動に使用するコマンドラインを指定する、バイナリ\_PATH\_NAME です。 このシナリオでは、サービスがまだ分離されていないため、このコマンドラインにはディレクトリパス、Svchost.exe、および場合によってはいくつかの SvcHost パラメーターが含まれます。 たとえば、次のようになります。

    ```console
    %SystemRoot%\System32\svchost.exe -k LocalServiceNoNetwork 
    ```

3.  このパスを変更するには、次のコマンドを実行します。

    ```console
    sc config ServiceName binPath= "RevisedPath" 
    ```

    このコマンドで、 *ServiceName*はサービスの名前です。 *REVISEDPATH*は、バイナリ\_パス\_名に指定する新しい値です。 *RevisedPath*の場合は、手順 2. で表示されたものとまったく同じパスを使用します。これには、変更を1つだけ行います。 Svchost.exe を Svchost2 に置き換えます。 *RevisedPath*を引用符で囲みます。 等号の後のスペースが必要です。

    たとえば、コマンドは次のようになります。

    ```console
    sc config MyService binPath= "%SystemRoot%\System32\svchost2.exe -k LocalServiceNoNetwork" 
    ```

    **Sc qc**コマンドをもう一度使用して、行った変更を確認できます。

4.  次のコマンドを使用して、サービスを再起動します。
    ```console
    net stop ServiceName 
    net start ServiceName 
    ```

この代替方法は、サービスの動作を変更できるため、推奨される方法ではありません。 この方法を使用する場合は、デバッグを完了した後で、 **sc config**コマンドを使用してパスを元の値に戻します。

 

 





