---
title: カーネル デバッガーを使用したカーネルモード メモリ リークの検出
description: カーネル デバッガーを使用したカーネルモード メモリ リークの検出
ms.assetid: eeadd505-b887-498d-9369-877156526355
keywords:
- メモリリーク、カーネルモード、カーネルデバッガー
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0398237fbd88fb8afd1f68d98b743c95bb32035f
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209628"
---
# <a name="using-the-kernel-debugger-to-find-a-kernel-mode-memory-leak"></a>カーネル デバッガーを使用したカーネルモード メモリ リークの検出


カーネルデバッガーによって、カーネルモードのメモリリークの正確な場所が決定されます。

### <a name="span-idenable_pool_tagging__windows_2000_and_windows_xp_spanspan-idenable_pool_tagging__windows_2000_and_windows_xp_spanenable-pool-tagging"></a><span id="enable_pool_tagging__windows_2000_and_windows_xp_"></span><span id="ENABLE_POOL_TAGGING__WINDOWS_2000_AND_WINDOWS_XP_"></span>プールのタグ付けを有効にする 

最初に、 [GFlags](gflags.md)を使用してプールのタグ付けを有効にする必要があります。 GFlags は、Windows 用デバッグツールに含まれています。 GFlags を起動し、[**システムレジストリ**] タブを選択し、[**プールタグ付けを有効にする**] チェックボックスをオンにして、[**適用**] をクリックします。 この設定を有効にするには、Windows を再起動する必要があります。

Windows Server 2003 以降のバージョンの Windows では、プールのタグ付けは常に有効になっています。

### <a name="span-iddetermining_the_pool_tag_of_the_leakspanspan-iddetermining_the_pool_tag_of_the_leakspandetermining-the-pool-tag-of-the-leak"></a><span id="determining_the_pool_tag_of_the_leak"></span><span id="DETERMINING_THE_POOL_TAG_OF_THE_LEAK"></span>リークのプールタグの特定

リークに関連付けられているプールタグを特定するには、通常、この手順で PoolMon ツールを使用するのが最も簡単です。 詳細については、「PoolMon を使用した[カーネルモードのメモリリークの検出](using-poolmon-to-find-a-kernel-mode-memory-leak.md)」を参照してください。

または、カーネルデバッガーを使用して、大きなプール割り当てに関連付けられているタグを検索することもできます。 これを行うには、次の手順に従います。

1.  [**リロード (モジュールの再読み込み)**](-reload--reload-module-.md)コマンドを使用して、すべてのモジュールを再読み込みします。

2.  [**! Poolused**](-poolused.md)拡張機能を使用します。 ページメモリ使用によって出力を並べ替えるには、フラグ "4" を含めます。
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

3.  メモリの最大使用量に関連付けられているプールタグを特定します。 この例では、タグ "Abc" を使用しているドライバーが最も多くのメモリを使用しています (約 34 MB)。 そのため、メモリリークは、このドライバーに含まれる可能性が最も高くなります。

### <a name="span-idfinding_the_leakspanspan-idfinding_the_leakspanfinding-the-leak"></a><span id="finding_the_leak"></span><span id="FINDING_THE_LEAK"></span>リークの検出

リークに関連付けられているプールタグを特定したら、次の手順に従って、リーク自体を見つけます。

1.  [**Ed (値の入力)**](e--ea--eb--ed--ed--ef--ep--eq--eu--ew--eza--ezu--enter-values-.md)コマンドを使用して、グローバルシステム変数の**poolヒットタグ**の値を変更します。 このグローバル変数を使用すると、その値に一致するプールタグが使用されるたびにデバッガーが中断します。

2.  **Poolヒットタグ**は、メモリリークの原因と思われるタグに等しく設定します。 シンボルの精度を向上させるには、モジュール名 "nt" を指定する必要があります。 タグ値は、リトルエンディアン形式 (つまり、後方) で入力する必要があります。 プールタグは常に4文字であるため、このタグは単に A-b-c ではなく、実際には a-b-c スペースです。 そのため、次のコマンドを使用します。
    ```dbgcmd
    kd> ed nt!poolhittag ' cbA' 
    ```

3.  **Poolヒットタグ**の現在の値を確認するには、 [**Db (Display Memory)**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)コマンドを使用します。
    ```dbgcmd
    kd> db nt!poolhittag L4 
    820f2ba4  41 62 63 20           Abc  
    ```

4.  タグ**Abc**でプールが割り当てられるか解放されるたびに、デバッガーは中断します。 これらの割り当てまたは解放操作のいずれかでデバッガーが中断するたびに、 [**kb (スタックバックトレースの表示)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)デバッガーコマンドを使用してスタックトレースを表示します。

この手順を使用すると、メモリに常駐しているコードで、タグ**Abc**でプールの割り当てが過剰になっていることを確認できます。

ブレークポイントをクリアするには、 **Poolヒットタグ**をゼロに設定します。

```dbgcmd
kd> ed nt!poolhittag 0 
```

このタグを持つメモリが割り当てられている場所が複数あり、これらがアプリケーションまたはドライバーに割り当てられている場合は、これらの割り当てごとに一意のタグを使用するようにソースコードを変更できます。

プログラムを再コンパイルできないが、コード内のいずれかの場所でリークの原因となっている箇所を特定する場合は、各場所でコードをアセンブルして、デバッガーを使用して、メモリ内に常駐するこのコードを編集し、各インスタンスが distinc を使用するようにします。t (および以前に未使用の) プールタグ。 次に、数分以内にシステムの実行を許可します。 しばらく時間が経過したら、デバッガーでもう一度中断し、 [**! poolfind**](-poolfind.md)拡張機能を使用して、新しい各タグに関連付けられているすべてのプール割り当てを検索します。

 

 





