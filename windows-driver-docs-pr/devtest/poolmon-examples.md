---
title: PoolMon の例
description: PoolMon の例
ms.assetid: aff0abdd-7d68-49b8-b9a1-71ab866c8487
keywords:
- PoolMon WDK、例
- メモリ プール モニタ WDK の例
- WDK PoolMon の例
ms.date: 07/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: bdb6caa7e3d4773a60f19f324e7dd87e1f04452d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327242"
---
# <a name="poolmon-examples"></a>PoolMon の例


## <span id="ddk_poolmon_examples_tools"></span><span id="DDK_POOLMON_EXAMPLES_TOOLS"></span>


このトピックでは、PoolMon 使用の次の例を示します。

例 1:表示と並べ替え PoolMon 出力

例 2:ドライバー名を表示します。

例 3: メモリ リークを検出します。

例 4:プールのメモリ リークを調べる

例 5:ターミナル サーバー セッションを監視します。

### <a name="span-idddkexample1displayandsortpoolmonoutputtoolsspanspan-idddkexample1displayandsortpoolmonoutputtoolsspanexample-1-display-and-sort-poolmon-output"></a><span id="ddk_example_1_display_and_sort_poolmon_output_tools"></span><span id="DDK_EXAMPLE_1_DISPLAY_AND_SORT_POOLMON_OUTPUT_TOOLS"></span>例 1:表示と並べ替え PoolMon 出力

この例では、PoolMon 画面を構成するさまざまな方法について説明します。 既定では、PoolMon はカーネル メモリの割り当てがすべてアルファベット順でタグ値で表示します。 コマンドラインで、または PoolMon の実行中にディスプレイの並べ替え順序を変更できます。

次のコマンドは、PoolMon を開始します。

```
poolmon
```

次のコマンドは、PoolMon が起動し、無料の操作の数で表示を並べ替えます。

```
poolmon /f
```

Poolmon の実行中には、表示を変更するのに、実行時のコマンドを使用できます。 たとえば、表示の使用バイト数で並べ替えに押します**b**します。 割り当てあたりのバイト数で並べ替えるには、キーを押して**m**します。

次のコマンドは、PoolMon を起動し、非ページ プールから割り当てのみが表示されます。

```
poolmon /p
```

PoolMon の実行中にキーを押して**p**ページ プール、非ページ プール、またはその両方からの割り当てを切り替える。

PoolMon を起動し、特定のタグの割り当てのデータを表示、使用、 **/i**パラメーター。 次のコマンドの表示を割り当て、 **AfdB**タグ (タグのデータ バッファーの afd.sys で使用)。

```
poolmon /iAfdB
```

特定のタグを割り当て、除外するを使用して、 **/x**パラメーター。 次のコマンドがないすべての割り当てを表示する、 **AfdB**タグ。

```
poolmon /xAfdB
```

アスタリスクを使用することができます (\*) や疑問符 (?) を同じ文字のタグのセットを指定します。 次のコマンドは、以降では、プール タグの割り当てを表示します**Afd**、afd.sys; で使用されるタグ。

```
poolmon /iAfd*
```

PoolMon スタートアップ コマンドは、複数を含めることができます **/i**と **/x**パラメーター。 次のコマンドで始まるタグの割り当てを表示する**Aud**以降では 4 文字のタグと**Cc**と割り当てを除く、 **CcBc**タグ。

```
poolmon /iAud* /iCc?? /xCcBc
```

更新プログラムの間の値を変更して、PoolMon 表示を並べ替えることもできます。 **/(** パラメーターは、並べ替えの変更によってモードに PoolMon を配置します。

次のコマンドで始まるタグの割り当てを表示する**Afd**割り当ての変更によって並べ替えます。 使用して、 **/a**割り当ての数で並べ替えるにパラメーターおよび **/)** 割り当ての数の変更を並べ替えるにはパラメーター。

```
poolmon /iAfd* /( /a
```

