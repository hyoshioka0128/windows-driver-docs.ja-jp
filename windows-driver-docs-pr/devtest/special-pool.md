---
title: 特別なプール
description: 特別なプール
ms.assetid: b1381a75-279a-42b7-b18d-43aba796424b
keywords:
- 特別なプール機能 WDK Driver Verifier
- メモリの破損 WDK Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28e20ecd0216b2556780281d2af4c424c346628a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538527"
---
# <a name="special-pool"></a>特別なプール


## <span id="ddk_special_memory_pool_tools"></span><span id="DDK_SPECIAL_MEMORY_POOL_TOOLS"></span>


メモリの破損は、一般的なドライバーの問題です。 ドライバーのエラーによりクラッシュ、エラーが発生した後もあります。 これらのエラーの最も一般的なが既に解放されたメモリにアクセスして、割り当て*n*バイトとにアクセスする*n*+1 のバイト数。

メモリの破損を検出するには、Driver Verifier は特別なプールからドライバーのメモリを割り当てるし、正しくないアクセス用には、そのプールを監視できます。 特別なプールのサポートがなどのカーネル モード システム指定のルーチンに対して提供されます[ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)と GDI システム指定のルーチンのもなど[ **EngAllocMem**](https://msdn.microsoft.com/library/windows/hardware/ff564176)します。

特別なプールの 2 つの配置を利用できます。 **終了の確認**アクセスのオーバーランを検出する方が、配置、**開始を確認します**アクセス アンダーランを検出する方が、配置します。 (ある膨大なメモリの破損は、オーバーランにより、いないアンダーランに注意してください)。

特別なプール機能がアクティブな場合と**終了の確認**が選択すると、ドライバーによって要求されたメモリ割り当てが別のページに配置します。 メモリは、ページの末尾と一致するように合わせて、ページ割り当ては、最上位アドレスが返されます。 ページの前の部分は、特殊なパターンと書き込まれます。 前のページと、次のページは、アクセス不能でマークされます。

Driver Verifier がこれ、すぐに検出され、発行する場合は、ドライバーが、割り当ての終了後にメモリにアクセスしようとすると、 [**バグ チェック 0 xcd**](https://msdn.microsoft.com/library/windows/hardware/ff560219)します。 ドライバーは、バッファーの先頭の前にメモリに書き込み、これと、パターンは変更 (おそらく)。 Driver Verifier は、変更と問題を検出、バッファーが解放されると、 [**バグ チェック 0xC1**](https://msdn.microsoft.com/library/windows/hardware/ff560183)します。

Driver Verifier を発行する場合は、ドライバーに対して読み取りまたは書き込みバッファーされ、解放した後、 [**バグ チェック 0 xcc**](https://msdn.microsoft.com/library/windows/hardware/ff560216)します。

ときに**確認を開始**は選択すると、メモリ バッファーは、ページの先頭に揃えられます。 この設定でアンダーラン、即時のバグ チェックが発生して、オーバーラン バグ チェックが発生するメモリが解放されるとき。 このオプションは、それ以外の場合と同じ、**終了の確認**オプション。

**最後の確認**オーバーラン エラーはドライバーでの一般的な不足エラーよりもはるかに既定の配置が。

個々 のメモリ割り当てがこれらの設定をオーバーライドし、アラインメントを呼び出すことによって選択[ **ExAllocatePoolWithTagPriority** ](https://msdn.microsoft.com/library/windows/hardware/ff544523)で、*優先度*パラメーター セットXxxSpecialPoolOverrun または XxxSpecialPoolUnderrun します。 (このルーチンことはできませんをアクティブ化、特別なプール機能を非アクティブ化または特別なプールは、それ以外の場合通常のプールから割り当てられるメモリの割り当てを要求します。 配置のみ制御できますこのルーチンから。)

Windows 7 および Windows オペレーティング システムの以降のバージョンでは、特別なプールのオプションには、次のカーネル Api を使用して割り当てられたメモリがサポートしています。

-   [**IoAllocateMdl**](https://msdn.microsoft.com/library/windows/hardware/ff548263)

-   [**IoAllocateIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff548257)と I/O を割り当てることができるその他のルーチン要求パケット (IRP) データ構造体

-   [**RtlAnsiStringToUnicodeString** ](https://msdn.microsoft.com/library/windows/hardware/ff561729)およびその他のランタイム ライブラリ (RTL) の文字列ルーチン

-   [**IoSetCompletionRoutineEx**](https://msdn.microsoft.com/library/windows/hardware/ff549686)

### <a name="span-idspecialpoolbypooltagorallocationsizespanspan-idspecialpoolbypooltagorallocationsizespanspecial-pool-by-pool-tag-or-allocation-size"></a><span id="special_pool_by_pool_tag_or_allocation_size"></span><span id="SPECIAL_POOL_BY_POOL_TAG_OR_ALLOCATION_SIZE"></span>プールでプールの特殊なタグまたはアロケーション サイズ

によって指定された特別なプールの割り当てを要求するだけでなく、特別なプールには、Driver Verifier の機能が、*ドライバー*は特別なプールを使用するその他の 2 つの方法があります。

-   **プール タグ。** 指定されたプール タグを持つすべての割り当て用の特別なプールを要求します。

-   **サイズ。** 指定したサイズの範囲内のすべての割り当て用の特別なプールを要求します。

プールのタグまたはサイズの範囲の特別なプールを要求する Gflags に付属のツールを使用して、*ツールを Windows のデバッグ*します。 詳細については、[グローバル フラグ ユーティリティを使用して](using-the-global-flags-utility.md)を参照してください。

同時には、Driver Verifier の特別なプール機能と Gflags の特別なプール機能を使用できます。 この場合、特別なプールが制限される、特別なは、プールが成功し、Windows が通常メモリの割り当てによって満たされる特別なプールからの割り当ての失敗の回数を成功状態を返すことから割り当てることの試みがすべてないことを注意してください。プール。

### <a name="span-idspecialpoolefficiencyspanspan-idspecialpoolefficiencyspanspecial-pool-efficiency"></a><span id="special_pool_efficiency"></span><span id="SPECIAL_POOL_EFFICIENCY"></span>特別なプールの効率性

すべての特別なプールの要求が満たされます。 特別なプールから各割り当ては、非ページングの物理メモリの 1 つのページと仮想アドレス空間の 2 つのページを使用します。 プールがなくなった場合は、特別なプールが再び使用可能になるまでに、標準的な方法でメモリが割り当てられます。 特別なプールの要求は、標準的なプールからいっぱいになると、要求元の関数エラーは返されませんが、プールの要求が成功したため。 そのため、特別なプール機能がアクティブの場合、複数のドライバーを同時に検証することをしないお勧めします。

多くのメモリ要求を行う 1 つのドライバーには、このプールが使い果たされもします。 このような場合は、ドライバーのメモリ割り当てにプール タグを割り当てるし、一度に 1 つのプール タグに専用の特別なプールすることをお勧め場合があります。

特別なプールのサイズはシステム上の物理メモリ量を増加します。理想的には少なくとも 1 ギガバイト (GB) があります。 X86 マシン、仮想 (場合によってに物理また) 領域が消費されるため、使用しないでください、 [ **3 GB** ](https://msdn.microsoft.com/library/windows/hardware/ff556232)ブート オプション。 2 または 3 の倍数でページファイルの最小値/最大数量を増やすことをお勧めします。

テスト中のすべてのドライバーの割り当てのことを確認するには、長期間にわたってドライバーを生じてすることをお勧めします。

### <a name="span-idmonitoringthespecialpoolspanspan-idmonitoringthespecialpoolspanmonitoring-the-special-pool"></a><span id="monitoring_the_special_pool"></span><span id="MONITORING_THE_SPECIAL_POOL"></span>特別なプールの監視

プールの割り当てに関連する統計情報を監視することができます。 これらは、ドライバー検証ツール マネージャーによって、Verifier.exe コマンドラインまたはログ ファイルに表示できます。 参照してください[グローバル カウンターの監視](monitoring-global-counters.md)詳細についてはします。

場合、**特別なプールにプールの割り当てが成功した**カウンターと等しい、**プールの割り当てが成功した**カウンター、特別なプールがすべてのメモリ割り当てをカバーするための十分なが。 前者のカウンターが、後者より低い場合は、特別なプールが使い果たされたを少なくとも 1 回です。

これらのカウンターは、サイズが 1 つのページ割り当てを追跡しないか、特別なプールから該当します。

特別なプール機能が有効になっているすべてのプール割り当ての 95% 未満を特別なプールから割り当てられている場合は、警告がドライバー検証マネージャーで表示されます。 Windows 2000 でこの警告が表示されます、 **ドライバ ステータスの**画面。 Windows XP 以降では、この警告に表示されます、**グローバル カウンター**画面。 この場合、ドライバーの短い一覧を確認します。 プールのタグを使用して個々 のプールを確認します、以上の物理メモリをシステムに追加またはする必要があります。

カーネル デバッガー拡張機能 **! verifier**特別なプールの使用状況を監視できます。 ドライバー検証マネージャーのする同様の情報が表示されます。 デバッガーの拡張機能については、[Windows デバッグ](https://msdn.microsoft.com/library/windows/hardware/ff551063)を参照してください。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>このオプションをアクティブ化します。

ドライバー検証マネージャーまたは Verifier.exe コマンドラインを使用して、1 つまたは複数のドライバー用に特別なプール機能をアクティブ化することができます。 詳細については、[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)を参照してください。

**注**  プール タグまたは割り当てのサイズの特別なプール機能をアクティブ化するかを設定する、**開始を確認します**(アンダーランの検出) と**終了の確認**(オーバーランの検出) 配置、使用して、[グローバル フラグ ユーティリティ](using-the-global-flags-utility.md); 特別なプールのすべての割り当てにこれらの配置の設定が適用されます。

 

-   **コマンドラインで**

    、コマンドラインでは、特別なプール オプションで表される**ビット 0 (0x1)** します。 特別なプールをアクティブ化するには、0x1 のフラグの値を使用するか、フラグの値を 0x1 を追加します。 次に、例を示します。

    ```
    verifier /flags 0x1 /driver MyDriver.sys
    ```

    この機能は、[次へ] の起動後にアクティブになります。

    Windows 2000 と Windows の以降のバージョンもアクティブ化し、特別なプールを追加することで、コンピューターを再起動しなくても非アクティブ化することができます、 **/volatile**パラメーターをコマンド。 次に、例を示します。

    ```
    verifier /volatile /flags 0x1 /adddriver MyDriver.sys
    ```

    この設定は、すぐに有効は、シャット ダウンするか、コンピューターを再起動すると失われます。 詳細については、[揮発性の設定を使用する](using-volatile-settings.md)を参照してください。

    特別なプール機能は、標準の設定にも含まれます。 次に、例を示します。

    ```
    verifier /standard /driver MyDriver.sys
    ```

-   **ドライバー検証マネージャーを使用します。**

    1.  選択 **(コード開発者) 用のカスタム設定を作成する**順にクリックします**次**します。
    2.  選択**完全な一覧から個々 の設定を選択します。** します。
    3.  選択 (チェック)**特別なプール**します。

    特別なプール機能は、標準の設定にも含まれます。 この機能では、ドライバー検証マネージャーでを使用する をクリックして**標準設定の作成**です。

 

 





