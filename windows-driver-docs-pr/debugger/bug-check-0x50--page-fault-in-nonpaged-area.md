---
title: バグ チェック 0x50 してください。
description: くださいのバグ チェックでは、0x00000050 の値を持ちます。 これは、無効なシステム メモリが参照されていることを示します。
ms.assetid: 63b4ab82-f7a9-4e14-bf7c-707a22d7e251
keywords:
- バグ チェック 0x50 してください。
- PAGE_FAULT_IN_NONPAGED_AREA
ms.date: 04/18/2019
topic_type:
- apiref
api_name:
- PAGE_FAULT_IN_NONPAGED_AREA
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2ce3e13240f76ca688c60ea0ecc0589a3a72cb98
ms.sourcegitcommit: 844841c21dd9961311cba589782e73bac4de5dbd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/09/2019
ms.locfileid: "67693343"
---
# <a name="bug-check-0x50-pagefaultinnonpagedarea"></a>バグ チェック 0x50:ページ\_フォールト\_IN\_非ページ\_領域


ページ\_フォールト\_IN\_非ページ\_領域のバグ チェックが 0x00000050 の値を持ちます。 これは、無効なシステム メモリが参照されていることを示します。 通常、メモリ アドレスが間違っているか、メモリ アドレスが解放されたメモリを指しています。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="pagefaultinnonpagedarea-parameters"></a>ページ\_フォールト\_IN\_非ページ\_領域のパラメーター


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
<p><i>Windows 1507 (TH1) バージョン - x64 </i> </p>
<p><strong>0:</strong>読み取り操作</p>
<p><strong>2:</strong>書き込み操作</p>
<p><strong>10:</strong>操作を実行します。</p>

<p><i> Windows 1507 (TH1) バージョン - x86 </i></p>
<p><strong>0:</strong>読み取り操作</p>
<p><strong>2:</strong>書き込み操作</p>
<p><strong>10:</strong>操作を実行します。</p>

<p><i> Windows 1507 (TH1) のバージョンの後に ARM </i></p>
<p><strong>0:</strong>読み取り操作</p>
<p><strong>1:</strong>書き込み操作</p>
<p><strong>8:</strong>操作を実行します。</p>

<p><i> 前の 1507 (TH1) バージョンの Windows x64 に、または x86 </i></p>
<p><strong>0:</strong>読み取り操作</p>
<p><strong>1:</strong>書き込み操作</p>
</td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>メモリ (わかる場合) を参照されているアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>ページ フォールトの種類</p>
<p>0x03 - NONPAGED_BUGCHECK_WRONG_SESSION - セッション空間アドレスへの実行しようとした参照が行われたセッションがないプロセスのコンテキストでします。  通常、呼び出し元が正しく、適切なプロセスへのオブジェクト参照を取得し、最初にアタッチすることがなく、セッションのアドレスへのアクセスに正しくしようとしてこれを意味します。 このバグチェック & サブタイプは、Windows 10 RS3 最後使用されました。  Windows 10 RS4 以降で、このエラーは代わりに 0x02 (NONPAGED_BUGCHECK_NOT_PRESENT_PAGE_TABLE) として表示します。</p>
<p>0x04 - NONPAGED_BUGCHECK_VA_NOT_CANONICAL - 非正規の (不正な) 仮想アドレス (パラメーター 1) を実行しようとした、参照が試行されました。  呼び出し元する必要がありますいないこととしているこのアドレスにアクセスします。</p>
</td>
</tr>
</tbody>
</table>

 
その名前がブルー スクリーンに印刷され、場所のメモリに格納されているドライバーのエラーの原因が識別できる場合 (PUNICODE\_文字列) **KiBugCheckDriver**します。 Dx のデバッガー コマンドを使用するには、これを表示する`dx KiBugCheckDriver`します。

<a name="cause"></a>原因
-----

システム障害のあるサービスまたは障害のあるドライバー コードのインストールによって、バグ チェック 0x50 可能性があります。 破損した NTFS ボリュームと同様、ウイルス対策ソフトウェアは、このエラーをトリガーもできます。

インストールされているハードウェアの障害のあるハードウェアまたはの障害が発生した場合、インストール後に発生する可能性も (通常は欠陥のあるメモリに関連してはメイン メモリ、RAM の L2 キャッシュ、またはビデオ RAM)。


<a name="remarks"></a>注釈
----------

