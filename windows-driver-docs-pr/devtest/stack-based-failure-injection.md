---
title: スタック ベースのエラー挿入
description: スタック ベースのエラー挿入オプションは、カーネル モード ドライバーにリソース エラーを挿入します。
ms.assetid: B5C06413-81FB-46DA-B053-80ED347DA3EB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d275e9327ee6ae827645baabb595ce1180c4d040
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379037"
---
# <a name="stack-based-failure-injection"></a>スタック ベースのエラー挿入


**注**  この機能を有効にする手順については、Windows 8 の WDK にのみ適用されます。 Windows 8.1 では、この機能を Driver Verifier に統合されています。 Windows 8.1 を実行するコンピューターでを使用して、[体系的な低リソース シミュレーション](systematic-low-resource-simulation.md)オプション。

 

スタック ベースのエラー挿入オプションは、カーネル モード ドライバーにリソース エラーを挿入します。 このオプションは、特別なドライバーである KmAutoFail.sys と[ドライバー検証ツール](driver-verifier.md)を使って、ドライバーのエラー処理パスに入り込みます。 これらのパスをテスト歴史的非常に困難です。 スタック ベースのエラー挿入オプションは、検出した再現可能な問題により、予測可能な方法でリソースの障害を挿入します。 エラー パスは、簡単に再現できますであるためにも簡単にこれらの問題の修正を確認します。

エラーの根本原因を特定するために、デバッガーの拡張機能は、挿入されているどのエラー正確に知ることができ、どのような順序で。

スタック ベースのエラー挿入オプションが特定のドライバーに対して有効な場合は、ドライバーからカーネルと Ndis.sys へのいくつかの呼び出しを受け取ります。 スタック ベースのエラー挿入が呼び出し履歴を調べ、具体的には、有効にするか、ドライバーに由来する呼び出しスタックの一部でします。 そのスタックを見たことも、初めての場合は、その呼び出しのセマンティクスに従って呼び出しは失敗します。 それ以外の場合、前に呼び出すことが示された場合、手を加えずを通過にされます。 スタック ベースのエラー挿入には、ドライバーのロードし、複数回をアンロードするという事実を処理するロジックが含まれています。 呼び出し履歴が同じである場合でも、別のメモリ位置に、ドライバーが再読み込みが認識されます。

## <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="Activating_this_option"></span><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブ化します。


