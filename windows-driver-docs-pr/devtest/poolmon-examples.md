---
title: PoolMon の例
description: PoolMon の例
ms.assetid: aff0abdd-7d68-49b8-b9a1-71ab866c8487
keywords:
- PoolMon WDK、例
- メモリプールモニタ WDK、例
- WDK PoolMon の例
ms.date: 07/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: f033c410126cc798d1106aafdbbd570f49f85e56
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769374"
---
# <a name="poolmon-examples"></a>PoolMon の例


## <span id="ddk_poolmon_examples_tools"></span><span id="DDK_POOLMON_EXAMPLES_TOOLS"></span>


このトピックには、次の PoolMon の使用例が含まれています。

例 1: PoolMon の出力を表示および並べ替える

例 2: ドライバー名を表示する

例 3: メモリリークを検出する

例 4: プールのメモリリークを調べる

例 5: ターミナルサーバーセッションを監視する

### <a name="span-idddk_example_1_display_and_sort_poolmon_output_toolsspanspan-idddk_example_1_display_and_sort_poolmon_output_toolsspanexample-1-display-and-sort-poolmon-output"></a><span id="ddk_example_1_display_and_sort_poolmon_output_tools"></span><span id="DDK_EXAMPLE_1_DISPLAY_AND_SORT_POOLMON_OUTPUT_TOOLS"></span>例 1: PoolMon の出力を表示および並べ替える

この例では、PoolMon の表示を構成するさまざまな方法について説明します。 既定では、PoolMon はタグ値によって、すべてのカーネルメモリ割り当てを英数字順に表示します。 コマンドラインまたは PoolMon の実行中に、表示の並べ替え順序を変更できます。

次のコマンドを実行すると、PoolMon が開始されます。

```
poolmon
```

次のコマンドは、PoolMon を起動し、空き操作の数で表示を並べ替えます。

```
poolmon /f
```

Poolmon の実行中は、実行時コマンドを使用して表示を変更できます。 たとえば、使用されているバイト数で表示を並べ替えるには、 **b**キーを押します。 割り当てごとにバイトで並べ替えるには、 **m**キーを押します。

次のコマンドは、PoolMon を起動し、非ページプールからの割り当てのみを表示します。

```
poolmon /p
```

PoolMon が実行されている間に、 **p**キーを押して、ページプール、非ページプール、またはその両方からの割り当てを切り替えることができます。

PoolMon を開始し、特定のタグを持つ割り当てのデータを表示するには、 **/i**パラメーターを使用します。 次のコマンドは、 **Afdb**タグ (データバッファー用に afd.sys によって使用されるタグ) の割り当てを表示します。

```
poolmon /iAfdB
```

特定のタグを持つ割り当てを除外するには、 **/x**パラメーターを使用します。 次のコマンドは、 **Afdb**タグを持たないすべての割り当てを表示します。

```
poolmon /xAfdB
```

アスタリスク ( \* ) や疑問符 (?) を使用して、同じ文字でタグのセットを指定できます。 次のコマンドは、 **afd**で始まるプールタグを持つ割り当てを表示します。これは、afd.sys によって使用されるタグです。

```
poolmon /iAfd*
```

PoolMon スタートアップコマンドには、複数の **/i**および **/x**パラメーターを含めることができます。 次のコマンドでは、 **Ccbc**タグを使用した割り当てを除いて、" **Aud** " で始まるタグと、 **Cc**で始まる4文字のタグを持つ割り当てを表示します。

```
poolmon /iAud* /iCc?? /xCcBc
```

また、更新間の値の変更によって、PoolMon の表示を並べ替えることもできます。 **/(** パラメーターを指定すると、PoolMon は変更モードで並べ替えられます。

次のコマンドは、 **Afd**で始まるタグの割り当てを表示し、割り当ての変更によって並べ替えます。 **/A**パラメーターを使用して割り当ての数で並べ替え、 **/)** パラメーターを使用して割り当ての数の変化によって並べ替えます。

```
poolmon /iAfd* /( /a
```

