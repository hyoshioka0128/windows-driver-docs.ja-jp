---
title: デバッガー コマンド プログラムの例
description: デバッガー コマンド プログラムの例
ms.assetid: da756906-6243-4cb9-b4e5-5b0b4540533d
keywords:
- デバッガー コマンド プログラム例
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c96157f368350ec2beb55a86f6bbab787e3a67a9
ms.sourcegitcommit: fee68bc5f92292281ecf1ee88155de45dfd841f5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716855"
---
# <a name="debugger-command-program-examples"></a>デバッガー コマンド プログラムの例


## <span id="ddk_debugger_command_program_examples_dbg"></span><span id="DDK_DEBUGGER_COMMAND_PROGRAM_EXAMPLES_DBG"></span>


次のセクションでは、デバッガー コマンド プログラムについて説明します。

### <a name="span-idusingtheforeachtokenspanspan-idusingtheforeachtokenspanusing-the-foreach-token"></a><span id="using_the__foreach_token"></span><span id="USING_THE__FOREACH_TOKEN"></span>.Foreach トークンを使用します。

次の例では、 [ **.foreach** ](-foreach.md) 5a4d の WORD 値を検索するトークン。 見つかった 5a4d 値ごとに、デバッガーでは 8 つの DWORD 値を表示します 5a4d dword 値が検出された場所のアドレスで始まります。

```dbgcmd
0:000> .foreach (place { s-[1]w 77000000 L?4000000 5a4d }) { dc place L8 } 
```

次の例では、 [ **.foreach** ](-foreach.md) 5a4d の WORD 値を検索するトークン。 見つかった 5a4d 値ごとに、デバッガーでは 8 つの DWORD 値を表示します 5a4d dword 値が検出された場所、アドレスの前に 4 バイトを開始します。

```dbgcmd
0:000> .foreach (place { s-[1]w 77000000 L?4000000 5a4d }) { dc place -0x4 L8 } 
```

次の例では、同じ値が表示されます。

```dbgcmd
0:000> .foreach (place { s-[1]w 77000000 L?4000000 5a4d }) { dc ( place -0x4 ) L8 } 
```

**注**  で変数名を操作するかどうか、 *OutCommands*部分コマンドの変数名の後にスペースを追加する必要があります。 たとえば、上記の例でスペースがある、変数間*配置*と減算演算子。

 

**- \[1\]** オプションと共に、 [ **s (メモリの検索)** ](s--search-memory-.md)コマンドにより、その出力は、アドレスのみを含めるこれで、これらのアドレスにある値ではなくは検索します。

次のコマンドでは、0x7F000000 を通じて 0x77000000 からメモリの範囲内にあるすべてのモジュールのモジュールの詳細な情報が表示されます。

```dbgcmd
0:000> .foreach (place { lm1m }) { .if ((${place} >= 0x77000000) & (${place} <= 0x7f000000)) { lmva place } } 
```

**1 m**オプションと共に、 [ **lm (読み込まれたモジュールの一覧)** ](lm--list-loaded-modules-.md)コマンドは、その出力のない完全な説明、モジュールのアドレスのみを含む、モジュール。

上記の例では、 [ **$ {} (別名インタープリター)** ](-------alias-interpreter-.md)トークンを他のテキストの横にある場合でも、エイリアスは置き換えられますことを確認します。 コマンドがこのトークンを含んでいない場合、かっこを横にある**配置**エイリアスの置換を防止します。 なお、 **${}** トークンで使用されている変数は **.foreach**とエイリアスが true でします。

### <a name="span-idwalkingtheprocesslistspanspan-idwalkingtheprocesslistspanwalking-the-process-list"></a><span id="walking_the_process_list"></span><span id="WALKING_THE_PROCESS_LIST"></span>プロセスの一覧のウォーク

次の例では、カーネル モード プロセスの一覧について説明し、エントリごとに実行可能ファイル名を一覧に表示されます。

この例のテキスト ファイルとして格納されているし、でを実行する必要があります、 [  **$$ &gt; &lt; (スクリプト ファイルを実行)** ](-----------------------a---run-script-file-.md)コマンド。 このコマンドは、ファイル全体を読み込みをセミコロンで区切って、すべての改行が置き換えられ、結果として得られるブロックを実行します。 このコマンドに 1 行上にプログラム全体ではなく、複数の行と、インデントを使用して、読み取り可能なプログラムを記述することができます。

この例では、次の機能を示します。

-   **$T0**、 **$t1**、および **$t2**擬似レジスタは、このプログラムで変数として使用されます。 プログラムもという名前のエイリアスを使用して**副**と **$ImageName**します。

