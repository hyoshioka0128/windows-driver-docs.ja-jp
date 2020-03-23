---
title: バグ チェック 0x50 PAGE_FAULT_IN_NONPAGED_AREA
description: PAGE_FAULT_IN_NONPAGED_AREA バグ チェックの値は 0x00000050 です。 これは、無効なシステム メモリが参照されたことを示します。
ms.assetid: 63b4ab82-f7a9-4e14-bf7c-707a22d7e251
keywords:
- バグ チェック 0x50 PAGE_FAULT_IN_NONPAGED_AREA
- PAGE_FAULT_IN_NONPAGED_AREA
ms.date: 04/18/2019
topic_type:
- apiref
api_name:
- PAGE_FAULT_IN_NONPAGED_AREA
api_type:
- NA
ms.localizationpriority: high
ms.openlocfilehash: c161f61dd3a5b08aa69dcfa8edb170eb31612dae
ms.sourcegitcommit: e1cfed28850a8208ea27e7a6a336de88c48e9948
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78402346"
---
# <a name="bug-check-0x50-page_fault_in_nonpaged_area"></a>バグ チェック 0x50:PAGE\_FAULT\_IN\_NONPAGED\_AREA


PAGE\_FAULT\_IN\_NONPAGED\_AREA バグ チェックの値は 0x00000050 です。 これは、無効なシステム メモリが参照されたことを示します。 通常は、メモリ アドレスが間違っているか、解放されたメモリがメモリ アドレスで指し示されています。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルー スクリーン エラー コードが表示される場合は、「[ブルー スクリーン エラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="page_fault_in_nonpaged_area-parameters"></a>PAGE\_FAULT\_IN\_NONPAGED\_AREA のパラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>参照されているメモリ アドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left">
<p><i>Windows 1507 (TH1) バージョン以降 - x64 </i> </p>
<p><strong>0:</strong> 読み取り操作</p>
<p><strong>2:</strong> 書き込み操作</p>
<p><strong>10:</strong> 実行操作</p>

<p><i>Windows 1507 (TH1) バージョン以降 - x86 </i></p>
<p><strong>0:</strong> 読み取り操作</p>
<p><strong>2:</strong> 書き込み操作</p>
<p><strong>10:</strong> 実行操作</p>

<p><i>Windows 1507 (TH1) バージョン以降 - ARM </i></p>
<p><strong>0:</strong> 読み取り操作</p>
<p><strong>1:</strong> 書き込み操作</p>
<p><strong>8:</strong> 実行操作</p>

<p><i>Windows 1507 (TH1) バージョンより前 - x64/x86 </i></p>
<p><strong>0:</strong> 読み取り操作</p>
<p><strong>1:</strong> 書き込み操作</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>メモリを参照したアドレス (わかっている場合)</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>ページ フォールトの種類</p>
<p>0x03 - NONPAGED_BUGCHECK_WRONG_SESSION - セッションを持たないプロセスのコンテキストで、セッション領域アドレスへの参照が試みられました。  通常、これは、呼び出し元が、最初に正しいプロセスへのオブジェクト参照を適切に取得してアタッチせずに、セッション アドレスに不適切にアクセスしようとしていることを意味します。 このバグ チェックとサブタイプが最後に使用されたのは Windows 10 RS3 です。  Windows 10 RS4 以降では、このエラーは、代わりに 0x02 (NONPAGED_BUGCHECK_NOT_PRESENT_PAGE_TABLE) として表示されます。</p>
<p>0x04 - NONPAGED_BUGCHECK_VA_NOT_CANONICAL - 非正規 (無効) な仮想アドレス (パラメーター 1) への参照が試みられました。  呼び出し元がこのアドレスにアクセスしようとすることはできません。</p>
</td>
</tr>
</tbody>
</table>

 
エラーの原因となったドライバーを特定できる場合は、その名前がブルー スクリーンに出力され、メモリ内の場所 (PUNICODE\_STRING) **KiBugCheckDriver** に格納されます。 デバッガーの dx コマンドを使用して、これを表示できます: `dx KiBugCheckDriver`。

<a name="cause"></a>原因
-----

バグ チェック 0x50 は、問題のあるシステム サービスまたは問題のあるドライバー コードのインストールが原因で発生する可能性があります。 破損した NTFS ボリュームと同様、ウイルス対策ソフトウェアでこのエラーがトリガーされる可能性もあります。

また、問題のあるハードウェアをインストールした後や、インストールしたハードウェアで障害が発生した場合にも、発生する可能性があります (通常は、メイン メモリ、L2 RAM キャッシュ、ビデオ RAM などの欠陥のある RAM に関係します)。


<a name="remarks"></a>コメント
----------

**イベント ログ:** イベント ビューアーを使用してシステム ログで追加のエラー メッセージを確認すると、エラーの原因になっているデバイスやドライバーを特定できる可能性があります。 詳しくは、[イベント ビューアーの使用](https://support.microsoft.com/hub/4338813/windows-help#1TC=windows-7)に関するページをご覧ください。 ブルー スクリーンと同じ時間帯に発生した重大なエラーをシステム ログで探します。

**問題のあるドライバーの解決:** ドライバーがブルー スクリーンに表示されているか、イベント ログに記録されている場合は、その名前を確認します。 ドライバーの製造元に問い合わせて、更新されたドライバーが利用可能かどうかを確認します。 

**障害が発生しているシステム サービスの問題の解決:** サービスを無効にし、これによってエラーが解決されることを確認します。 その場合は、システム サービスの製造元に、更新プログラムを入手できるかどうかを確認します。 システムの起動中にエラーが発生する場合は、Windows の修復オプションを調べます。 詳しくは、「[Windows 10 の回復オプション](https://support.microsoft.com/help/12415/windows-10-recovery-options)」をご覧ください。

**ウイルス対策ソフトウェアの問題の解決:** プログラムを無効にし、これによってエラーが解決されることを確認します。 その場合は、プログラムの製造元に、更新プログラムを入手できるかどうかを確認します。

**破損した NTFS ボリュームの問題の解決:** **Chkdsk /f /r** を実行し、ディスク エラーを検出して修復します。 システム パーティションでディスク スキャンを開始する前に、システムを再起動する必要があります。 ハード ドライブ システムの製造元に問い合わせて、ハード ドライブ サブシステム用に提供されている診断ツールを入手します。

**Windows メモリ診断:** Windows メモリ診断ツールを実行して、物理メモリをテストします。 [スタート] ボタンをクリックし、[コントロール パネル] をクリックします。 検索ボックスに「メモリ」と入力し、"*お使いのコンピューターのメモリの問題の診断*" をクリックします。テストの実行後、イベント ビューアーを使用して、システム ログの結果を表示します。 *MemoryDiagnostics-Results* エントリを探して、結果を表示します。

**欠陥のあるハードウェアの問題の解決:** 最近システムにハードウェアを追加した場合は、それを外して、エラーが引き続き発生するかどうかを確認します。 既存のハードウェアで障害が発生した場合は、問題のあるコンポーネントを外すか交換します。 システムの製造元から提供されているハードウェア診断を実行する必要があります。 これらの手順の詳細については、コンピューターの取扱説明書を参照してください。

ブルー スクリーンの一般的なトラブルシューティングの情報については、「[**ブルー スクリーンのデータ**](blue-screen-data.md)」をご覧ください。

<a name="resolution"></a>解決方法
----------

通常は、参照されているアドレスが解放されたメモリ内にあるか、単に無効になっています。 これは、**try - except** ハンドラーでは保護できません。プローブまたは同様のプログラミング手法によってのみ保護できます。

[ **!analyze**](-analyze.md) デバッグ拡張機能を -v 詳細オプションと共に使用して、バグ チェックに関する情報を表示し、根本原因を特定します。

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

この例では、メモリ領域の読み取り時にバグ チェックが発生したことが、パラメーター 2 で示されています。

!analyze のすべての出力を調べて、バグ チェックが発生したときの状況に関する情報を取得します。 MODULE_NAME: および FAULTING_MODULE: を調べて、無効なシステム メモリの参照に関係するコードを確認します。

STACK TEXT で、障害が発生したときに実行されていたものに関する手掛かりを調べます。 複数のダンプ ファイルが使用可能な場合は、情報を比較して、スタック内の共通するコードを探します。

!analyze の出力で提供されている .trap コマンドを使用して、コンテキストを設定します。

```dbgcmd
TRAP_FRAME:  fffff98112e8b3d0 -- (.trap 0xfffff98112e8b3d0)
```

 [**kb (スタック バックトレースの表示)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) などのデバッガー コマンドを使用して、問題のあるコードを調査します。

`lm t n` を使用して、メモリに読み込まれているモジュールの一覧を表示します。

[d、da、db、dc、dd、dD、df、dp、dq、du、dw (メモリの表示)](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md) コマンドを使用して、パラメーター 1 とパラメーター 3 によって参照されているメモリ領域を調べます。

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
次の例では、このパラメーター 1 のメモリ領域にはデータが存在するように見えません。これが、読み取りを試みたメモリ領域です。

[!address](-address.md) コマンドを使用して、無効なメモリを参照した命令のアドレスであるパラメーター 3 を確認します。

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

パラメーター 3 で [u、ub、uu (逆アセンブル)](u--unassemble-.md) を使用して、無効なメモリを参照したものを調べます。 X64 プロセッサとアセンブリ言語について詳しくは、「[x64 プロセッサ](the-x64-processor.md)」をご覧ください。 

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

`ub` を使用して、特定のアドレスから後方に逆アセンブルします。

[r (レジスタ)](r--registers-.md) コマンドを使用して、システム バグがチェックされたときに実行されていた内容を確認します。 

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

この場合、`fffff80240d322f9` は命令ポインター レジスタ rip 内にあります。

`!pte` コマンドと `!pool` コマンドも、メモリを調べるために使用できます。

`!memusage` を使用して、システム メモリの全般的な状態を確認します。 

**ドライバーの検証ツール**

ドライバーの検証ツールは、リアルタイムで実行してドライバーの動作を調べるためのツールです。 たとえば、ドライバーの検証ツールでは、メモリ プールなどのメモリ リソースの使用がチェックされます。 ドライバー コードの実行でエラーが検出された場合は、ドライバー コードのその部分をさらに詳しく調査できるように、事前に例外が作成されます。 ドライバーの検証ツール マネージャーは、Windows に組み込まれており、すべての Windows PC で使用できます。 ドライバーの検証ツール マネージャーを起動するには、コマンド プロンプトで「*Verifier*」と入力します。 どのドライバーを検証するかを構成できます。 ドライバーを検証するコードが実行されるとオーバーヘッドが増えるので、可能な限り少ない数のドライバーで試してみてください。 詳細については、「[ドライバーの検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)」を参照してください。

