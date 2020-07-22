---
title: ドライバー検証ツールでの特殊なプールメモリ破損検出
description: メモリの破損を検出するために、ドライバーの検証ツールは特殊なプールからドライバーのメモリを割り当て、そのプールを監視して不正なアクセスを防ぐことができます。
ms.assetid: b1381a75-279a-42b7-b18d-43aba796424b
keywords:
- 特別なプール機能 WDK ドライバー検証ツール
- メモリ破損 WDK ドライバー検証ツール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff0e87f3ee7169c6ebdc204326bcc7791e7020a9
ms.sourcegitcommit: 3ec971f54122b77408433f7f1e59c467099fb4de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/21/2020
ms.locfileid: "86873871"
---
# <a name="special-pool-memory-corruption-detection-in-driver-verifier"></a>ドライバー検証ツールでの特殊なプールメモリ破損検出

メモリの破損は、一般的なドライバーの問題です。 ドライバーエラーが発生すると、エラーが発生した後にクラッシュすることがあります。 これらのエラーの最も一般的な部分は、既に解放されているメモリにアクセスし、 *n*バイトを割り当ててから*n*+ 1 バイトにアクセスすることです。

メモリの破損を検出するために、ドライバーの検証ツールは特殊なプールからドライバーのメモリを割り当て、そのプールを監視して不正なアクセスを防ぐことができます。 特別なプールのサポートは、 [**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)などのカーネルモードシステム提供のルーチンや、 [**ENGALLOCMEM**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engallocmem)などの GDI システム提供のルーチンに対して提供されます。

特別なプールの2つのアラインメントを使用できます。 **検証の終了**アラインメントは、アクセスオーバーランの検出に適しています。また、**検証の開始**アラインメントは、アクセスアンダーランの検出に適しています。 (メモリの破損の大部分は、アンダーランではなくオーバーランによるものであることに注意してください)。

特別なプール機能がアクティブになっていて、[ **End** ] が選択されている場合、ドライバーによって要求された各メモリ割り当てが別のページに配置されます。 ページに合わせて割り当てを可能にする最大のアドレスが返されます。これにより、ページの末尾にメモリが配置されます。 ページの前の部分は特殊なパターンで記述されています。 前のページと次のページにはアクセスできないとマークされています。

ドライバーが割り当ての終了後にメモリにアクセスしようとすると、ドライバーの検証ツールはこれをすぐに検出し、[**バグチェック 0xCD**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xcd--page-fault-beyond-end-of-allocation)を発行します。 ドライバーがバッファーの先頭より前にメモリを書き込んだ場合は、パターンが変更されることがあります。 バッファーが解放されると、ドライバー検証ツールは変更を検出し、[**バグチェック 0xC1**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xc1--special-pool-detected-memory-corruption)を発行します。

ドライバーが解放された後に、そのバッファーの読み取りまたは書き込みを実行すると、ドライバーの検証ツールによって[**バグチェック 0xCC**](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xcc--page-fault-in-freed-special-pool)が発行されます。

[**開始の確認**] を選択すると、メモリバッファーはページの先頭に合わせて調整されます。 この設定では、アンダーランによって即時のバグチェックが発生し、オーバーランによってメモリが解放されるとバグチェックが発生します。 このオプションは、それ以外の場合は、[**終了の確認**] オプションと同じです。

[終了] が既定の配置である**ことを確認**します。これは、オーバーランエラーよりもドライバーでオーバーランエラーがはるかに一般的になるためです。

個々のメモリ割り当てでは、これらの設定を上書きして、*優先順位*パラメーターを xxx に設定して[**Exallocatepoolwithtagpriority**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtagpriority)を呼び出すことによって、その配置を選択できます。 (このルーチンでは、特別なプール機能をアクティブ化または非アクティブ化したり、メモリ割り当て用に特別なプールを要求したりすることはできません。この場合、通常のプールから割り当てられます。 このルーチンから制御できるのはアラインメントだけです)。

Windows 7 以降のバージョンの Windows オペレーティングシステムでは、特別なプールオプションは、次のカーネル Api を使用して割り当てられたメモリをサポートしています。

-   [**IoAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl)

-   [**Ioallocateirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)および i/o 要求パケット (IRP) データ構造を割り当てることができる他のルーチン

-   [**RtlAnsiStringToUnicodeString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlansistringtounicodestring)およびその他のランタイムライブラリ (RTL) 文字列ルーチン

-   [**IoSetCompletionRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)

### <a name="span-idspecial_pool_by_pool_tag_or_allocation_sizespanspan-idspecial_pool_by_pool_tag_or_allocation_sizespanspecial-pool-by-pool-tag-or-allocation-size"></a><span id="special_pool_by_pool_tag_or_allocation_size"></span><span id="SPECIAL_POOL_BY_POOL_TAG_OR_ALLOCATION_SIZE"></span>プールタグまたは割り当てサイズ別の特別なプール

特定の*ドライバー*による割り当てに特別なプールを要求する driver Verifier の特別なプール機能に加えて、特殊なプールを使用するには、次の2つの方法があります。

-   **プールタグ。** 指定されたプールタグを持つすべての割り当てに対して、特別なプールを要求します。

-   **幅.** 指定されたサイズ範囲内のすべての割り当てに対して、特別なプールを要求します。

プールタグまたはサイズ範囲に特別なプールを要求するには、 *Windows 用デバッグツール*に含まれている Gflags ツールを使用します。 詳細については、「[グローバルフラグユーティリティの使用](using-the-global-flags-utility.md)」を参照してください。