**/(** パラメーターとかっこのキーはトグルスイッチです。 PoolMon が変更モードである場合、すべての並べ替えコマンドが、値の変更によって並べ替えられるようにコマンドとして解釈されます。 もう一度かっこのキーを押すと、値で並べ替えられます。

### <a name="span-idddk_example_2_display_driver_names_toolsspanspan-idddk_example_2_display_driver_names_toolsspanexample-2-display-driver-names"></a><span id="ddk_example_2_display_driver_names_tools"></span><span id="DDK_EXAMPLE_2_DISPLAY_DRIVER_NAMES_TOOLS"></span>例 2: ドライバー名を表示する

PoolMon **/g**パラメーターを使用すると、各プールタグを割り当てる Windows コンポーネントと一般的に使用されるドライバーの名前を表示できます。 特定のタグを持つ割り当てに問題が見つかった場合、この機能は問題のあるコンポーネントまたはドライバーを特定するのに役立ちます。

コンポーネントとドライバーは、画面の右端の列である [マップされたドライバー] 列に一覧表示され \_ ます。 マップされたドライバーの列のデータは、 \_ PoolMon と共にインストールされるファイルである pooltag .txt から取得されます。

次のコマンドは、 **Ntf**で始まるタグで割り当てられたメモリを表示します。 (疑問符文字 (**?**) をワイルドカードとして使用します)。**/G**パラメーターを指定すると、マップされたドライバーの列が追加され \_ ます。

```
poolmon /iNtF? /g
```

結果の表示には、 **Ntf**で始まるタグを使用した割り当てが一覧表示されます。 [マップされたドライバーの表示] の右端の列は、メモリが ntfs \_ ファイルシステムのドライバーである ntfs.sys によって割り当てられたことを示しています。 この場合、pooltag .txt には NTFS 割り当てのソースファイルが含まれているため、表示はさらに具体的です。

```
 Memory:  260620K Avail:   65152K  PageFlts:    85   InRam Krnl: 2116K P:19560K
 Commit: 237688K Limit: 640916K Peak: 260632K            Pool N: 8500K P:33024K
 System pool information
 Tag  Type     Allocs            Frees            Diff   Bytes      Per Alloc  Mapped_Driver

 NtFA Nonp       9112 (   0)      9112 (   0)     0       0 (     0)      0 [ntfs.sys  -  AttrSup.c]
 NtFB Paged      3996 (   0)      3986 (   0)    10  252088 (     0)  25208 [ntfs.sys  -  BitmpSup.c]
 NtFC Paged   1579279 (   0)   1579269 (   0)    10     640 (     0)     64 [ntfs.sys  -  Create.c]
 NtFD Nonp         13 (   0)        13 (   0)     0       0 (     0)      0 [ntfs.sys  -  DevioSup.c]
 NtFF Paged      1128 (   0)      1128 (   0)     0       0 (     0)      0 [ntfs.sys  -  FileInfo.c]
 NtFI Nonp        152 (   0)       152 (   0)     0       0 (     0)      0 [ntfs.sys  -  IndexSup.c]
 NtFL Nonp      68398 (   0)     68390 (   0)     8   27280 (     0)   3410 [ntfs.sys  -  LogSup.c]
 NtFS Paged      2915 (   0)      2614 (   0)   301   80192 (     0)    266 [ntfs.sys  -  SecurSup.c]
 NtFa Paged       838 (   0)       829 (   0)     9     288 (     0)     32 [ntfs.sys  -  AllocSup.c]
 NtFd Paged    137696 (   0)    137688 (   0)     8     720 (     0)     90 [ntfs.sys  -  DirCtrl.c]
 NtFf Nonp          2 (   0)         1 (   0)     1      40 (     0)     40 [ntfs.sys  -  FsCtrl.c]
 NtFs Nonp      48825 (   0)     47226 (   0)  1599   64536 (     0)     40 [ntfs.sys  -  StrucSup.c]
 NtFv Paged       551 (   0)       551 (   0)     0       0 (     0)      0 [ntfs.sys  -  ViewSup.c]
```

Pooltag .txt は広く使用されていますが、Windows で使用されているすべてのタグの完全な一覧ではありません。 表示に表示されているタグが pooltag .txt に含まれていない場合、タグの [マップされたドライバー] 列に "不明なドライバー" と表示され \_ ます。 この場合、 **/c**パラメーターを使用してローカルシステム上のドライバーを検索し、タグが割り当てられているかどうかを判断できます。

このメソッドの例を次に示します。

次のコマンドでは、 **/i**パラメーターを使用して、メモリ内で終了するタグの割り当てを一覧表示します。 **/G**パラメーターは、ドライバー名を pooltag .txt ファイルから表示に追加します。

```
poolmon /i?MEM /g
```

結果の表示には、メモリ内で終了タグがある割り当てが一覧表示されます。 ただし、メモリタグは pooltag に含まれていないため、 \_ ドライバー名の代わりに [マップされたドライバー] 列に "不明なドライバー" が表示されます。

```
 Tag  Type        Allocs          Frees      Diff   Bytes      Per Alloc    Mapped_Driver

 1MEM Nonp       1 (   0)         0 (   0)     1    3344 (     0)   3344   Unknown Driver
 2MEM Nonp       1 (   0)         0 (   0)     1    3944 (     0)   3944   Unknown Driver
 3MEM Nonp       3 (   0)         0 (   0)     3     248 (     0)     82   Unknown Driver
```

この場合、 **/c**パラメーターを使用して、ローカルドライバーの一覧と割り当てられたタグをコンパイルし、[マップされたドライバー] 列にローカルドライバーの名前を表示でき \_ ます。

次のコマンドを実行すると、PoolMon が開始されます。 **/I**パラメーターを使用して、メモリで終わるタグの割り当てを一覧表示し、 **/c**パラメーターを使用してタグを割り当てるローカルドライバーを表示します。

```
poolmon /i?MEM /c
```

ローカルタグファイルを指定せず、PoolMon で localtag .txt ファイルが見つからない場合は、次の画面メッセージに示すように、そのファイルが作成されます。 (PoolMon は、64ビットバージョンの Windows でローカルタグファイルを生成することはできません)。

```
d:\tools\poolmon>poolmon /?MEM /c
PoolMon: No localtag.txt in current directory
PoolMon: Creating localtag.txt in current directory......
```

新しく作成された localtag .txt ファイルのコンテンツを使用して、[マップされたドライバー] 列にローカルドライバー名が表示され \_ ます。

```
 Memory:  260620K Avail:   57840K  PageFlts:   162   InRam Krnl: 2116K P:19448K
 Commit: 244580K Limit: 640916K Peak: 265416K            Pool N: 8496K P:32904K
 System pool information
 Tag  Type     Allocs            Frees            Diff   Bytes      Per Alloc  Mapped_Driver

 1MEM Nonp          1 (   0)         0 (   0)        1    3344 (     0)   3344 [el90xbc5]
 2MEM Nonp          1 (   0)         0 (   0)        1    3944 (     0)   3944 [el90xbc5]
 3MEM Nonp          3 (   0)         0 (   0)        3     248 (     0)     82 [el90xbc5]
```

包括的なドライバー名の表示では、コマンドで **/c**パラメーターと **/g**パラメーターを組み合わせることができます。 (パラメーターの順序によって出力が変更されることはありません)。次のコマンドは、 **Ip**で始まるタグの割り当てを一覧表示します。 **/C**パラメーターを使用します。これは、[マップされたドライバー] 列の localtag .txt ファイルの内容を使用し、/g パラメーターを使用します。このパラメーターは、[マップされ \_ **/g**たドライバー] \_ 列にある pooltag .txt ファイルの内容を使用します。

```
poolmon /iIp* /c /g
```

結果の表示では、[マップされたドライバー] 列に、 \_ localtag .txt ファイルと pooltag .txt ファイルの両方のデータが含まれています。

```
 Memory:  130616K Avail:   23692K  PageFlts:   146   InRam Krnl: 2108K P: 9532K
 Commit: 187940K Limit: 318628K Peak: 192000K            Pool N: 8372K P:13384K
 System pool information
 Tag  Type     Allocs            Frees            Diff   Bytes      Per Alloc  Mapped_Driver

 IpEQ Nonp          1 (   0)         0 (   0)        1    1808 (     0)   1808 [ipsec][ipsec.sys    -  event queue]
 IpFI Nonp         26 (   0)         0 (   0)       26    7408 (     0)    284 [ipsec][ipsec.sys    -  Filter blocks]
 IpHP Nonp          1 (   0)         1 (   0)        0       0 (     0)      0 [ipsec.sys    - IP Security]
 IpIO Nonp          1 (   0)         1 (   0)        0       0 (     0)      0 [ipsec]
 IpLA Nonp          1 (   0)         0 (   0)        1     248 (     0)    248 [ipsec][ipsec.sys    -  lookaside lists]
 IpSH Nonp          1 (   0)         1 (   0)        0       0 (     0)      0 [ipsec.sys    - IP Security]
 IpSI Nonp       1027 (   0)         0 (   0)     1027   53272 (     0)     51 [ipsec][ipsec.sys    - initial allcoations]
 IpTI Nonp          3 (   0)         0 (   0)        3    5400 (     0)   1800 [ipsec][ipsec.sys    -  timers]
```

### <a name="span-idddk_example_3_detect_memory_leakage_toolsspanspan-idddk_example_3_detect_memory_leakage_toolsspanexample-3-detect-memory-leakage"></a><span id="ddk_example_3_detect_memory_leakage_tools"></span><span id="DDK_EXAMPLE_3_DETECT_MEMORY_LEAKAGE_TOOLS"></span>例 3: メモリリークを検出する

この例では、PoolMon を使用してメモリリークを検出する手順を示します。

1.  パラメーター **/p/p** (ページングプールからの割り当てのみを表示) と **/b** (バイト数で並べ替え) を使用して PoolMon を開始します。
    ```
    poolmon /p /p /b
    ```

2.  PoolMon を数時間実行します。 PoolMon を開始するとデータが変更されるため、データの信頼性を確保するには安定した状態になる必要があります。

3.  PoolMon によって生成された情報をスクリーンショットとして保存するか、コマンドウィンドウからコピーしてメモ帳に貼り付けます。

4.  PoolMon に戻り、 **p**キーを2回押して、非ページプールからの割り当てのみを表示します。

5.  少なくとも2時間は30分ごとに手順3と4を繰り返し、ページングされたプールと非ページプールを切り替えるたびに切り替えます。

6.  データ収集が完了したら、各タグについて、差分 (割り当て操作から解放操作を差し引いた値から解放されたバイト数を引いた値) を確認し、継続的に増加しているものがないかどうかを確認します。

7.  次に、PoolMon を停止し、数時間待ってから、PoolMon を再起動します。

8.  増加している割り当てを確認し、バイトが解放されたかどうかを判断します。 原因としては、まだ解放されていないか、またはサイズが増加し続けている割り当てが考えられます。


### <a name="span-idddk_example_4_examine_a_pool_memory_leak_toolsspanspan-idddk_example_4_examine_a_pool_memory_leak_toolsspanexample-4-examine-a-pool-memory-leak"></a><span id="ddk_example_4_examine_a_pool_memory_leak_tools"></span><span id="DDK_EXAMPLE_4_EXAMINE_A_POOL_MEMORY_LEAK_TOOLS"></span>例 4: プールのメモリリークを調べる

次の例では、PoolMon を使用して、疑わしいプリンタードライバーからプールメモリリークを調査します。 この例では、Windows が Dsrd タグを使用してメモリ割り当てについて収集したデータを表示します。

プリンタードライバーは、グラフィカルデバイスインターフェイス (GDI) オブジェクトと関連付けられたメモリを割り当てるときに Drsd タグを割り当てます。 プリンタドライバにオブジェクトリークがある場合、Drsd タグを使用して割り当てられたメモリにもリークが発生します。

**メモ**   この例の手順を実行する前に、使用しているプリンターが完了するまで中断されないようにしてください。 それ以外の場合は、結果が無効になることがあります。

 

コマンドラインで、次のように入力します。

```
poolmon /iDrsd
```

このコマンドは、Drsd タグを使用した割り当ての情報を表示するように PoolMon に指示します。 (プールタグでは大文字と小文字が区別されます。そのため、必ず示されているとおりにコマンドを入力してください)。

[Diff] 列と [Bytes] 列に値を記録します。 次のサンプルの表示では、Diff の値は21、バイト数は17472です。

```
Memory:  130480K Avail:   91856K  PageFlts:  1220   InRam Krnl: 2484K P: 7988K
Commit:  30104K Limit: 248432K Peak:  34028K            Pool N: 2224K P: 8004K
Tag  Type        Allocs           Frees           Diff  Bytes           Per Alloc

Drsd Paged       560 ( 177)       539 ( 171)       21   17472 (  4992)    832 
```

プリンターにジョブを送信し、Windows が正常に戻るまでしばらく待ってから、Diff と Bytes 列の値を記録します。

```
Memory:  130480K Avail:   91808K  PageFlts:  1240   InRam Krnl: 2488K P: 7996K
Commit:  30152K Limit: 248432K Peak:  34052K            Pool N: 2224K P: 8012K
Tag  Type        Allocs           Frees           Diff  Bytes          Per Alloc

Drsd Paged       737 (   0)       710 (   0)       27   22464 (     0)    832  
```

プリンタードライバーのメモリ管理が正常に機能している場合、差分の値は、印刷後の元の値21に戻ります。 ただし、上記の出力に示すように、Diff の値は27になり、バイト数は22464になります。 最初と2番目の出力の違いは、6つの Drsd ブロック (合計4992バイト) が印刷中にリークしていることを意味します。

### <a name="span-idfor_more_informationspanspan-idfor_more_informationspanspan-idfor_more_informationspanfor-more-information"></a><span id="For_More_Information"></span><span id="for_more_information"></span><span id="FOR_MORE_INFORMATION"></span>詳細情報

ドライバーがリークしていると思われる場合は、 [Microsoft サポート](https://support.microsoft.com/)の web サイトにアクセスして、サポート技術情報の記事を検索してください。

### <a name="span-idddk_example_5_monitor_a_terminal_server_session_toolsspanspan-idddk_example_5_monitor_a_terminal_server_session_toolsspanexample-5-monitor-a-terminal-server-session"></a><span id="ddk_example_5_monitor_a_terminal_server_session_tools"></span><span id="DDK_EXAMPLE_5_MONITOR_A_TERMINAL_SERVER_SESSION_TOOLS"></span>例 5: ターミナルサーバーセッションを監視する

この例では、ターミナルサービスのセッションプールから割り当てを表示するいくつかの方法を示します。 **/S**コマンドラインパラメーター、 **s**、 *tssessionid*、および**i**を実行するパラメーターの使用方法を示します。

次のコマンドは、すべてのターミナルサービスセッションプールからの割り当てを表示します。 この例では、ターミナルサーバーとして構成されているローカルコンピューターがセッションをホストしており、クライアントコンピューターがリモートデスクトップ機能を使用してホストに接続しています。

```
poolmon /s
```

応答として、PoolMon はすべてのセッションプールからの割り当てを表示します。 ヘッダーの "すべてのセッションプール情報" タイトルに注意してください。

```
Memory:  523572K Avail:  233036K  PageFlts:   344   InRam Krnl: 1828K P:18380K
Commit: 193632K Limit:1279764K Peak: 987356K            Pool N:14332K P:18644K
All sessions pool information
 Tag  Type     Allocs            Frees            Diff   Bytes       Per Alloc

 Bmfd Paged       361 (   0)       336 (   0)       25   57832 (     0)   2313
 DDfb Paged        34 (   0)        22 (   0)       12     720 (     0)     60
 Dddp Paged         8 (   0)         6 (   0)        2     272 (     0)    136
 Dh 1 Paged        24 (   0)        24 (   0)        0       0 (     0)      0
 Dh 2 Paged       344 (   0)       344 (   0)        0       0 (     0)      0
 Dvgr Paged         2 (   0)         2 (   0)        0       0 (     0)      0
 GDev Paged       108 (   0)       102 (   0)        6   20272 (     0)   3378
 GFil Paged        29 (   0)        27 (   0)        2     160 (     0)     80
 GPal Paged        11 (   0)         8 (   0)        3     816 (     0)    272
 GTmp Paged     88876 (   1)     88876 (   1)        0       0 (     0)      0
 GUma Paged         2 (   0)         2 (   0)        0       0 (     0)      0
 Galp Paged      3250 (   0)      3250 (   0)        0       0 (     0)      0
 Gbaf Paged      9829 (   0)      9801 (   0)       28   19712 (     0)    704
 Gcac Paged      3761 (   0)      3706 (   0)       55  288968 (     0)   5253
 Gcsl Paged         1 (   0)         0 (   0)        1     488 (     0)    488
 Gdbr Paged      6277 (   0)      6271 (   0)        6    1872 (     0)    312
 ...
```

特定のセッションプールからの割り当てを表示するには、次のコマンドに示すように、 **/s**パラメーターの直後にセッション ID を入力します。 このコマンドは、ターミナルサービスセッション0のセッションプールの割り当てを表示します。

```
poolmon /s0
```

応答として、PoolMon は、ターミナルサービスセッション0のセッションプールからの割り当てを表示します。 ヘッダーの "Session 0 pool information" タイトルに注意してください。

```
Memory:  523572K Avail:  233024K  PageFlts:   525   InRam Krnl: 1828K P:18384K
 Commit: 193760K Limit:1279764K Peak: 987356K            Pool N:14340K P:18644K
 Session 0 pool information
 Tag  Type     Allocs            Frees            Diff   Bytes       Per Alloc

 Bmfd Paged       361 (   0)       336 (   0)       25   57832 (     0)   2313
 DDfb Paged        34 (   0)        22 (   0)       12     720 (     0)     60
 Dddp Paged         8 (   0)         6 (   0)        2     272 (     0)    136
 Dh 1 Paged        24 (   0)        24 (   0)        0       0 (     0)      0
 Dh 2 Paged       344 (   0)       344 (   0)        0       0 (     0)      0
 Dvgr Paged         2 (   0)         2 (   0)        0       0 (     0)      0
 GDev Paged       108 (   0)       102 (   0)        6   20272 (     0)   3378
 GFil Paged        29 (   0)        27 (   0)        2     160 (     0)     80
 GPal Paged        11 (   0)         8 (   0)        3     816 (     0)    272
 GTmp Paged     89079 (  99)     89079 (  99)        0       0 (     0)      0
 GUma Paged         2 (   0)         2 (   0)        0       0 (     0)      0
 Galp Paged      3250 (   0)      3250 (   0)        0       0 (     0)      0
 Gbaf Paged      9830 (   0)      9802 (   0)       28   19712 (     0)    704
 Gcac Paged      3762 (   0)      3707 (   0)       55  283632 (     0)   5156
 Gcsl Paged         1 (   0)         0 (   0)        1     488 (     0)    488
 Gdbr Paged      6280 (   0)      6274 (   0)        6    1872 (     0)    312
 ...
```

セッションプールからメモリを割り当てているドライバーとコンポーネントを特定するには、次のコマンドに示すように、 **/g**パラメーターを追加します。 **/G**パラメーターを \_ 指定すると、各タグを割り当てる Windows コンポーネントとドライバーを一覧表示する、マップされたドライバーの列が追加されます。

```
poolmon /s0 /g

Memory:  523572K Avail:  235876K  PageFlts:    43   InRam Krnl: 1900K P:18860K
Commit: 185040K Limit:1279764K Peak: 987356K            Pool N:14684K P:19124K
Session 0 pool information
Tag  Type     Allocs            Frees            Diff   Bytes      Per Alloc  Mapped_Driver

Bmfd Paged       421 (   0)       396 (   0)       25   57832 (     0)   2313 [Font related stuff]
DDfb Paged        34 (   0)        22 (   0)       12     720 (     0)     60 Unknown Driver
Dddp Paged        11 (   0)         6 (   0)        5     392 (     0)     78 Unknown Driver
Dh 1 Paged        37 (   0)        35 (   0)        2     224 (     0)    112 Unknown Driver
Dh 2 Paged       367 (   0)       364 (   0)        3     912 (     0)    304 Unknown Driver
Dvgr Paged         2 (   0)         2 (   0)        0       0 (     0)      0 [vga for risc video driver]
GDev Paged       119 (   0)       113 (   0)        6   20272 (     0)   3378 [Gdi pdev]
GFil Paged        29 (   0)        27 (   0)        2     160 (     0)     80 [Gdi engine descriptor list]
GPal Paged        11 (   0)         8 (   0)        3     816 (     0)    272 [Gdi Objects]
GTmp Paged     98626 (   1)     98626 (   1)        0       0 (     0)      0 [Gdi Objects]
GUma Paged         2 (   0)         2 (   0)        0       0 (     0)      0 [Gdi Objects]
Galp Paged      3250 (   0)      3250 (   0)        0       0 (     0)      0 [Gdi Objects]
Gbaf Paged     10331 (   0)     10305 (   0)       26   18304 (     0)    704 [Gdi Objects]
Gcac Paged      4722 (   0)      4666 (   0)       56  305400 (     0)   5453 [Gdi glyph cache]
Gcsl Paged         1 (   0)         0 (   0)        1     488 (     0)    488 [Gdi string resource script names]
Gdbr Paged      6972 (   0)      6965 (   0)        7    2184 (     0)    312 [Gdi driver brush realization]
```

また、PoolMon の実行中にターミナルサービスセッションプールの表示を構成することもできます。 次の表に、一連の実行中のコマンドを入力順に示し、結果の PoolMon を表示します。

シリーズは、PoolMon を開始するコマンドで始まります。 他のすべてのパラメーターは、PoolMon の実行中に入力されます。

```
poolmon
```

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Key</th>
<th align="left">結果</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>s</strong></p></td>
<td align="left"><p>すべてのセッションプールを表示します。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>2$s</strong></p></td>
<td align="left"><p>システムプールを表示します。</p></td>
<td align="left"><p><strong>S</strong>パラメーターを指定すると、システムプールとターミナルサービスセッションプールの間の表示が切り替わります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>0</strong></p></td>
<td align="left"><p>セッション0のプールを表示します。</p></td>
<td align="left"><p>システムプールを表示しているときに、セッション ID を入力できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>7</strong></p></td>
<td align="left"><p>セッション7プールを表示します。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>ある</strong></p></td>
<td align="left"><p>セッション7のプール割り当てを、割り当ての数で並べ替えて表示します。</p></td>
<td align="left"><p>すべての標準の実行パラメーターは、セッションプールの表示に対して有効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>0</strong></p></td>
<td align="left"><p>割り当ての数によって並べ替えられた、セッション0の割り当てを表示します。</p></td>
<td align="left"><p>セッションおよび並べ替えのオプションは、変更されるまで保持されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>2$s</strong></p></td>
<td align="left"><p>システムプールを表示します。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>2$s</strong></p></td>
<td align="left"><p>割り当ての数によって並べ替えられた、セッション0の割り当てを表示します。</p></td>
<td align="left"><p>セッションオプションは保持されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>10ENTER</strong></p></td>
<td align="left"><p>セッション1の割り当てを表示し、セッション0の割り当てを表示します。</p></td>
<td align="left"><p><strong>I</strong>を使用しない場合は、セッション id 0 ~ 9 のみを入力できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>i</strong></p></td>
<td align="left"><p>ターミナルサーバーのセッション ID の入力を求めます。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>"<strong>10</strong>"</p></td>
<td align="left"><p>セッション10の割り当てを表示します。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>i</strong></p></td>
<td align="left"><p>ターミナルサーバーのセッション ID の入力を求めます。</p></td>
<td align="left"><p>すべてのセッションプールを表示するには、 <strong>i</strong>キーを押して enter キーを押します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>を入力し</strong></p></td>
<td align="left"><p>すべてのセッションプールを表示します。</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

ターミナルサーバーとして構成されているシステムのみがセッションプールからメモリを割り当てます。 PoolMon を使用して、ターミナルサーバーではないコンピューターにセッションプールを表示した場合、または Windows に存在しないセッション ID を入力した場合、PoolMon に割り当ては表示されません。 代わりに、一般的なメモリデータを含む見出しだけが表示されます。

次のコマンドは、すべてのターミナルサービスセッションプールからの割り当てを表示します。

```
poolmon /s
```

次の図は、ターミナルサーバーとして構成できなかった Windows XP を実行しているコンピューターに **/s**コマンドが送信された場合に発生する PoolMon の表示を示しています。

```
 Memory:  260620K Avail:   44956K  PageFlts:   308   InRam Krnl: 2744K P:20444K
 Commit: 185452K Limit: 640872K Peak: 192472K            Pool N: 8112K P:20648K
 All sessions pool information
 Tag  Type     Allocs            Frees            Diff   Bytes       Per Alloc
```

 

 