**/(** パラメーターと、かっこキーは、トグル スイッチ。 PoolMon がモードの並べ替えの変更によって、値の変更を並べ替えるにはコマンドとして並べ替えのすべてのコマンドを解釈します。 もう一度かっこキーを押すと場合、値によって並べ替えます。

### <a name="span-idddkexample2displaydrivernamestoolsspanspan-idddkexample2displaydrivernamestoolsspanexample-2-display-driver-names"></a><span id="ddk_example_2_display_driver_names_tools"></span><span id="DDK_EXAMPLE_2_DISPLAY_DRIVER_NAMES_TOOLS"></span>例 2:ドライバー名を表示します。

PoolMon を使用する **/g**と一般的な Windows コンポーネントの名前を表示するパラメーターは、各プール タグを割り当てることがドライバーを使用します。 この機能で特定のタグの割り当てに問題がある場合、問題が発生したコンポーネントまたはドライバーを識別できます。

コンポーネントとドライバーが、マップ先で表示されている\_ドライバー列、ディスプレイの右端の列。 マップ済みデータ\_ドライバー列 pooltag.txt、PoolMon にインストールされているファイルに由来します。

次のコマンドで始まるタグで割り当てられたメモリを表示する**NtF**します。 (疑問符 () 文字を使用して (**?**) をワイルドカードとして)。**/G**パラメーターの追加、マップ済み\_ドライバー列。

```
poolmon /iNtF? /g
```

結果の表示の開始タグと割り当てを一覧表示**NtF**します。 ディスプレイ画面の右端の列にマップされている\_ドライバーは、NTFS ファイル システムのドライバー、ntfs.sys、によって、メモリが割り当てられたことを示しています。 この場合、表示がさらに詳細な pooltag.txt に NTFS 割り当てのソース ファイルが含まれるためです。

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

Pooltag.txt が大きいが、Windows で使用されるすべてのタグの完全な一覧ではありません。 Pooltag.txt では、画面に表示するタグが含まれていない、PoolMon が、マップ先で「不明なドライバー」が表示されます\_タグのドライバーの列。 これが発生したときに使用できます、 **/c**パラメーターをローカル システムでドライバーを検索し、タグを割り当てることがあるかどうかを判断します。

次の例では、このメソッドを示します。

次のコマンドを使用して、 **/i**パラメーターをメモリ最適化の終了タグの割り当てを一覧します。 **/G**パラメーター pooltag.txt ファイルから、表示するため、ドライバー名を追加します。

```
poolmon /i?MEM /g
```

結果の表示では、メモリ最適化の終了タグの割り当てを一覧表示します。 ただし、メモリ最適化のタグが pooltag.txt で含まれていないため、「不明なドライバー」は、マップ先に表示されます\_ドライバー名の代わりにドライバー列。

```
 Tag  Type        Allocs          Frees      Diff   Bytes      Per Alloc    Mapped_Driver

 1MEM Nonp       1 (   0)         0 (   0)     1    3344 (     0)   3344   Unknown Driver
 2MEM Nonp       1 (   0)         0 (   0)     1    3944 (     0)   3944   Unknown Driver
 3MEM Nonp       3 (   0)         0 (   0)     3     248 (     0)     82   Unknown Driver
```

この場合、使用することができます、 **/c**パラメーターをローカルのドライバーと割り当てることも、タグの一覧をコンパイルして、マップ先のローカルのドライバーの名前を表示する\_ドライバー列。

次のコマンドは、PoolMon を開始します。 使用して、 **/i**でメモリ最適化では、終了タグの割り当てを一覧にパラメーターおよび **/c**ローカル ドライバー、タグの割り当てを表示するパラメーター。

```
poolmon /i?MEM /c
```

タグのローカル ファイルと PoolMon localtag.txt ファイルを見つけることができませんを指定しない場合が作成されます、次の画面のメッセージで示すように。 (PoolMon は、64 ビット版 Windows 上のローカル タグ ファイルを生成できません)

```
d:\tools\poolmon>poolmon /?MEM /c
PoolMon: No localtag.txt in current directory
PoolMon: Creating localtag.txt in current directory......
```

結果の表示を新しく作成された localtag.txt ファイルからコンテンツを使用して、マップ済みで、ローカル ドライバー名を示しています\_ドライバー列。

```
 Memory:  260620K Avail:   57840K  PageFlts:   162   InRam Krnl: 2116K P:19448K
 Commit: 244580K Limit: 640916K Peak: 265416K            Pool N: 8496K P:32904K
 System pool information
 Tag  Type     Allocs            Frees            Diff   Bytes      Per Alloc  Mapped_Driver

 1MEM Nonp          1 (   0)         0 (   0)        1    3344 (     0)   3344 [el90xbc5]
 2MEM Nonp          1 (   0)         0 (   0)        1    3944 (     0)   3944 [el90xbc5]
 3MEM Nonp          3 (   0)         0 (   0)        3     248 (     0)     82 [el90xbc5]
```

包括的なドライバーの名前の表示を組み合わせることができます、 **/c**と **/g**コマンドのパラメーター。 (パラメーターの順序は、出力を変更はありません)。次のコマンドで始まるタグの割り当てを一覧表示**Ip**します。 使用して、 **/c** localtag.txt、マップ済みファイルの内容を使用して、パラメーター\_ドライバー列、および **/g** pooltag.txt、マップ済みファイルの内容を使用して、パラメーター\_ドライバー列。

```
poolmon /iIp* /c /g
```

結果の表示、マップ先で\_ドライバー列には localtag.txt と pooltag.txt の両方のファイルからのデータが含まれています。

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

### <a name="span-idddkexample3detectmemoryleakagetoolsspanspan-idddkexample3detectmemoryleakagetoolsspanexample-3-detect-memory-leakage"></a><span id="ddk_example_3_detect_memory_leakage_tools"></span><span id="DDK_EXAMPLE_3_DETECT_MEMORY_LEAKAGE_TOOLS"></span>例 3:メモリ リークを検出します。

この例では、PoolMon を使用して、メモリ リークを検出するための手順を提案します。

1.  パラメーターを使用して PoolMon をスタート **/p/p** (ページ プールから割り当てのみを表示) と **/b** (バイト数で並べ替え) します。
    ```
    poolmon /p /p /b
    ```

2.  PoolMon、数時間実行することができます。 開始 PoolMon にデータが変更されたために、前に、データは信頼性の高い、安定した状態を回復する必要があります。

3.  スクリーン ショット、または、コマンド ウィンドウからコピーしてメモ帳に貼り付けて PoolMon、生成した情報を保存します。

4.  PoolMon に戻って、キーを押して、 **p**非ページ プールから割り当てのみを表示するには、2 回のキー。

5.  手順 3 と 4 30 分に約 2 時間以上のたびにページおよび非ページ プールの表示を切り替える.

6.  データ収集が完了したら、確認、相違点 (無料の操作-割り当て操作) とバイト数 (解放されるバイト数-割り当てられたバイト数) の各値がタグ、および増加し続けることに注意してください。

7.  次に、PoolMon を停止し、数時間待って、して PoolMon を再起動します。

8.  割り当てを増やすと、バイトが解放されるかどうかを判断するを確認します。 考えられる原因は、割り当てがまだ解放されていないか、サイズが増加し続けているです。


### <a name="span-idddkexample4examineapoolmemoryleaktoolsspanspan-idddkexample4examineapoolmemoryleaktoolsspanexample-4-examine-a-pool-memory-leak"></a><span id="ddk_example_4_examine_a_pool_memory_leak_tools"></span><span id="DDK_EXAMPLE_4_EXAMINE_A_POOL_MEMORY_LEAK_TOOLS"></span>例 4:プールのメモリ リークを調べる

次の例では、疑いのあるプリンター ドライバーからプールのメモリ リークを調査する PoolMon を使用してを示します。 この例では、PoolMon は、Windows が Dsrd タグを持つメモリの割り当てについて収集するデータを表示します。

プリンター ドライバーは、グラフィック デバイス インターフェイス (GDI) オブジェクトと関連付けられているメモリを割り当て、ときに、Drsd タグを割り当てます。 プリンター ドライバーに、オブジェクトのリークがある場合は、Drsd タグに割り当てられるメモリもリークが発生します。

**注**  この例では、手順を実行する前に完了するまで使用しているプリンターは中断されないことを確認します。 それ以外の場合、結果は有効でない可能性があります。

 

コマンド ラインで、次のように入力します。

```
poolmon /iDrsd
```

このコマンドでは、PoolMon Drsd タグの割り当ての情報を表示するように指示します。 (プール タグは大文字小文字を区別、あるため、正確に示すように、コマンドを入力してください)。

Diff およびバイト列の値を記録します。 次のサンプル表示での相違の値は 21 とは 17472 のバイト数。

```
Memory:  130480K Avail:   91856K  PageFlts:  1220   InRam Krnl: 2484K P: 7988K
Commit:  30104K Limit: 248432K Peak:  34028K            Pool N: 2224K P: 8004K
Tag  Type        Allocs           Frees           Diff  Bytes           Per Alloc

Drsd Paged       560 ( 177)       539 ( 171)       21   17472 (  4992)    832 
```

ジョブをプリンターに送信を返すには、通常、Windows を簡単に待つし、Diff およびバイト列の値を記録しています。

```
Memory:  130480K Avail:   91808K  PageFlts:  1240   InRam Krnl: 2488K P: 7996K
Commit:  30152K Limit: 248432K Peak:  34052K            Pool N: 2224K P: 8012K
Tag  Type        Allocs           Frees           Diff  Bytes          Per Alloc

Drsd Paged       737 (   0)       710 (   0)       27   22464 (     0)    832  
```

プリンター ドライバーのメモリ管理が正常に動作して、相違の値は、印刷後に元の値は 21 に返す必要があります。 ただし、上記の出力としてに示した、27 と 22464 に rose のバイト数には差分の値。 初期およびそれ以降の出力間の差 4992 (バイト単位) の合計で 6 つの Drsd ブロックが印刷中にリークすることを意味します。

### <a name="span-idformoreinformationspanspan-idformoreinformationspanspan-idformoreinformationspanfor-more-information"></a><span id="For_More_Information"></span><span id="for_more_information"></span><span id="FOR_MORE_INFORMATION"></span>詳細については

リークしているドライバーを特定したと思われる場合は、 [Microsoft サポート](https://go.microsoft.com/fwlink/p/?linkid=8713)web サイトおよび関連する記事の検索、ナレッジ ベース。

### <a name="span-idddkexample5monitoraterminalserversessiontoolsspanspan-idddkexample5monitoraterminalserversessiontoolsspanexample-5-monitor-a-terminal-server-session"></a><span id="ddk_example_5_monitor_a_terminal_server_session_tools"></span><span id="DDK_EXAMPLE_5_MONITOR_A_TERMINAL_SERVER_SESSION_TOOLS"></span>例 5:ターミナル サーバー セッションを監視します。

この例では、ターミナル サービス セッションのプールから割り当てを表示するいくつかの方法を示します。 使用例を示します、 **/s**コマンド ライン パラメーター、および**s**、 *TSSessionID*、および**は**パラメーターを実行しています。

次のコマンドは、すべてのターミナル サービス セッションのプールから割り当てを表示します。 この例で、セッションをホストしているローカルのコンピューターは、ターミナル サーバーとして構成して、ホストに接続するリモート デスクトップ機能を使用しているクライアント コンピューター。

```
poolmon /s
```

応答、PoolMon はセッションのすべてのプールから割り当てを表示します。 ヘッダーに「すべてのセッション プール情報」のタイトルに注意してください。

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

特定のセッションのプールから割り当てを表示するには、セッション ID を入力した直後に、 **/s**パラメーターは、次のコマンドで示すようにします。 このコマンドは、ターミナル サービス セッション 0 のセッションのプール割り当てを表示します。

```
poolmon /s0
```

応答として、PoolMon はターミナル サービス セッション 0 のセッションのプールから割り当てを表示します。 ヘッダーに「Session 0 プール情報」のタイトルに注意してください。

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

セッションのプールからメモリの割り当ては、ドライバーやコンポーネントを確認するためには、追加、 **/g**パラメーターは、次のコマンドで示すようにします。 **/G**パラメーターの追加、マップ済み\_ドライバー列に、Windows のコンポーネントと各タグを割り当てることがドライバーを表示します。

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

PoolMon の実行中には、ターミナル サービス セッションのプールの表示を構成することもできます。 次の表では、一連の順序で入力された、および結果として得られる PoolMon 表示で、コマンドの実行を示します。

系列は、PoolMon を起動するコマンドから始まります。 PoolMon の実行中に、その他のすべてのパラメーターが入力されます。

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
<td align="left"><p>セッションのすべてのプールを表示します。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>s</strong></p></td>
<td align="left"><p>システム プールが表示されます。</p></td>
<td align="left"><p><strong>S</strong>パラメーターは、システム プールと、ターミナル サービス セッションのプールの表示を切り替えます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>0</strong></p></td>
<td align="left"><p>セッション 0 プールが表示されます。</p></td>
<td align="left"><p>システム プールを表示するときに、セッション ID を入力できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>7</strong></p></td>
<td align="left"><p>セッションの 7 プールが表示されます。</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>a</strong></p></td>
<td align="left"><p>割り当ての数で並べ替えられますセッション、7 のプール割り当てを表示します。</p></td>
<td align="left"><p>すべての標準実行中のパラメーターは、セッション プールの表示に対して有効です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>0</strong></p></td>
<td align="left"><p>割り当ての数によって並べ替えられて、セッション 0 の割り当てを表示します。</p></td>
<td align="left"><p>セッションおよび並べ替えのオプションは、変更されるまで保持されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>s</strong></p></td>
<td align="left"><p>システム プールが表示されます。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>s</strong></p></td>
<td align="left"><p>割り当ての数によって並べ替えられて、セッション 0 の割り当てを表示します。</p></td>
<td align="left"><p>セッション オプションが保持されます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>10ENTER</strong></p></td>
<td align="left"><p>セッション 1 の割り当てを表示し、セッション 0 の割り当てを表示します。</p></td>
<td align="left"><p>せず<strong>は</strong>、セッション Id 0 ~ 9 のみを入力することができます。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>i</strong></p></td>
<td align="left"><p>ターミナル サーバー セッションの ID のプロンプト</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>"<strong>10</strong>"</p></td>
<td align="left"><p>セッションの 10 の割り当てを表示します。</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><strong>i</strong></p></td>
<td align="left"><p>ターミナル サーバー セッションの ID のプロンプト</p></td>
<td align="left"><p>セッションのすべてのプールを表示するには、キーを押します<strong>は</strong>し、ENTER キーを押します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>入力します</strong></p></td>
<td align="left"><p>セッションのすべてのプールを表示します。</p></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

ターミナル サーバーとして構成されているシステムのみでは、セッションのプールからメモリを割り当てます。 ターミナル サーバーではないコンピューターでセッションのプールを表示する PoolMon を使用する場合、または Windows に存在しないセッション ID を入力する場合は、PoolMon では、この割り当ては表示されません。 代わりに、全般的なメモリのデータに見出しだけが表示されます。

次のコマンドでは、ターミナル サービス セッションのすべてのプールからの割り当てが表示されます。

```
poolmon /s
```

次の図に、PoolMon ディスプレイを表す場合、 **/s**ターミナル サーバーとして構成できませんでした Windows XP を実行するコンピューターに送信されたコマンド。

```
 Memory:  260620K Avail:   44956K  PageFlts:   308   InRam Krnl: 2744K P:20444K
 Commit: 185452K Limit: 640872K Peak: 192472K            Pool N: 8112K P:20648K
 All sessions pool information
 Tag  Type     Allocs            Frees            Diff   Bytes       Per Alloc
```

 

 