ドライバー検証ツールの特別なプール機能と、Gflags の特別なプール機能を同時に使用することができます。 特別なプールが制限されているのに、特別なプールからの割り当てが成功するわけではなく、通常のメモリプールからの割り当てによって満たされた特殊なプールからの割り当てに失敗した場合の成功の状態が返されることに注意してください。

### <a name="span-idspecial_pool_efficiencyspanspan-idspecial_pool_efficiencyspanspecial-pool-efficiency"></a><span id="special_pool_efficiency"></span><span id="SPECIAL_POOL_EFFICIENCY"></span>特別なプールの効率性

すべての特別なプール要求が満たされているわけではありません。 特別なプールからの各割り当てでは、非ページング物理メモリの1ページと仮想アドレス空間の2つのページが使用されます。 プールが使い果たされると、特別なプールが再び使用可能になるまで、メモリは標準の方法で割り当てられます。 特別なプール要求が標準プールから入力された場合、要求元の関数はエラーを返しません。これは、プール要求が成功したためです。 したがって、特別なプール機能がアクティブ化されている場合は、複数のドライバーを同時に検証することはお勧めしません。

多数の小さなメモリ要求を実行する1つのドライバーによっても、このプールが消費される可能性があります。 この問題が発生した場合は、ドライバーのメモリ割り当てにプールタグを割り当て、一度に1つのプールタグに専用のプールを割り当てることをお勧めします。

特別なプールのサイズは、システムの物理メモリの量によって増加します。理想的には、1 Gb 以上である必要があります。 X86 コンピューターでは、仮想 (物理ディスクに加えて) 領域が消費されるため、 [**/3gb**](https://docs.microsoft.com/windows-hardware/drivers/devtest/boot-3gb)ブートオプションは使用しないでください。 また、ページファイルの最小/最大数を 2 ~ 3 の係数で増やすことをお勧めします。

すべてのドライバーの割り当てがテストされていることを確認するには、長い時間をかけてドライバーをストレスすることをお勧めします。

### <a name="span-idmonitoring_the_special_poolspanspan-idmonitoring_the_special_poolspanmonitoring-the-special-pool"></a><span id="monitoring_the_special_pool"></span><span id="MONITORING_THE_SPECIAL_POOL"></span>特別なプールの監視

プール割り当てに関連する統計を監視できます。 これらは、ドライバー検証マネージャー、Verifier.exe コマンドライン、またはログファイルで表示できます。 詳細については、「[グローバルカウンターの監視](monitoring-global-counters.md)」を参照してください。

"**特殊**なプールの割り当てが成功しました" というカウンターが "プールの割り当てに成功しました **" カウンターと**等しい場合は、特別なプールによってすべてのメモリの割り当てを処理できます。 前者のカウンターが後者より小さい場合は、特別なプールが少なくとも1回使い果たされています。

これらのカウンターは、サイズが1ページ以上の割り当てを追跡しません。これは、特殊なプールが適用されないためです。

特別なプール機能が有効になっていても、すべてのプール割り当ての95% 未満が特別なプールから割り当てられている場合は、ドライバー検証マネージャーに警告が表示されます。 Windows 2000 では、この警告はドライバーの**ステータス**画面に表示されます。 Windows XP 以降では、この警告は [**グローバルカウンター** ] 画面に表示されます。 この問題が発生した場合は、短いドライバーの一覧を確認し、プールタグによって個々のプールを確認するか、システムに物理メモリを追加します。

カーネルデバッガー拡張機能の**検証ツール**は、特別なプールの使用を監視するためにも使用できます。 ドライバー検証ツールマネージャーと同様の情報が表示されます。 デバッガー拡張機能の詳細については、「 [Windows デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/index)」を参照してください。

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブにする

ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して、1つまたは複数のドライバーの特別なプール機能をアクティブ化できます。 詳細については、「[ドライバーの検証オプションの選択](selecting-driver-verifier-options.md)」を参照してください。

**メモ**   プールタグまたは割り当てサイズによって特別なプール機能をアクティブ化したり、[**開始の確認**] (アンダーランの検出) と [End (オーバーランの検出)] の配置を**確認**したりするには、[グローバルフラグユーティリティ](using-the-global-flags-utility.md)を使用します。これらの配置設定は、すべての特別なプール割り当てに適用されます。

 

-   **コマンドラインで**

    コマンドラインでは、特殊なプールオプションは**ビット 0 (0x1)** で表されます。 特別なプールをアクティブ化するには、フラグ値0x1 を使用するか、フラグ値に0x1 を追加します。 次に例を示します。

    ```
    verifier /flags 0x1 /driver MyDriver.sys
    ```

    この機能は、次回の起動時にアクティブになります。

    Windows 2000 以降のバージョンの Windows では、 **/volatile**パラメーターをコマンドに追加することで、コンピューターを再起動しなくても、特別なプールのアクティブ化と非アクティブ化を行うことができます。 次に例を示します。

    ```
    verifier /volatile /flags 0x1 /adddriver MyDriver.sys
    ```

    この設定は直ちに有効になりますが、コンピューターをシャットダウンまたは再起動すると失われます。 詳細については、「 [Volatile 設定の使用](using-volatile-settings.md)」を参照してください。

    特別なプール機能は、標準設定にも含まれています。 次に例を示します。

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **ドライバー検証マネージャーの使用**

    1.  [**カスタム設定の作成] (コード開発者向け)** を選択し、[**次へ**] をクリックします。
    2.  [**完全な一覧から個々の設定を選択]** を選択します。
    3.  [**特殊なプール**] を選択します。

    特別なプール機能は、標準設定にも含まれています。 この機能を使用するには、ドライバー検証マネージャーで [**標準設定の作成**] をクリックします。

 

 





