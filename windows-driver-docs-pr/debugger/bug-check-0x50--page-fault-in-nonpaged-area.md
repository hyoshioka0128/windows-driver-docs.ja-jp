---
title: バグチェック 0x50 PAGE_FAULT_IN_NONPAGED_AREA
description: PAGE_FAULT_IN_NONPAGED_AREA のバグチェックの値は0x00000050 です。 これは、無効なシステムメモリが参照されていることを示します。
ms.assetid: 63b4ab82-f7a9-4e14-bf7c-707a22d7e251
keywords:
- バグチェック 0x50 PAGE_FAULT_IN_NONPAGED_AREA
- PAGE_FAULT_IN_NONPAGED_AREA
ms.date: 04/18/2019
topic_type:
- apiref
api_name:
- PAGE_FAULT_IN_NONPAGED_AREA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b046ff169db86578684c12ae37f4c8b106e18dba
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025327"
---
# <a name="bug-check-0x50-page_fault_in_nonpaged_area"></a>バグ チェック 0x50:ページング\_\_\_される領域内のページフォールト\_


\_ページング\_\_されていない領域のバグチェックのページフォールトの値は0x00000050です。\_ これは、無効なシステムメモリが参照されていることを示します。 通常、メモリアドレスが間違っているか、メモリアドレスが解放されたメモリを指しています。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="page_fault_in_nonpaged_area-parameters"></a>非\_\_\_ページ領域パラメーターのページフォールト\_


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">引き</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>参照されたメモリアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left">
<p><i>Windows 1507 (TH1) バージョンの後-x64</i> </p>
<p><strong>0</strong>読み取り操作</p>
<p><strong>2:</strong>書き込み操作</p>
<p><strong>種類</strong>操作の実行</p>

<p><i>Windows 1507 (TH1) バージョンの後-x86</i></p>
<p><strong>0</strong>読み取り操作</p>
<p><strong>2:</strong>書き込み操作</p>
<p><strong>種類</strong>操作の実行</p>

<p><i>Windows 1507 (TH1) バージョンの後-ARM</i></p>
<p><strong>0</strong>読み取り操作</p>
<p><strong>1:</strong>書き込み操作</p>
<p><strong>8</strong>操作の実行</p>

<p><i>Windows 1507 (TH1) バージョン x64/x86 より前</i></p>
<p><strong>0</strong>読み取り操作</p>
<p><strong>1:</strong>書き込み操作</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>参照されているメモリ (既知の場合) のアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>ページフォールトの種類</p>
<p>NONPAGED_BUGCHECK_WRONG_SESSION-セッション領域アドレスへの参照が、セッションを持たないプロセスのコンテキストで行われました。  通常、これは、適切なプロセスへのオブジェクト参照を適切に取得して最初にアタッチせずに、呼び出し元がセッションアドレスに不適切にアクセスしようとすることを意味します。 このバグチェック & サブタイプは、Windows 10 RS3 で最後に使用されました。  Windows 10 RS4 以降では、このエラーは代わりに 0x02 (NONPAGED_BUGCHECK_NOT_PRESENT_PAGE_TABLE) として表示されます。</p>
<p>0x04-NONPAGED_BUGCHECK_VA_NOT_CANONICAL-非正規 (無効) 仮想アドレス (パラメーター 1) への参照が試行されました。  呼び出し元は、このアドレスにアクセスしようとすることはできません。</p>
</td>
</tr>
</tbody>
</table>

 
エラーの原因となっているドライバーを識別できる場合は、その名前が青色の画面に出力され、メモリ内の場所\_(punicode 文字列) **KiBugCheckDriver**に格納されます。 デバッガーの dx コマンドを使用して、この- `dx KiBugCheckDriver`を表示できます。

<a name="cause"></a>原因
-----

バグチェック0x50 は、問題のあるシステムサービスのインストールまたはドライバーコードの不具合が原因で発生する可能性があります。 ウイルス対策ソフトウェアは、NTFS ボリュームが破損している可能性があるため、このエラーをトリガーすることもできます。

また、障害が発生したハードウェアをインストールした後、またはインストールされたハードウェアの障害が発生した場合にも発生する可能性があります (通常は、欠陥のある RAM、メインメモリ、L2 RAM キャッシュ、またはビデオ RAM)。


<a name="remarks"></a>コメント
----------

