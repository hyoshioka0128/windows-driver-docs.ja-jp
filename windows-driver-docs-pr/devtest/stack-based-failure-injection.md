---
title: スタック ベースのエラー挿入
description: スタックベースのエラー挿入オプションにより、カーネルモードドライバーにリソースエラーが挿入されます。
ms.assetid: B5C06413-81FB-46DA-B053-80ED347DA3EB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 942ec9c93cb2435873c18beb9f23701a53c85f64
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839317"
---
# <a name="stack-based-failure-injection"></a>スタック ベースのエラー挿入


**注**  この機能を有効にする手順は、Windows 8 用の WDK にのみ適用されます。 Windows 8.1 の場合、この機能はドライバー検証ツールに統合されています。 Windows 8.1 を実行しているコンピューターでは、[[体系的なリソース不足] シミュレーション](systematic-low-resource-simulation.md)オプションを使用します。

 

スタックベースのエラー挿入オプションにより、カーネルモードドライバーにリソースエラーが挿入されます。 このオプションは、特別なドライバーである KmAutoFail.sys と[ドライバー検証ツール](driver-verifier.md)を使って、ドライバーのエラー処理パスに入り込みます。 これらのパスのテストは、従来、非常に困難でした。 スタックベースのエラー挿入オプションでは、予測可能な方法でリソースエラーが挿入されます。これにより、再現可能な問題が検出されます。 エラーパスは再現しやすいので、これらの問題の修正を簡単に確認することもできます。

エラーの根本原因を特定するのに役立つように、デバッガー拡張機能が用意されており、どのようなエラーが挿入されているかを正確に知ることができます。

特定のドライバーでスタックベースの失敗の挿入オプションが有効になっている場合は、そのドライバーからカーネルと Ndis に対して一部の呼び出しがインターセプトされます。 スタックベースのエラー挿入では、呼び出し履歴 (特に、有効になっているドライバーからの呼び出し履歴の部分) が参照されます。 このスタックが初めて見られたときは、その呼び出しのセマンティクスに従って呼び出しが失敗します。 それ以外の場合は、それより前にが呼び出された場合は、それをそのまま渡します。 スタックベースのエラー挿入には、ドライバーを何度も読み込んでアンロードできるという事実を処理するロジックが含まれています。 ドライバーが別のメモリ位置に再読み込みされた場合でも、呼び出し履歴は同じであることが認識されます。

## <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブにする


