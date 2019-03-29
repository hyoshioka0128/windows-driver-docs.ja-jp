---
title: カーネル デバッガーを使用したカーネルモード メモリ リークの検出
description: カーネル デバッガーを使用したカーネルモード メモリ リークの検出
ms.assetid: eeadd505-b887-498d-9369-877156526355
keywords:
- メモリ リーク、カーネル モード、カーネル デバッガー
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5162aa2d79a996f32676e8575a929a2f5aa7d975
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572862"
---
# <a name="using-the-kernel-debugger-to-find-a-kernel-mode-memory-leak"></a>カーネル デバッガーを使用したカーネルモード メモリ リークの検出


カーネル デバッガーは、カーネル モードのメモリ リークの正確な場所を決定します。

### <a name="span-idenablepooltaggingwindows2000andwindowsxpspanspan-idenablepooltaggingwindows2000andwindowsxpspanenable-pool-tagging-windows-2000-and-windows-xp"></a><span id="enable_pool_tagging__windows_2000_and_windows_xp_"></span><span id="ENABLE_POOL_TAGGING__WINDOWS_2000_AND_WINDOWS_XP_"></span>プール (Windows 2000 および Windows XP) のタグ付けを有効にします。

使用する必要がありますまず[GFlags](gflags.md)プール タグ付けを有効にします。 Windows ツールをデバッグには GFlags が含まれます。 開始 GFlags、選択、**システム レジストリ** タブで、チェック、**プールのタグ付けを有効にする**ボックスをクリックして**適用**します。 この設定を有効にする Windows を再起動する必要があります。

Windows Server 2003 および Windows の以降のバージョンでは、プールのタグ付けは常に有効です。

### <a name="span-iddeterminingthepooltagoftheleakspanspan-iddeterminingthepooltagoftheleakspandetermining-the-pool-tag-of-the-leak"></a><span id="determining_the_pool_tag_of_the_leak"></span><span id="DETERMINING_THE_POOL_TAG_OF_THE_LEAK"></span>リークのプール タグを決定します。

どのプール タグはをリークに関連付けを確認するのには、通常 PoolMon ツールを使用して、この手順を最も簡単なは。 詳細については、次を参照してください。[カーネル モード メモリ リークの検出に使用する PoolMon](using-poolmon-to-find-a-kernel-mode-memory-leak.md)します。

また、カーネル デバッガーを使用すると、大規模なプールの割り当てに関連付けられているタグを探します。 これを行うには、次の手順を実行します。

1.  すべてのモジュールを再読み込みを使用して、 [ **.reload (モジュールの再読み込み)** ](-reload--reload-module-.md)コマンド。

2.  使用して、 [ **! poolused** ](-poolused.md)拡張機能。 フラグ ページングされたメモリを使用して、出力を並べ替えるには、「4」にはが含まれます。
    ```dbgcmd
    kd> !poolused 4 
    Sorting by Paged Pool Consumed

    Pool Used:
                NonPaged            Paged     
    Tag    Allocs     Used    Allocs     Used 
    Abc         0        0     36405 33930272 
    Tron        0        0       552  7863232 
    IoN7        0        0     10939   998432 
    Gla5        1      128      2222   924352 
    Ggb         0        0        22   828384 
    ```

3.  メモリの最大使用量に関連付けられているプール タグを確認します。 この例では、"Abc"のタグを使用して、ドライバーは、最もメモリ--ほぼ 34 MB を使用しています。 そのため、メモリ リークは、このドライバーである可能性は。

### <a name="span-idfindingtheleakspanspan-idfindingtheleakspanfinding-the-leak"></a><span id="finding_the_leak"></span><span id="FINDING_THE_LEAK"></span>メモリ リークを見つける

プール タグを確認した後、リーク自体を検索するには、この手順に従ってくださいリークに関連付けられました。

1.  使用して、 [ **ed (値を入力)** ](e--ea--eb--ed--ed--ef--ep--eq--eu--ew--eza--ezu--enter-values-.md)グローバル システム変数の値を変更するコマンド**PoolHitTag**します。 このグローバル変数には、デバッガーがその値に一致するプール タグを使用する場合に中断が発生します。

2.  設定**PoolHitTag**メモリ リークのソースにすると思われるタグと同じです。 高速のシンボル解決のためには、"nt"モジュール名を指定してください。 (つまり、逆方向)、タグの値をリトル エンディアン形式で入力する必要があります。 プール タグは、次の 4 つの文字では常に、ために、このタグは、実際には A から b c-空間、だけで A、b、c ではなく、します。 したがって、次のコマンドを使用します。
    ```dbgcmd
    kd> ed nt!poolhittag ' cbA' 
    ```

3.  現在の値を確認する**PoolHitTag**を使用して、 [ **db (表示メモリ)** ](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)コマンド。
    ```dbgcmd
    kd> db nt!poolhittag L4 
    820f2ba4  41 62 63 20           Abc  
    ```

4.  そのプールが割り当てられているか、タグを使用して解放するたびに、デバッガーは中断**Abc**します。 これらの割り当てまたは無料の操作のいずれかで、デバッガーが中断毎回使用して、 [ **kb (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)デバッガー スタック トレースを表示するコマンド。

この手順を使用して、するかを調べるコードをメモリに常駐プール タグ内容を変更は**Abc**します。

ブレークポイントをクリアするには、設定**PoolHitTag**をゼロにします。

```dbgcmd
kd> ed nt!poolhittag 0 
```

複数の異なる場所でこのタグにメモリが割り当てられると、これらは、アプリケーションまたは記述したドライバーである場合は、これらの割り当てのそれぞれに一意のタグを使用するソース コードを変更できます。

プログラムを再コンパイルすることはできません、リークの原因であるコードにいくつかの場所のどれを判別する場合は、各場所でコードを逆アセンブルし、デバッガーを使用して、各インスタンスで、distinc を使用するようにメモリに常駐しているこのコードを編集t (および未使用) タグをプールします。 数分以上を実行するシステムを許可します。 少し時間が経過すると、デバッガーで中断し、使用、 [ **! poolfind** ](-poolfind.md)新しいタグのそれぞれに関連付けられているすべてのプール割り当てを検索する拡張機能。

 

 