-   このプログラムは、MASM 式エバリュエーターを使用します。 ただし、 **@@c+ ()** トークンに 1 つの時刻が表示されます。 このトークンは、C++ の式エバリュエーターを使用して、かっこで囲まれた式を解析するプログラムをさせます。 この使用法を使用すると、C++ 構造体のトークンを直接使用するプログラム。

-   **でしょうか。** フラグを併用、 [ **r (レジスタ)** ](r--registers-.md)コマンド。 このフラグは、擬似レジスタに型指定された値を割り当てます **$t2**します。

```dbgcmd
$$  Get process list LIST_ENTRY in $t0.
r $t0 = nt!PsActiveProcessHead

$$  Iterate over all processes in list.
.for (r $t1 = poi(@$t0);
      (@$t1 != 0) & (@$t1 != @$t0);
      r $t1 = poi(@$t1))
{
    r? $t2 = #CONTAINING_RECORD(@$t1, nt!_EPROCESS, ActiveProcessLinks);
    as /x Procc @$t2

 $$  Get image name into $ImageName.
 as /ma $ImageName @@c++(&@$t2->ImageFileName[0])

 .block
    {
        .echo ${$ImageName} at ${Procc}
    }

    ad $ImageName
    ad Procc
}
```

### <a name="span-idwalkingtheldrdatatableentrylistspanspan-idwalkingtheldrdatatableentrylistspanwalking-the-ldrdatatableentry-list"></a><span id="walking_the_ldr_data_table_entry_list"></span><span id="WALKING_THE_LDR_DATA_TABLE_ENTRY_LIST"></span>LDR のウォーク\_データ\_テーブル\_エントリの一覧

次の例の手順をユーザー モード LDR\_データ\_テーブル\_エントリ一覧ベース アドレスとリストの各エントリの完全なパスが表示されます。

上記の例のようにこのプログラムする必要があります、ファイルに保存して実行されると、 [  **$$ &gt; &lt; (スクリプト ファイルを実行)** ](-----------------------a---run-script-file-.md)コマンド。

この例では、次の機能を示します。

- このプログラムは、MASM 式エバリュエーターを使用します。 ただし、2 つの場所で、 **@@c+ ()** トークンが表示されます。 このトークンは、C++ の式エバリュエーターを使用して、かっこで囲まれた式を解析するプログラムをさせます。 この使用法を使用すると、C++ 構造体のトークンを直接使用するプログラム。

- **でしょうか。** フラグを併用、 [ **r (レジスタ)** ](r--registers-.md)コマンド。 このフラグは、擬似レジスタに型指定された値を割り当てます **$t0**と **$t1**します。 ループの本体で **$t1**タイプ**ntdll!\_LDR\_データ\_テーブル\_エントリ\\\*** プログラムは、参照に直接的なメンバーにことができるようにします。

- という名前のユーザー別名 **$Base**と **$Mod**このプログラムで使用されます。 ドル記号は、これらのエイリアスがデバッガーの現在のセッションで以前使用されている可能性を低減します。 ドル記号は必要ありません。 [ **${/V:}** ](-------alias-interpreter-.md)トークン エイリアスの解釈文字どおり、スクリプトの実行前に定義されている場合に置き換えられるを避けます。 ブロックの前に、別名定義が使用されていることを防ぐために、任意のブロックと共にこのトークンを使用することもできます。

- [ **.Block** ](-block.md)余分なエイリアスの置換手順を追加するトークンを使用します。 エイリアスの置換は、スクリプト全体が読み込まれるときに 1 回、1 回の各ブロックが入力された場合に発生します。 なし、 **.block**トークンと、その中かっこ、 **.echo**コマンドがの値を受信していない、 **$Mod**と **$Base**の別名は前の行に割り当てられます。

```dbgcmd
$$ Get module list LIST_ENTRY in $t0.
r? $t0 = &@$peb->Ldr->InLoadOrderModuleList
 
$$ Iterate over all modules in list.
.for (r? $t1 = *(ntdll!_LDR_DATA_TABLE_ENTRY**)@$t0;
 (@$t1 != 0) & (@$t1 != @$t0);
      r? $t1 = (ntdll!_LDR_DATA_TABLE_ENTRY*)@$t1->InLoadOrderLinks.Flink)
{
    $$ Get base address in $Base.
 as /x ${/v:$Base} @@c++(@$t1->DllBase)
 
 $$ Get full name into $Mod.
 as /msu ${/v:$Mod} @@c++(&@$t1->FullDllName)
 
 .block
    {
        .echo ${$Mod} at ${$Base}
    }
 
    ad ${/v:$Base}
    ad ${/v:$Mod}
}
```

 

 