[テストコンピューターにドライバーを展開](https://docs.microsoft.com/windows-hardware/drivers)するときに、1つまたは複数のドライバーに対して、スタックベースの失敗挿入機能をアクティブにすることができます。 [ドライバーパッケージプロジェクトのドライバーの検証ツールのプロパティ](https://docs.microsoft.com/windows-hardware/drivers)を構成するときに、[スタックベースの失敗の挿入] オプションを選択できます。 スタックベースのエラー挿入オプションをアクティブ化または非アクティブ化するには、コンピューターを再起動する必要があります。 テストユーティリティを実行して、テストコンピューターでドライバー検証機能とこの機能を有効にすることもできます。

**重要**  テストコンピューターでスタックベースのエラー挿入を有効にする場合は、[[低リソースシミュレーション](low-resources-simulation.md)] も選択しないようにしてください。

 

-   **[Driver Verifier] プロパティページの使用**

    1.  ドライバー パッケージのプロパティ ページを開きます。 **ソリューションエクスプローラー**でドライバーパッケージプロジェクトを右クリックし、 **[プロパティ]** を選択します。
    2.  ドライバーパッケージのプロパティページで、 **[構成プロパティ]** をクリックし、 **[ドライバーのインストール]** をクリックして、 **[ドライバーの検証ツール]** をクリックします。
    3.  **[ドライバーの検証を有効にする]** を選択します。 テストコンピューターでドライバーの検証を有効にすると、コンピューター上のすべてのドライバー、ドライバープロジェクトのみ、または指定したドライバーの一覧に対して、ドライバーの検証を有効にすることができます。
    4.  **スタックベースの失敗インジェクター** で、スタックベースの失敗の挿入 を選択します。
    5.  **[適用]** または **[OK]** をクリックします。
    6.  詳細については、「[テストコンピューターへのドライバーの展開](https://docs.microsoft.com/windows-hardware/drivers)」を参照してください。 このオプションをアクティブにするには、テストコンピューターを再起動する必要があります。
-   **ドライバー検証ツールテストの有効化と無効化の使用**

    1.  ユーティリティテストを実行して、ドライバーの検証機能を有効にすることもできます。 「[実行時に Visual Studio を使用してドライバーをテストする方法](https://docs.microsoft.com/windows-hardware/drivers)」で説明されている手順に従います。 [**すべてのテスト\\ドライバーの検証ツール**のテスト] カテゴリで、 **[ドライバーの検証ツールを有効にする (再起動が必要)]** を選択し、 **[ドライバーの検証ツール (再起動が必要]** な場合) テストを無効にします。
    2.  ドライバーの**テストグループ**ウィンドウで、[ドライバーの**検証ツールを有効にする (再起動が必要な場合)** ] テストの名前をクリックして、ドライバーの検証ツールのオプションを選択します。
    3.  スタックベースの失敗の挿入を選択 (チェック) します。
    4.  テストグループにこれらのテストを追加した後、テストグループを保存できます。 スタックベースのエラー挿入を有効にするには、テスト用に構成したコンピューターで、[**ドライバーの検証ツールを有効にする (再起動が必要な**場合があります)] テストを実行します。

        ドライバーの検証ツールを非アクティブ化するには、 **[ドライバーの検証ツールを無効にする (再起動が必要)]** テストを実行します。

## <a name="span-idusing_the_stack_based_failure_injection_optionspanspan-idusing_the_stack_based_failure_injection_optionspanspan-idusing_the_stack_based_failure_injection_optionspanusing-the-stack-based-failure-injection-option"></a><span id="Using_the_Stack_Based_Failure_Injection_option"></span><span id="using_the_stack_based_failure_injection_option"></span><span id="USING_THE_STACK_BASED_FAILURE_INJECTION_OPTION"></span>スタックベースの失敗挿入オプションの使用


スタックベースのエラー挿入を使用してテストする場合の重要な考慮事項の1つは、検出されたほとんどのバグがバグチェックになることです。 これにより、ドライバーがブートで読み込まれたドライバーである場合に多少の負担が生じる可能性があります。 このため、ドライバーの検証ツールが無効になっている場合は、自動的にスタックベースのエラーの挿入を無効にします。 これは、コマンド **! verifier-disable**を使用してドライバーの検証を無効にすることで、起動時に起動時にスタックベースのエラーの挿入を無効にできることを意味します。

可能であれば、スタックベースのエラー挿入を含む初期テストでは、ブート時に読み込まれないようにドライバーを設定します。 その後、いくつかの単純なロードテストとアンロードテストを実行できます。 スタックベースのエラー挿入によって検出されたバグの多くは、初期化またはクリーンアップ中に発生します。 ドライバーを繰り返し読み込んでアンロードすることは、これらを見つけるのに適した方法です。

ロードアンロードテストを成功させるために必要な修正を行った後は、IOCTL ベースのテスト、完全な機能テスト、および最終的なストレステストに進むことができます。 一般に、このテストの進行に従う場合は、コードパスのほとんどが既に実行されているため、ストレステスト中に多くの新しい問題が明らかになることはありません。

## <a name="span-idusing_the_stack_based_failure_injection__sbfi__debugger_extensionspanspan-idusing_the_stack_based_failure_injection__sbfi__debugger_extensionspanspan-idusing_the_stack_based_failure_injection__sbfi__debugger_extensionspanusing-the-stack-based-failure-injection-sbfi-debugger-extension"></a><span id="Using_the_Stack_Based_Failure_Injection__SBFI__debugger_extension"></span><span id="using_the_stack_based_failure_injection__sbfi__debugger_extension"></span><span id="USING_THE_STACK_BASED_FAILURE_INJECTION__SBFI__DEBUGGER_EXTENSION"></span>スタックベースのエラー挿入 (SBFI) デバッガー拡張機能の使用


スタックベースのエラー挿入で見つかった問題のほとんどは、バグチェックになります。 これらのコードバグの原因を特定するために、WDK はスタックベースのエラー挿入デバッガー拡張機能と必要なシンボルを提供します。 インストール手順は、両方ともデバッガーシステムにインストールされます。 既定の場所は C:\\Program Files (x86)\\Windows Kit\\8.0\\デバッガー\\ *&lt;arch&gt;* です。

**デバッガー拡張機能を実行するには**

- デバッガーのコマンドプロンプトで、次のコマンドを入力**します。** <em>&lt;パス&gt;\\</em> **kmautofaildbg。 autofail**. たとえば、デバッガー拡張が c:\\dbgext にインストールされていて、kmautofail がシンボルパスにあると仮定すると、次のコマンドを入力します。

  ```
  !c:\dbgext\kmautofaildbg.dll.autofail
  ```

これにより、最新のエラーが挿入された呼び出し履歴を示す情報がデバッガーにダンプされます。 各エントリは、実際のテストの実行から取得された次のようになります。 次の例では、Mydriver. sys でスタックベースのエラー挿入が有効になっています。

```
Sequence: 2, Test Number: 0, Process ID: 0, Thread ID: 0
                 IRQ Level: 2, HASH: 0xea98a56083aae93c
 0xfffff8800129ed83 kmautofail!ShimHookExAllocatePoolWithTag+0x37
 0xfffff88003c77566 mydriver!AddDestination+0x66
 0xfffff88003c5eeb2 mydriver!ProcessPacketDestination+0x82
 0xfffff88003c7db82 mydriver!ProcessPacketSource+0x8b2
 0xfffff88003c5d0d8 mydriver!ForwardPackets+0xb8
 0xfffff88003c81102 mydriver!RoutePackets+0x142
 0xfffff88003c83826 mydriver!RouteNetBufferLists+0x306
 0xfffff88003c59a76 mydriver!DeviceSendPackets+0x156
 0xfffff88003c59754 mydriver!ProcessingComplete+0x4a4
 0xfffff88001b69b81 systemdriver2!ProcessEvent+0x1a1
 0xfffff88001b3edc4 systemdriver1!CallChildDriver+0x20
 0xfffff88001b3fc0a systemdriver1!ProcessEvent+0x3e
 0xfffff800c3ea6eb9 nt!KiRetireDpcList+0x209
 0xfffff800c3ea869a nt!KiIdleLoop+0x5a
```

出力の先頭にあるシーケンス番号は、挿入されたエラーの数をカウントします。 この例は、このテストの実行中に挿入された2番目のエラーを示しています。 プロセス ID は0であるため、これはシステムプロセスです。 IRQL は2であるため、ディスパッチレベルで呼び出されます。

スタックから、KmAutoFail はスタックベースの障害注入ドライバーです。 KmAutoFail 関数名は、Mydriver からの関数呼び出しがインターセプトされ、エラーが挿入されたことを示します。 ここでは、失敗した関数は[**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)でした。 KmAutoFail のすべての関数は、Ntoskrnl.exe または Ndis の呼び出しをインターセプトして、この名前付け規則を使用します。 次に、テスト対象のドライバー (Mydriver .sys) を含むコールスタックが表示されます。 これは、スタックの一意性を判断するために使用される呼び出し履歴の部分です。 このため、デバッガー拡張機能によってダンプされた各エントリは、呼び出し履歴のこの部分で一意になります。 呼び出し履歴の残りの部分は、ドライバーを呼び出したユーザーを示します。 この重要な重要な点は、ドライバーが (IOCTL によって) ユーザーモードから呼び出されるか、カーネルモードドライバーから呼び出されるかということです。

ドライバーが[*Driverentry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンからエラーを返した場合、通常は別のメモリ位置で再読み込みが試行されることに注意してください。 この場合、以前の場所のコールスタックには、ドライバーからのスタック情報ではなく、"ガーベジ" が含まれていることがあります。 ただし、これは問題ではありません。これは、ドライバーが挿入されたエラーを正しく処理したことを示します。

次のエントリは、ユーザーモードからの IOCTL によってドライバーが呼び出されることを示しています。 プロセス ID と IRQ レベルをメモしておきます。 Mydriver は NDIS フィルタードライバーであるため、IOCTL が使用されていました。 Nt!NtDeviceIoControlFile はスタック上にあります。 Ioctl を使用するドライバーで実行するすべてのテストは、この関数を経由します。

```
Sequence: 5, Test Number: 0, Process ID: 2052, Thread ID: 4588
                 IRQ Level: 0, HASH: 0xecd4650e9c25ee4
 0xfffff8800129ed83 kmautofail!ShimHookExAllocatePoolWithTag+0x37
 0xfffff88003c6fb39 mydriver!SendMultipleOids+0x41
 0xfffff88003c7157b mydriver!PvtDisconnect+0x437
 0xfffff88003c71069 mydriver!NicDisconnect+0xd9
 0xfffff88003ca3538 mydriver!NicControl+0x10c
 0xfffff88003c99625 mydriver!DeviceControl+0x4c5
 0xfffff88001559d93 NDIS!ndisDummyIrpHandler+0x73
 0xfffff88001559339 NDIS!ndisDeviceControlIrpHandler+0xc9
 0xfffff800c445cc96 nt!IovCallDriver+0x3e6
 0xfffff800c42735ae nt!IopXxxControlFile+0x7cc
 0xfffff800c4274836 nt!NtDeviceIoControlFile+0x56
 0xfffff800c3e74753 nt!KiSystemServiceCopyEnd+0x13
```

## <a name="span-idanalyzing_the_results_of_stack_based_failure_injectionspanspan-idanalyzing_the_results_of_stack_based_failure_injectionspanspan-idanalyzing_the_results_of_stack_based_failure_injectionspananalyzing-the-results-of-stack-based-failure-injection"></a><span id="Analyzing_the_results_of_Stack_Based_Failure_Injection"></span><span id="analyzing_the_results_of_stack_based_failure_injection"></span><span id="ANALYZING_THE_RESULTS_OF_STACK_BASED_FAILURE_INJECTION"></span>スタックベースの失敗の挿入の結果を分析する


お使いのドライバーでテストを実行しています。突然問題が発生しています。 多くの場合、これはバグチェックでしたが、コンピューターが応答しなくなったことが原因である可能性もあります。 原因を見つけるにはどうすればよいですか。 バグチェックであると仮定した場合は、最初に上記の拡張機能を使用して、挿入されたエラーの一覧を見つけ、デバッガーコマンド: **! analyze – v**を使用します。

最も一般的なバグチェックは、割り当てが成功したかどうかをチェックしないことによって発生します。 この場合、バグチェック分析のスタックは、挿入された最後のエラーのスタックとほぼ同じであると考えられます。 失敗した割り当て (多くの場合、次の行) の後のある時点で、ドライバーは null ポインターにアクセスします。 この種のバグは、非常に簡単に修正できます。 失敗した割り当てが一覧の1つまたは2つ上にある場合もありますが、この種類の検索と修正は非常に簡単です。

2番目の最も一般的なバグチェックは、クリーンアップ中に発生します。 この場合、ドライバーは割り当てエラーを検出し、クリーンアップにジャンプしました。しかし、クリーンアップ中に、ドライバーはポインターを確認せず、再び null ポインターにアクセスしました。 密接に関連したケースでは、クリーンアップを2回呼び出すことができます。 解放した後に、クリーンアップが構造体へのポインターを null に設定しなかった場合、2回目のクリーンアップ関数が呼び出されると、その構造はもう一度解放され、バグチェックが行われます。

コンピューターが応答しなくなる原因となるエラーは診断が困難ですが、デバッグの手順は似ています。 これらのエラーは、多くの場合、参照カウントまたはスピンロックの問題が原因で発生します。 幸いなことに、[ドライバーの検証ツール](driver-verifier.md)では、問題が発生する前に、多くのスピンロックの問題が検出されます。 このような場合は、デバッガーを中断し、デバッガー拡張機能を使用して、スタックベースのエラー挿入によって挿入されたエラーの一覧をダンプします。 最新のエラーのコードを簡単に確認すると、エラーが発生する前に、の後に解放されない参照カウントが表示される場合があります。 それ以外の場合は、スピンロックを待機している、または明らかに間違っている参照カウントに対して、ドライバー内のスレッドを探します。

 

 