**イベントログ:** エラーの原因となっているデバイスまたはドライバーの特定に役立つ可能性のある追加のエラーメッセージについては、イベントビューアーのシステムログを確認してください。 詳細については、「 [Open イベントビューアー](https://support.microsoft.com/hub/4338813/windows-help#1TC=windows-7)」を参照してください。 ブルースクリーンと同じ時間枠内に発生したシステムログの重大なエラーを探します。

**問題のあるドライバーの解決:** 青い画面に表示されているか、イベントログに記録されている場合は、ドライバーの名前を確認します。 ドライバーの製造元に問い合わせて、更新されたドライバーが利用可能かどうかを確認してください。 

**障害が発生しているシステムサービスの問題の解決:** サービスを無効にし、これによってエラーが解決されることを確認します。 その場合は、システムサービスの製造元に連絡して、可能性のある更新プログラムを入手してください。 システムの起動中にエラーが発生した場合は、Windows の修復オプションを調べてください。 詳細については、「 [Windows 10 の回復オプション](https://support.microsoft.com/help/12415/windows-10-recovery-options)」を参照してください。

**ウイルス対策ソフトウェアの問題の解決:** プログラムを無効にし、これによってエラーが解決されることを確認します。 更新されている場合は、プログラムの製造元に問い合わせてください。

**破損した NTFS ボリュームの問題の解決:** **Chkdsk/f/r**を実行して、ディスクエラーを検出して修復します。 システムパーティションでディスクスキャンを開始する前に、システムを再起動する必要があります。 ハードドライブシステムの製造元に問い合わせて、ハードドライブサブシステム用に提供されている診断ツールを見つけます。

**Windows メモリ診断:** Windows メモリ診断ツールを実行して、物理メモリをテストします。 [スタート] ボタンをクリックし、[コントロールパネル] をクリックします。 検索ボックスに「Memory」と入力し、[*コンピューターのメモリの問題を診断する*] をクリックします。テストの実行後、イベントビューアーを使用して、システムログの下に結果を表示します。 結果を表示するには、 *Memorydiagnostics-results*エントリを探します。

**欠陥のあるハードウェアの問題の解決:** ハードウェアが最近システムに追加されている場合は、それを削除して、エラーが引き続き発生するかどうかを確認します。 既存のハードウェアに障害が発生した場合は、問題のあるコンポーネントを削除または交換します。 システムの製造元から提供されているハードウェア診断を実行する必要があります。 これらの手順の詳細については、コンピューターの所有者のマニュアルを参照してください。

ブルースクリーンの一般的なトラブルシューティング情報については、「 [**Blue Screen Data**](blue-screen-data.md)」を参照してください。

<a name="resolution"></a>解決方法
----------

通常、参照先のアドレスは解放されたメモリ内にあるか、単に無効になっています。 これは、 **try-except**ハンドラーによって保護することはできません。プローブまたは同様のプログラミング手法によってのみ保護できます。

-V verbose オプションを指定して、 [ **! analyze**](-analyze.md)デバッグ拡張機能を使用して、バグチェックに関する情報を表示し、根本原因を特定します。

```dbgcmd
2: kd> !analyze -v
*******************************************************************************
*                                                                             *
*                        Bugcheck Analysis                                    *
*                                                                             *
*******************************************************************************

PAGE_FAULT_IN_NONPAGED_AREA (50)
Invalid system memory was referenced.  This cannot be protected by try-except.
Typically the address is just plain bad or it is pointing at freed memory.
Arguments:
Arg1: ffffffff00000090, memory referenced.
Arg2: 0000000000000000, value 0 = read operation, 1 = write operation.
Arg3: fffff80240d322f9, If non-zero, the instruction address which referenced the bad memory
    address.
Arg4: 000000000000000c, (reserved)
```

この例では、パラメーター2は、メモリ領域が読み取られたときにバグチェックが発生したことを示します。

すべての! analyze 出力を調べて、バグチェックが発生したときの状況に関する情報を取得します。 モジュール名: と FAULTING_MODULE: を調べて、無効なシステムメモリの参照に関係するコードを確認します。

エラーが発生したときに実行されていたことに関する手掛かりについては、スタックテキストを参照してください。 複数のダンプファイルが使用可能な場合は、情報を比較して、スタック内の共通コードを探します。

! Analyze 出力に指定された. trap コマンドを使用して、コンテキストを設定します。

```dbgcmd
TRAP_FRAME:  fffff98112e8b3d0 -- (.trap 0xfffff98112e8b3d0)
```

 [**Kb (スタックバックトレースの表示)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)などのデバッガーコマンドを使用して、エラーが発生しているコードを調査します。

`lm t n`を使用して、メモリに読み込まれているモジュールの一覧を表示します。

パラメーター1とパラメーター3によって参照されるメモリ領域を調べるには、 [d、da、db、dc、dd、dd、df、dp、dq、du、dw (Display Memory)](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)コマンドを使用します。

```dbgcmd
2: kd> db ffffffff00000090
ffffffff`00000090  ?? ?? ?? ?? ?? ?? ?? ??-?? ?? ?? ?? ?? ?? ?? ??  ????????????????
ffffffff`000000a0  ?? ?? ?? ?? ?? ?? ?? ??-?? ?? ?? ?? ?? ?? ?? ??  ????????????????
ffffffff`000000b0  ?? ?? ?? ?? ?? ?? ?? ??-?? ?? ?? ?? ?? ?? ?? ??  ????????????????
ffffffff`000000c0  ?? ?? ?? ?? ?? ?? ?? ??-?? ?? ?? ?? ?? ?? ?? ??  ????????????????
ffffffff`000000d0  ?? ?? ?? ?? ?? ?? ?? ??-?? ?? ?? ?? ?? ?? ?? ??  ????????????????
ffffffff`000000e0  ?? ?? ?? ?? ?? ?? ?? ??-?? ?? ?? ?? ?? ?? ?? ??  ????????????????
ffffffff`000000f0  ?? ?? ?? ?? ?? ?? ?? ??-?? ?? ?? ?? ?? ?? ?? ??  ????????????????
ffffffff`00000100  ?? ?? ?? ?? ?? ?? ?? ??-?? ?? ?? ?? ?? ?? ?? ??  ????????????????
```
この場合、パラメーター1のメモリ領域にデータがあるように見えません。これは、読み取りを試みたメモリ領域です。

[! Address](-address.md)コマンドを使用して、無効なメモリを参照する命令のアドレスであるパラメーター3を確認します。

```dbgcmd
2: kd> !address fffff80240d322f9
Usage:                  Module
Base Address:           fffff802`40ca8000
End Address:            fffff802`415fb000
Region Size:            00000000`00953000
VA Type:                BootLoaded
Module name:            ntoskrnl.exe
Module path:            [\SystemRoot\system32\ntoskrnl.exe]
```

パラメーター3で[u, ub, uu (unassemble)](u--unassemble-.md)を使用して、無効なメモリが参照されているを確認します。 X64 プロセッサとアセンブリ言語の詳細について[は、「X64 プロセッサ](the-x64-processor.md)」を参照してください。 

```dbgcmd
2: kd> u fffff80240d322f9 
nt!RtlSubtreePredecessor+0x9:
fffff802`40d322f9 488b4810        mov     rcx,qword ptr [rax+10h]
fffff802`40d322fd eb07            jmp     nt!RtlSubtreePredecessor+0x16 (fffff802`40d32306)
fffff802`40d322ff 488bc1          mov     rax,rcx
fffff802`40d32302 488b4910        mov     rcx,qword ptr [rcx+10h]
fffff802`40d32306 4885c9          test    rcx,rcx
fffff802`40d32309 75f4            jne     nt!RtlSubtreePredecessor+0xf (fffff802`40d322ff)
fffff802`40d3230b c3              ret
fffff802`40d3230c c3              ret
```

指定`ub`されたアドレスから後方への逆アセンブルに使用します。

[ [R (レジスタ)](r--registers-.md) ] コマンドを使用して、システムバグがチェックされたときに実行された内容を確認します。 

```dbgcmd
2: kd> r
Last set context:
rax=ffffffff00000080 rbx=0000000000000000 rcx=ffffa68337cb7028
rdx=7a107838c48dfc00 rsi=0000000000000000 rdi=0000000000000000
rip=fffff80240d322f9 rsp=ffff840c96510958 rbp=ffffffffffffffff
 r8=ffffffffffffffff  r9=0000000000000000 r10=7ffffffffffffffc
r11=ffff840c96510a10 r12=0000000000000000 r13=0000000000000000
r14=0000000000000000 r15=0000000000000000
iopl=0         nv up ei ng nz na pe nc
cs=0010  ss=0018  ds=0000  es=0000  fs=0000  gs=0000             efl=00010282
nt!RtlSubtreePredecessor+0x9:
fffff802`40d322f9 488b4810        mov     rcx,qword ptr [rax+10h] ds:ffffffff`00000090=????????????????
```

この場合`fffff80240d322f9` 、は命令ポインターレジスタである rip です。

`!pte` と`!pool`コマンドを使用して、メモリを調べることもできます。

および`!memusage`を使用して、システムメモリの一般的な状態を確認します。 

**ドライバーの検証ツール**

ドライバーの検証ツールは、ドライバーの動作を確認するためにリアルタイムで実行されるツールです。 たとえば、ドライバーの検証ツールは、メモリプールなどのメモリリソースの使用を確認します。 ドライバーコードの実行中にエラーが発生した場合は、ドライバーコードのその部分をさらに詳しく調査できるように、例外を事前に作成します。 Driver verifier マネージャーは Windows に組み込まれており、すべての Windows Pc で使用できます。 ドライバー検証マネージャーを起動するには、コマンドプロンプトで「 *Verifer* 」と入力します。 確認するドライバーを構成できます。 ドライバーを検証するコードは、実行中のオーバーヘッドを追加するので、可能な限り最小のドライバー数を試してみてください。 詳細については、「 [Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)」を参照してください。

