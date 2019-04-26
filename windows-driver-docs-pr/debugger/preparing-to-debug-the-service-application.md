---
title: サービス アプリケーションのデバッグの準備
description: サービス アプリケーションのデバッグの準備
ms.assetid: 332b7bcf-22e4-4b98-bcb3-3646f8bd63fd
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2967f4b5d31b49adbfbf25f9f967948ffb761429
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357036"
---
# <a name="preparing-to-debug-the-service-application"></a>サービス アプリケーションのデバッグの準備


このトピックでは、サービス アプリケーションをデバッグする前に必要な可能性のあるすべての準備手順を使用します。 自分のシナリオでどの手順が必要に依存オプションを選択し、選択したデバッグ構成をアタッチします。 これらの選択肢の一覧は、次を参照してください。[最適な方法を選択する](choosing-the-best-method.md)します。

このトピックで説明されている準備手順のそれぞれには、必要がある条件を指定します。 任意の順序では、次の手順を実行できます。

### <a name="span-idenabling-the-debugging-of-the-initializationcodespanspan-idenablingthedebuggingoftheinitializationcodespan-enabling-the-debugging-of-the-initialization-code"></a><span id="enabling-the-debugging-of-the-initialization_code"></span><span id="ENABLING_THE_DEBUGGING_OF_THE_INITIALIZATION_CODE"></span> 初期化コードのデバッグの有効化

初期化コードを含む、その実行の先頭からのサービス アプリケーションをデバッグする場合は、このような準備手順が必要です。

検索するか、次のレジストリ キーの作成場所*ProgramName*サービス アプリケーションの実行可能ファイルの名前を指定します。

```text
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\ProgramName 
```

*ProgramName*ファイル名拡張子がパスではなく、含める必要があります。 たとえば、 *ProgramName* Myservice.exe または Thisservice.dll 可能性があります。

このレジストリ キーの作成というタイトルの文字列データ値**デバッガー**します。 この文字列の値は、サービス アプリケーションにアタッチするデバッガーの完全なパスとファイル名に設定する必要があります。

-   ローカルでデバッグする場合は、次などの文字列を使用します。

    ```console
    c:\Debuggers\windbg.exe 
    ```

    Windows Vista または Windows の以降のバージョンを実行している場合は、このオプションを選択しないでください。

-   リモート デバッグを使用する場合は、NTSD - noio オプションを使用して指定します。 これにより、独自の任意のコンソールなしで実行する NTSD をリモート接続を介してのみアクセスできます。 次に、例を示します。

    ```console
    c:\Debuggers\ntsd.exe -server ServerTransport -noio -y SymbolPath 
    ```

    デバッグ セッションの開始前に、Windows が完全に読み込まれると、; リモート共有からのシンボルにアクセスできません可能性があります。このような場合は、ローカル シンボルを使用する必要があります。 *サーバトランスポート*TCP や NPIPE などのユーザー モード サービスとのやり取りせず、Windows カーネルによって実装されているトランスポート プロトコルを指定する必要があります。 構文の*サーバトランスポート*を参照してください[**デバッグ サーバー アクティブ化する**](activating-a-debugging-server.md)します。

-   カーネル モード デバッガーからユーザー モードのデバッガーを制御する場合は、-d オプションを使用して NTSD を指定します。 次に、例を示します。

    ```console
    c:\Debuggers\ntsd.exe -d -y SymbolPath 
    ```

    ときにこのメソッドを使用して、ユーザー モードのシンボルがシンボル サーバーからアクセスされる場合は、このメソッドをリモート デバッグと組み合わせる必要があります。 この場合、- ddefer オプションを使用して NTSD を指定します。 TCP または NPIPE などのユーザー モード サービスとのやり取りせず、Windows カーネルによって実装されているトランスポート プロトコルを選択します。 次に、例を示します。

    ```console
    c:\Debuggers\ntsd.exe -server ServerTransport -ddefer -y SymbolPath 
    ```

    詳細については、次を参照してください。[カーネル デバッガーからユーザー モード デバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)します。

このレジストリ編集が完了した後、この名前のサービスを開始または再起動されるたびに、デバッガーが起動します。

### <a name="span-idenabling-the-service-application-to-break-into-the-debuggerspanspan-idenablingtheserviceapplicationtobreakintothedebuggerspan-enabling-the-service-application-to-break-into-the-debugger"></a><span id="enabling-the-service-application-to-break-into-the-debugger"></span><span id="ENABLING_THE_SERVICE_APPLICATION_TO_BREAK_INTO_THE_DEBUGGER"></span> デバッガーを中断するサービス アプリケーションを有効にします。

