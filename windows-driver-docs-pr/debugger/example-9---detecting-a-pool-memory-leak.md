---
title: 例 9 プールのメモリ リークを検出します。
description: 例 9 プールのメモリ リークを検出します。
ms.assetid: 3f634593-a024-46d1-9f3d-9d39b28bab03
keywords:
- PoolMon、PoolMon および GFlags
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: f4a193fbd6a2d17964f3d7478c92eb789b116e45
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552341"
---
# <a name="example-9-detecting-a-pool-memory-leak"></a>例 9:プールのメモリ リークを検出します。


## <span id="ddk_example_9___detecting_a_pool_memory_leak_dtools"></span><span id="DDK_EXAMPLE_9___DETECTING_A_POOL_MEMORY_LEAK_DTOOLS"></span>


次の例では、システム全体を設定する GFlags を使用して[プール タグ付けを有効にする](enable-pool-tagging.md)レジストリのフラグ。 次に、メモリ プールのサイズを表示するのに PoolMon (poolmon.exe)、Windows Driver Kit のツールを使用します。

PoolMon では、ページおよび非ページ メモリ プール内のバイトを監視し、プール タグで並べ替えています。 PoolMon を定期的に実行すると、時間の経過と共に継続的に展開するプールを特定できます。 このパターンは、多くの場合、メモリ リークを表します。

**注**   Windows Server 2003 および以降のバージョンの Windows では完全に有効になってプール タグ付けします。 これらのシステムで、**プール タグ付けを有効にする**チェック ボックスをオン、**グローバル フラグ** ダイアログ ボックスは淡色表示になり、プール タグ付けの失敗を有効または無効にするコマンド。
プールのタグ付けが有効でない場合、PoolMon は失敗し、次のメッセージが表示されます。「クエリを pooltags Failed c0000002。」

 

**プールのメモリ リークを検出するには**

1.  プールの Windows Server 2003 より前のバージョンの Windows でのすべてのプロセスのタグ付けを有効にするには、システム全体を設定[プール タグ付けを有効にする](enable-pool-tagging.md)レジストリのフラグ。 次のコマンド ライン フラグの省略形メソッドを使用しますが、16 進値で、フラグを識別したり、使用して、**グローバル フラグ** ダイアログ ボックス。
    ```console
    gflags /r +ptg 
    ```

2.  レジストリの変更を有効にするコンピューターを再起動します。

3.  次のコマンドを使用して、PoolMon を定期的に実行します。 このコマンドで、 **/b**パラメーターが、プール サイズの降順で並べ替えられます。

    ```console
    poolmon /b 
    ```

    応答では、降順でサイズの数など、メモリ プールから PoolMon 表示割り当ては、操作および無料の操作と (バイト列) のプールに残っているメモリの量を割り当てます。

    ```console
    Memory: 16224K Avail: 4564K PageFlts: 31 InRam Krnl: 684K P: 680K
     Commit: 24140K Limit: 24952K Peak: 24932K  Pool N: 744K P: 2180K

     Tag  Type    Allocs          Frees         Diff   Bytes      Per Alloc
    -----------------------------------------------------------------------

     CM   Paged    1283 (   0)    1002 (   0)    281 1377312 (     0) 4901
    Strg  Paged   10385 (  10)    6658 (   4)   3727  317952 (   512)   85
     Fat  Paged    6662 (   8)    4971 (   6)   1691  174560 (   128)  103
    MmSt  Paged     614 (   0)     441 (   0)    173   83456 (     0)  482
    ```

    場合の値、**バイト**割り当て列が明らかな理由の継続的に展開、そのプールでメモリ リークしている可能性がありますがあります。

4.  クリア、**プール タグ付けを有効にする**フラグ。

    次のコマンド ライン フラグの省略形メソッドを使用しますが、16 進値で、フラグを識別したり、使用して、**グローバル フラグ** ダイアログ ボックス。

    ```console
    gflags /r -ptg 
    ```

5.  レジストリの変更を有効にする Windows を再起動します。

**注**  追加シンボルを使用して (**&gt;&gt;**) PoolMon 出力ログ ファイルにリダイレクトします。 後で、プール サイズの傾向のログ ファイルを確認することができます。 次に、例を示します。

 

```console
poolmon.exe /b >> poolmon.log 
```

 

 