スタック ベースのエラー挿入の機能の 1 つまたは複数のドライバーをアクティブ化することができます[テスト コンピューターにドライバーを展開する](https://docs.microsoft.com/windows-hardware/drivers)します。 スタック ベースのエラー挿入オプションを選択するには、構成するときに、[ドライバー パッケージのプロジェクトの Driver Verifier プロパティ](https://docs.microsoft.com/windows-hardware/drivers)します。 スタック ベースのエラー挿入オプションをアクティブ化またはコンピューターを再起動する必要があります。 ドライバーの検証とテスト コンピューターでこの機能を有効にするためのテスト ユーティリティを実行することもできます。

**重要な**  スタック ベースのエラー挿入をテスト コンピューターでアクティブ化するとことを確認しても選択しない[低リソース シミュレーション](low-resources-simulation.md)します。

 

-   **Driver Verifier のプロパティ ページを使用してください。**

    1.  ドライバー パッケージのプロパティ ページを開きます。 ドライバー パッケージのプロジェクトを右クリックして**ソリューション エクスプ ローラー**選択と**プロパティ**。
    2.  ドライバ パッケージのプロパティ ページで次のようにクリックします。**構成プロパティ**、 をクリック**ドライバー インストール**、順にクリックします**Driver Verifier**します。
    3.  選択**Driver Verifier を有効にする**します。 テスト コンピューターでドライバーの検証を有効にする場合にのみ、または指定したドライバーの一覧については、コンピューターのドライバーのプロジェクトのすべてのドライバーをドライバーの検証ツールを有効にすることもできます。
    4.  **スタック ベースのエラー インジェクター**、スタック ベースのエラー挿入の (チェック) を選択します。
    5.  **[適用]** または **[OK]** をクリックします。
    6.  参照してください[テスト コンピューターにドライバーを展開する](https://docs.microsoft.com/windows-hardware/drivers)詳細についてはします。 このオプションをアクティブ化するテスト コンピューターを再起動する必要があります。
-   **テストの有効化と無効にする Driver Verifier を使用**

    1.  Driver Verifier は、ユーティリティのテストを実行してもできます。 説明されている指示に従って[Visual Studio を使用して実行時にドライバーをテストする方法](https://docs.microsoft.com/windows-hardware/drivers)します。 下、**すべてのテスト\\Driver Verifier**テスト カテゴリを選択、 **Driver Verifier を有効にする」(可能な再起動が必要)** と**Driver Verifier (可能な再起動の無効にします。必要な)** テストします。
    2.  名前をクリックして、Driver Verifier のオプションを選択して、 **Driver Verifier を有効にする」(可能な再起動が必要)** でテスト、**ドライバー テスト グループ**ウィンドウ。
    3.  選択 (チェック) スタック ベースのエラー挿入します。
    4.  これらのテストをテスト グループに追加した後は、テスト グループを保存できます。 スタック ベースのエラー挿入を有効にするのには、実行、 **Driver Verifier を有効にする」(可能な再起動が必要)** テスト用に構成したコンピューターでテストします。

        Driver Verifier を非アクティブ化するには実行、 **Driver Verifier を無効にする」(可能な再起動が必要)** をテストします。

## <a name="span-idusingthestackbasedfailureinjectionoptionspanspan-idusingthestackbasedfailureinjectionoptionspanspan-idusingthestackbasedfailureinjectionoptionspanusing-the-stack-based-failure-injection-option"></a><span id="Using_the_Stack_Based_Failure_Injection_option"></span><span id="using_the_stack_based_failure_injection_option"></span><span id="USING_THE_STACK_BASED_FAILURE_INJECTION_OPTION"></span>スタック ベースのエラー挿入オプションを使用します。


1 つの重要な考慮事項とスタック ベースのエラー挿入テストするときに、バグ チェックで検出されたほとんどのバグがなります。 これをドライバーがブート読み込まれるドライバーの場合、少し厄介でした証明します。 このためが自動的に無効化スタック ベースのエラー挿入ドライバーの検証が無効になっている場合。 つまり、スタック ベースのエラー挿入コマンドを使用してドライバーの検証を無効にすると、デバッガーからのブート時に無効できます **! verifier – 無効にする**します。

可能であれば、スタック ベースのエラー挿入では、初期テスト用である場合は、ブート時に読み込まれないように、ドライバーを設定します。 いくつかの単純なロードを実行し、テストをアンロードできます。 スタック ベースのエラー挿入によって見つかったバグの多くは、初期化やクリーンアップ中に発生します。 繰り返しを読み込むと、ドライバーをアンロードは、これらを検索することをお勧めです。

負荷のために必要な修正が成功するテストのアンロード後、IOCTL ベースのテスト移動できますは機能テストでは、完全なし、最後にストレス テストします。 一般に、このテストの進行を実行する場合はしないが明らかになった多くの新しい問題ストレス テストのため、ほとんどのコード パスが既に実行されているこれまでの中に。

## <a name="span-idusingthestackbasedfailureinjectionsbfidebuggerextensionspanspan-idusingthestackbasedfailureinjectionsbfidebuggerextensionspanspan-idusingthestackbasedfailureinjectionsbfidebuggerextensionspanusing-the-stack-based-failure-injection-sbfi-debugger-extension"></a><span id="Using_the_Stack_Based_Failure_Injection__SBFI__debugger_extension"></span><span id="using_the_stack_based_failure_injection__sbfi__debugger_extension"></span><span id="USING_THE_STACK_BASED_FAILURE_INJECTION__SBFI__DEBUGGER_EXTENSION"></span>スタック ベースのエラーの挿入 (SBFI) デバッガー拡張機能の使用


ほとんどのバグでスタック ベースのエラー挿入の結果で見つかった問題を確認します。 これらのコードのバグの原因を特定するには、WDK は、拡張機能と必要なシンボルにスタック ベースのエラー挿入のデバッガーを提供します。 インストール手順は、デバッガー システムの両方にインストールされます。 既定の場所は c:\\Program Files (x86)\\Windows キット\\8.0\\デバッガー\\ *&lt;arch&gt;* します。

**デバッガーの拡張機能を実行するには**

- デバッガーのコマンド プロンプトから次のコマンドを入力: **!** <em>&lt;パス&gt;\\</em>**kmautofaildbg.dll.autofail**します。 たとえば、c: でデバッガーの拡張機能がインストールされていると仮定すると\\dbgext とその kmautofail.pdb がシンボル パスには、次のコマンドを入力します。

  ```
  !c:\dbgext\kmautofaildbg.dll.autofail
  ```

これは、デバッガーが挿入され、最新の障害からの呼び出し履歴を表示する情報がダンプされます。 各エントリは、実際のテストからの取得を実行、次のようなものを検索します。 次の例では、スタック ベースのエラー挿入は Mydriver.sys で有効に

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

出力の上部にあるシーケンス番号を注入する違反の数をカウントします。 この例では、このテストの実行中に挿入された 2 つ目のエラーを示します。 プロセス ID は、これは、システム プロセス、0 です。 IRQL は、2 は、これは、ディスパッチ レベルで呼び出されます。

スタックから KmAutoFail は、スタック ベースのエラー挿入ドライバーです。 関数名では、Mydriver.sys からどのような関数を呼び出すことを示します KmAutoFail のインターセプトされ、フォールト挿入されます。 ここでは、失敗した関数が[ **exallocatepoolwithtag に**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)します。 すべての関数 KmAutoFail Ntoskrnl.sys または Ndis.sys 切片の呼び出しがこの名前付け規則を使用します。 次に、ドライバーが呼び出し履歴のテスト (Mydriver.sys) 参照してください。 これは、スタックの一意性を特定するために使用する呼び出しスタックの一部です。 したがって、デバッガーの拡張機能によってダンプの各エントリは、コール スタックのこの部分で一意になります。 呼び出し履歴の残りの部分では、ドライバーと呼ばれるユーザーを示します。 これの主な重要度は、(IOCTL) を使用してユーザー モードまたはカーネル モード ドライバーからかどうか、ドライバーが呼び出されます。

ドライバーにエラーが返された場合に注意するその[ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)ルーチンを再読み込み試行は通常行わさまざまなメモリの場所にします。 その場合は、以前の場所からのコール スタックでは、ドライバー スタック情報ではなく「不要な」が含まれます可能性があります。 これは問題ではありませんが、ドライバーは、挿入されたエラーを正しく処理を指示します。

この次のエントリは、ユーザー モードから IOCTL を使用して、ドライバーへの呼び出しを示します。 プロセス ID と IRQ レベルに注意してください。 Mydriver.sys は、NDIS フィルター ドライバーであるため、IOCTL Ndis.sys が通過します。 注その nt!NtDeviceIoControlFile がスタック上にします。 Ioctl で使用される、ドライバーで実行する任意のテストは、この関数で移動します。

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

## <a name="span-idanalyzingtheresultsofstackbasedfailureinjectionspanspan-idanalyzingtheresultsofstackbasedfailureinjectionspanspan-idanalyzingtheresultsofstackbasedfailureinjectionspananalyzing-the-results-of-stack-based-failure-injection"></a><span id="Analyzing_the_results_of_Stack_Based_Failure_Injection"></span><span id="analyzing_the_results_of_stack_based_failure_injection"></span><span id="ANALYZING_THE_RESULTS_OF_STACK_BASED_FAILURE_INJECTION"></span>スタック ベースのエラー挿入の結果の分析


ドライバーのテストを実行して、突然問題が発生します。 バグ チェックでは、これはほとんどの場合ですが、また、コンピューターに応答しなくなったためです。 原因をどのように見つけますか。 バグ チェックが構成されている場合、まず上記の拡張機能を使用して、挿入されたエラーの一覧を検索し、デバッガー コマンドを使用して: **! 分析 – v**します。

バグの最も一般的なチェックは、割り当ての成功をオンにしない原因です。 ここでのバグ チェック分析スタックは、挿入された最後のエラーのおそらくほとんどと同じです。 失敗した割り当て (多くの場合、次の行) 後に、ある時点で、ドライバーは、null ポインターにアクセスします。 この種のバグが非常に簡単に修正できます。 失敗した割り当てが 1 つまたは 2 つのリストが場合がありますが、この型も非常に簡単に見つけて修正します。

最も一般的な 2 つ目のバグ チェックでは、クリーンアップ中に発生します。 この場合、ドライバー可能性があります割り当てエラーの検出し、クリーンアップ; にジャンプクリーンアップ中に、ドライバーがポインターを確認していないと、null ポインターをもう一度アクセスします。 密接に関連するケースは、クリーンアップを 2 回呼び出すことが場所です。 クリーンアップがこれによって解放した後に null を構造体へのポインターを設定しない場合クリーンアップ関数を呼び出す 2 回目にしようとバグ チェックでその結果、2 番目の時間構造体を解放します。

応答しなくなるとコンピューターのエラーは、診断が困難ですが、それらをデバッグする手順は似ています。 これらのエラーは、多くの場合、参照カウントによって発生またはロックの問題を作成できます。 さいわい、 [Driver Verifier](driver-verifier.md)問題につながる、前に、スピン ロック問題の多くを受け取ります。 このような場合は、スタック ベースのエラー挿入によって挿入されているエラーの一覧をダンプするデバッガー拡張機能を使用して、デバッガーを中断できます。 最新のエラーの周辺のコードを簡単に見てにでは、障害発生前に実行されるが、後に解放されない参照カウントによって表示されます。 それ以外の場合は、ドライバー、スピン ロックで待機しているスレッドか明らかに不適切であるすべての参照カウントになります。

 

 