**イベント ログ:** デバイスまたはエラーの原因となっているドライバーの特定に役立つ可能性がある追加のエラー メッセージをイベント ビューアーのシステム ログを確認します。 詳細については、次を参照してください。[イベント ビューアーを開く](https://support.microsoft.com/hub/4338813/windows-help#1TC=windows-7)します。 ブルー スクリーンに同じ期間に発生したシステム ログの重大なエラーを探します。

**障害のあるドライバーを解決するには。** ブルー スクリーンに表示されているかがイベント ログに存在する場合は、ドライバーの名前を確認します。 更新されたドライバが利用可能なドライバーのベンダーに問い合わせてください。 

**障害のあるシステム サービスの問題を解決するには。** サービスを無効にし、これによって、エラーが解決することを確認します。 そうである場合は、可能な更新プログラムのシステム サービスの製造元にお問い合わせください。 システムの起動中にエラーが発生する場合は、Windows の修復オプションを調査します。 詳細については、次を参照してください。 [Windows 10 での回復オプション](https://support.microsoft.com/help/12415/windows-10-recovery-options)します。

**ウイルス対策ソフトウェアの問題を解決するには。** プログラムを無効にし、これによって、エラーが解決することを確認します。 その場合、可能な更新プログラムのプログラムの製造元に問い合わせてください。

**NTFS ボリュームの破損の問題を解決するには。** 実行**Chkdsk/f/r**ディスク エラーを検出および修復します。 システム パーティションにディスクのスキャンが開始する前に、システムを再起動する必要があります。 ハード ディスク ドライブ サブシステムを提供する診断ツールを検索するハード ドライブのシステムの製造元に問い合わせてください。

**Windows メモリ診断:** 物理メモリをテストする、Windows メモリ診断ツールを実行します。 [スタート] ボタンと [コントロール パネル] をクリックします。 検索ボックスに、メモリを入力し、クリックして *、コンピューターのメモリの問題を診断*します。テストの実行後は、イベント ビューアーを使用して、システム ログで結果を表示します。 探して、 *MemoryDiagnostics 結果*結果を表示するエントリ。

**障害のあるハードウェアの問題を解決するには。** システム ハードウェアが最近追加された場合は、エラーが再発するかどうかに表示することを削除します。 既存のハードウェアが失敗した場合は、削除または障害のあるコンポーネントの交換します。 システム製造元から提供されたハードウェア診断を実行する必要があります。 詳細については、これらの手順は、コンピューターの製造元のマニュアルを参照してください。

一般的なブルー スクリーンがトラブルシューティング情報について、次を参照してください。 [**青い画面データ**](blue-screen-data.md)します。

<a name="resolution"></a>解決方法
----------

通常、参照先のアドレスは解放されたメモリでは、またはが単に無効です。 これで保護することはできません、 **- お試しくださいを除く**ハンドラー--のみを指定できます、プローブによって保護されているまたは類似のプログラミング手法です。

使用して、 [ **! 分析**](-analyze.md)根本原因を特定するためのバグ チェックに関する情報を表示 - v の詳細オプションを使用して拡張機能をデバッグします。

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

この例では、パラメーター 2 は、メモリの領域が読み込まれると、バグ チェックが発生したことを示します。

すべてを見て、! ものについての情報を取得する出力の分析バグ チェックが発生したときにします。 モジュール名を確認します。 および、FAULTING_MODULE: 無効なシステム メモリを参照するコードが関係しているかを確認します。

障害が発生したときに実行されていたものでスタック テキスト手がかりを確認します。 複数のダンプ ファイルが使用可能な場合は、情報を探す、スタックに共通のコードを比較します。

提供される .trap コマンドを使用して、!、コンテキストを設定する出力を分析します。

```dbgcmd
TRAP_FRAME:  fffff98112e8b3d0 -- (.trap 0xfffff98112e8b3d0)
```

 使用率などのデバッガー コマンドを使用して[ **kb (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)エラーが発生したコードを調査します。

使用して、`lm t n`メモリに読み込まれたモジュールを一覧表示します。

使用して、 [d、da、db、dc、dd、dD、df、dp、dq、du、dw (表示メモリ)](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)パラメーター 1 と 3 番目のパラメーターで参照されるメモリの領域を調査するコマンド。

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
ここでいないようで読み取りが試行しているメモリの領域は、パラメーター 1 では、メモリのこの領域にデータが存在します。

使用して、 [! アドレス](-address.md)アドレスである 3 番目のパラメーターを確認するコマンドの不良メモリを参照する命令です。

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

使用[u、ub、uu (Unassemble) Dissasemble](u--unassemble-.md)パラメーター 3、不良メモリ、参照されている、確認を使用します。 詳細については、X64 プロセッサとアセンブリ言語を参照してください[x64 プロセッサ](the-x64-processor.md)します。 

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

使用`ub`dissassemble から下位に、特定のアドレス。

使用して、 [r (レジスタ)](r--registers-.md)システムのバグ チェックとして実行されていた内容を確認するコマンド。 

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

ここで`fffff80240d322f9`命令ポインターでは、登録、取り込みます。

`!pte`と`!pool`コマンドは、メモリの確認にも使用可能性があります。

使用`!memusage`と、システム メモリの [全般] の状態を確認します。 

**ドライバーの検証ツール**

Driver Verifier は、ドライバーの動作を確認するのにはリアルタイムで実行されているツールです。 たとえば、Driver Verifier は、メモリ プールなどのメモリ リソースの使用を確認します。 ドライバー コードの実行でエラーが表示される、さらに細かく検証するドライバー コードの部分を許可する例外が事前に作成されます。 ドライバー検証マネージャーは、Windows に組み込まれているしはすべての Windows Pc で使用できます。 ドライバー検証マネージャーを起動する入力*Verifer*コマンド プロンプトでします。 確認するにはどのドライバーを構成することができます。 ドライバーを検証するコードは実行時にオーバーヘッドを追加、のでお試しくださいし、可能なドライバーの最小数を確認します。 詳細については、次を参照してください。 [Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)します。


**旅行時間のトレース**

バグ チェックはオンデマンドで再現できる場合は、WinDbg のプレビューを使用してタイム トラベル トレースを取ることの可能性を調査します。 詳細については、次を参照してください。[タイム トラベルのデバッグ - 概要](time-travel-debugging-overview.md)します。