サービス アプリケーションがクラッシュまたは例外が発生したときに、デバッガーを中断する場合は、このような準備手順が必要です。 この手順は必要も呼び出すことによって、デバッガーを中断するサービス アプリケーションの場合、 **DebugBreak**関数。

**注**   (「初期化コードの、デバッグの有効化」のサブセクションで説明する手順) の初期化コードのデバッグを有効にした場合は、この手順をスキップする必要があります。 開始時に、すべてのクラッシュ、例外の原因し、への呼び出しをサービス アプリケーションに初期化コードのデバッグが有効になっているときに、デバッガーがアタッチされます**DebugBreak**せずデバッガーにルーティングされるようにする追加準備が必要になります。

 

このような準備手順では、選択したデバッガーを事後デバッガーとして登録する必要があります。 これは、デバッガーのコマンド ラインで iae - または - iaec オプションを使用して行います。 次のコマンドをお勧めしますが、それらを変更する場合の構文の詳細についてを参照してください。 ここ[事後のデバッグを有効にする](enabling-postmortem-debugging.md)します。

-   ローカルでデバッグする場合は、次のコマンドを使用します。

    ```console
    windbg -iae 
    ```

    Windows Vista または Windows の以降のバージョンを実行している場合は、このオプションを選択しないでください。

-   リモート デバッグを使用する場合は、NTSD - noio オプションを使用して指定します。 これにより、独自の任意のコンソールなしで実行する NTSD をリモート接続を介してのみアクセスできます。 含む事後デバッガーにインストールするサーバー パラメータを手動でレジストリを編集する必要があります詳細については、次を参照してください。[事後のデバッグを有効にする](enabling-postmortem-debugging.md)します。 たとえば、**デバッガー**の値、 **AeDebug**キーには、次が可能性があります。

    ```console
    ntsd -server npipe:pipe=myproc%x -noio -p %ld -e %ld -g -y SymbolPath 
    ```

    パイプの仕様、 **%x**トークンは、デバッガーを起動するプロセスのプロセス ID に置き換えられます。 これによりに場合は、複数のプロセスでは、事後デバッガーが起動したら、それぞれが一意のパイプ名。 デバッグ セッションの開始前に、Windows が完全に読み込まれると、; リモート共有からのシンボルにアクセスできません可能性があります。このような場合は、ローカル シンボルを使用する必要があります。 *サーバトランスポート*TCP や NPIPE などのユーザー モード サービスとのやり取りせず、Windows カーネルによって実装されているトランスポート プロトコルを指定する必要があります。 構文の*サーバトランスポート*を参照してください[**デバッグ サーバー アクティブ化する**](activating-a-debugging-server.md)します。

-   カーネル モード デバッガーからユーザー モードのデバッガーを制御する場合は、-d オプションを使用して NTSD を指定します。 次に、例を示します。

    ```console
    ntsd -iaec -d -y SymbolPath 
    ```

    このメソッドを選択してユーザー モードのシンボルをシンボル サーバーからアクセスする場合は、リモート デバッグでこのメソッドを組み合わせる必要があります。 この場合、- ddefer オプションを使用して NTSD を指定します。 TCP または NPIPE などのユーザー モード サービスとのやり取りせず、Windows カーネルによって実装されているトランスポート プロトコルを選択します。 含む事後デバッガーにインストールするサーバー パラメータを手動でレジストリを編集する必要があります詳細については、次を参照してください。[事後のデバッグを有効にする](enabling-postmortem-debugging.md)します。 たとえば、**デバッガー**の値、 **AeDebug**キーには、次が可能性があります。

    ```console
    ntsd -server npipe:pipe=myproc%x -ddefer -p %ld -e %ld -g -y SymbolPath 
    ```

    詳細については、次を参照してください。[カーネル デバッガーからユーザー モード デバッガーの制御](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)します。

これらのコマンドを実行する事後分析のデバッガーが登録されます。 このデバッガーを起動するにはサービス アプリケーションを含む、任意のユーザー モード プログラムが例外を検出または実行されるたびに、 **DebugBreak**関数。

### <a name="span-idadjusting-the-service-application-timeoutspanspan-idadjustingtheserviceapplicationtimeoutspan-adjusting-the-service-application-timeout"></a><span id="adjusting-the-service-application-timeout"></span><span id="ADJUSTING_THE_SERVICE_APPLICATION_TIMEOUT"></span> サービス アプリケーションのタイムアウトを調整します。

デバッガーを自動的に起動する場合 (サービスの開始時か、または例外が発生した場合)、このような準備手順が必要です。

次のレジストリ キーを探します。

```text
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control
```

このキーの下の 検索またはという DWORD データ値を作成する**ServicesPipeTimeout**します。 このエントリをサービスがタイムアウトになるまで待機するミリ秒単位の時間に設定します。たとえば、60,000 の値は 86,400, 000 の値は 24 時間中に、1 分間です。 このレジストリ値が設定されていないときに既定のタイムアウトは約 30 秒にします。

この値の意味とは、クロックが各サービスが起動され、時、およびタイムアウト値に達すると実行を開始、サービスに接続されているすべてのデバッガーは終了です。 そのため、選択した値は、サービスと、デバッグ セッションの完了を起動するまでに経過した時間の合計より長くする必要があります。

この設定は、開始またはレジストリの編集が完了した後に再起動されているすべてのサービスに適用されます。 サービスがクラッシュまたはハング、この設定の一部である場合は、Windows で問題が検出されない、有効にします。 そのため、デバッグ中にのみ、この設定を使用して、デバッグが完了した後、元の値に、レジストリ キーを返すください。

### <a name="span-idisolating-the-servicespanspan-idisolatingtheservicespan-isolating-the-service"></a><span id="isolating-the-service"></span><span id="ISOLATING_THE_SERVICE"></span> サービスを分離します。

場合によっては、複数のサービスは、1 つのサービス ホスト (Svchost) プロセスで結合されます。 このようなサービスをデバッグする場合は、まず別の Svchost プロセスに切り離す必要があります。

サービスを特定できる 3 つの方法はあります。 Microsoft は、移行をお勧めします。 次のように、そのメソッドのグループを作成するサービス。 (サービスの種類を変更して、SvcHost バイナリを複製する)、他の方法は、デバッグについては、一時的に使用できますが、最初の方法として、信頼性の高いため、サービスの実行方法を変更することはできません。

**推奨される方法:サービスを独自のグループに移動します。**

1.  次のサービス構成ツール (Sc.exe) コマンドを発行場所*ServiceName*サービスの名前を指定します。

    ```console
    sc qc ServiceName 
    ```

    これには、サービスの現在の構成値が表示されます。 目的の値はバイナリ\_パス\_名前は、サービス コントロールのプログラムを起動するために使用するコマンドラインを指定します。 このシナリオで、サービスがまだ、分離できないためこのコマンドラインが含まれていますディレクトリ パス、Svchost.exe、およびグループ名が続く、-k スイッチを含む、いくつかの SvcHost パラメーター。 たとえば、この値がこのようになります。

    ```console
    %SystemRoot%\System32\svchost.exe -k LocalServiceNoNetwork 
    ```

    このパスと、グループの名前に注意してください。手順 5 と 6 で使用されます。

2.  次のレジストリ キーを探します。

    ```text
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\SvcHost 
    ```

    新しいレジストリの作成\_マルチ\_SZ 値に一意の名前 (たとえば、**新しく作成した TempGrp**)。

3.  この新しい値を分離するサービスの名前に設定します。 任意のディレクトリ パスまたはファイル名拡張子を含めないでください。 たとえば、新しい値を設定する可能性があります**新しく作成した TempGrp**等しく**MyService**します。

4.  同じレジストリ キーの下には、手順 2. で使用する同じ名前の新しいキーを作成します。 次に、例を示します。

    ```text
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\SvcHost\TempGrp 
    ```

    ここで SvcHost キーは、新しい名前を持つ値が含まれていて、この同じ名前の下位のキーがあります。

5.  下位手順 1 で見つかったグループと同じ名前を持つ SvcHost キーに別のキーを探します。 このようなキーが存在する場合でのすべての値を確認し、手順 4. で作成した新しいキーでそれらの複製を作成します。

    たとえば、古いキー名前この。

    ```text
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\SvcHost\LocalServiceNoNetwork 
    ```

    値など、含まれると**CoInitializeSecurityParam**、 **AuthenticationCapabilities**、およびその他の値。 新しく作成したキーには。

    ```text
    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\SvcHost\TempGrp 
    ```

    以前のキーの名前、種類、およびデータでも同じですが、値を作成する.

    古いキーが存在しない場合は、新しいキーを作成する必要はありません。

6.  手順 1 で見つかったパスを変更するのにには、次のサービス構成ツールのコマンドを使用します。

    ```console
    sc config ServiceName binPath= "RevisedPath" 
    ```

    このコマンドで、 *ServiceName* 、サービスの名前を指定し、 *RevisedPath*のバイナリを指定している新しい値は、\_パス\_名。 *RevisedPath*、同一のパスを使用して、手順 1 (1 つだけの変更を行った、その行に表示されるすべてのオプションを含む) に表示される 1 つとして: した新しいレジストリ値の名前を持つスイッチ、-k を次のパラメーターの置換手順 2. で作成します。 囲む*RevisedPath*引用符で囲んで指定します。 等号の後のスペースが必要です。

    たとえば、コマンドは、次のようになります可能性があります。

    ```console
    sc config MyService binPath= "%SystemRoot%\System32\svchost.exe -k TempGrp" 
    ```

    使用することがあります、 **sc qc**対して行った変更を確認するには、もう一度コマンド。

これらの設定は、サービスが開始されて、次回に有効になります。 古いサービスの効果をクリアするをお勧め Windows を再起動するサービスを再起動するだけではなく。

完了した後にデバッグを使用して、共有サービス ホストにこのサービスを返す場合、 **sc config**キーし、する値を元の値にバイナリのパスを返し、新しいレジストリの削除をもう一度コマンド作成するには.

**別の方法:サービスの種類を変更します。**

1.  次のサービス構成ツール (Sc.exe) コマンドを発行場所*ServiceName*サービスの名前を指定します。

    ```console
    sc config ServiceName type= own 
    ```

    等号の後のスペースが必要です。

2.  次のコマンドを使用して、サービスを再起動します。
    ```console
    net stop ServiceName 
    net start ServiceName 
    ```

この方法は、サービスの動作を変更できるため、推奨される方法ではありません。 このメソッドを使用する場合は、デバッグを行った後、通常の動作に戻すには、次のコマンドを使用します。

```console
sc config ServiceName type= share 
```

**別の方法:SvcHost バイナリを複製します。**

1.  Windows の system32 ディレクトリには、Svchost.exe の実行可能ファイルにあります。 このファイルのコピーを行い、svhost2.exe という名前を付けます system32 ディレクトリにも配置します。

2.  次のサービス構成ツール (Sc.exe) コマンドを発行場所*ServiceName*サービスの名前を指定します。

    ```console
    sc qc ServiceName 
    ```

    このコマンドは、サービスの現在の構成値を表示します。 目的の値はバイナリ\_パス\_名前は、サービス コントロールのプログラムを起動するために使用するコマンドラインを指定します。 このシナリオで、サービスがまだ、分離できないために、このコマンド ライン ディレクトリ パス、Svchost.exe、およびいくつかのパラメーターの SvcHost おそらく含まれます。 たとえば、この値がこのようになります。

    ```console
    %SystemRoot%\System32\svchost.exe -k LocalServiceNoNetwork 
    ```

3.  このパスを変更するには、次のコマンドを発行します。

    ```console
    sc config ServiceName binPath= "RevisedPath" 
    ```

    このコマンドで、 *ServiceName* 、サービスの名前を指定し、 *RevisedPath*のバイナリを指定している新しい値は、\_パス\_名。 *RevisedPath*、同一のパスを使用して、手順 2、1 つだけの変更を行った、その行に表示されるすべてのオプションを含むに表示される 1 つとして: Svchost2.exe で Svchost.exe を置き換えます。 囲む*RevisedPath*引用符で囲んで指定します。 等号の後のスペースが必要です。

    たとえば、コマンドは、次のようになります可能性があります。

    ```console
    sc config MyService binPath= "%SystemRoot%\System32\svchost2.exe -k LocalServiceNoNetwork" 
    ```

    使用することができます、 **sc qc**対して行った変更を確認するには、もう一度コマンド。

4.  次のコマンドを使用して、サービスを再起動します。
    ```console
    net stop ServiceName 
    net start ServiceName 
    ```

この方法は、サービスの動作を変更できるため、推奨される方法ではありません。 このメソッドを使用する場合は、使用、 **sc config**にデバッグを行った後、その元の値にパスを変更するコマンド。

 

 





