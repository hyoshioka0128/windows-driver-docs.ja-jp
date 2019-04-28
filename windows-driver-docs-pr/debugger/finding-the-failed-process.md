---
title: エラーが発生したプロセスの検索
description: エラーが発生したプロセスの検索
ms.assetid: 64d1fa71-940f-4f67-87a6-00d41d6f24e0
keywords:
- 失敗したプロセス検索プロセス
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b13581d75dcb0a68d9b8840af69f741a90b38ec8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372338"
---
# <a name="finding-the-failed-process"></a>エラーが発生したプロセスの検索


## <span id="ddk_finding_the_failed_process_dbg"></span><span id="DDK_FINDING_THE_FAILED_PROCESS_DBG"></span>


失敗したプロセスを検索するには、前に、受け入れ側のプロセッサのコンテキストであることを確認します。 受け入れのプロセッサを調べるには、 [ **! pcr** ](-pcr.md)各プロセッサの拡張機能の例外ハンドラーが読み込まれたプロセッサを探します。 受け入れのプロセッサの例外ハンドラーが、0 xffffffff 以外のアドレス。

たとえば、ためのアドレス**NtTib.ExceptionList**このプロセッサは 0 xffffffff、これは、失敗したプロセスのプロセッサではありません。

```dbgcmd
0: kd> !pcr 
PCR Processor 0 @ffdff000
 NtTib.ExceptionList: ffffffff
            NtTib.StackBase: 80470650
           NtTib.StackLimit: 8046d860
         NtTib.SubSystemTib: 00000000
              NtTib.Version: 00000000
          NtTib.UserPointer: 00000000
              NtTib.SelfTib: 00000000

                    SelfPcr: ffdff000
                       Prcb: ffdff120
                       Irql: 00000000
                        IRR: 00000000
                        IDR: ffffffff
              InterruptMode: 00000000
                        IDT: 80036400
                        GDT: 80036000
                        TSS: 80257000

              CurrentThread: 8046c610
                 NextThread: 00000000
                 IdleThread: 8046c610

                  DpcQueue: 
```

ただし、プロセッサ 1 の結果は大きく異なります。 この例では、値で**NtTib.ExceptionList**は**f0823cc0**、いない 0 xffffffff、例外が発生したプロセッサであることを示します。

```dbgcmd
0: kd> ~1 
1: kd> !pcr
PCR Processor 1 @81497000
 NtTib.ExceptionList: f0823cc0
            NtTib.StackBase: f0823df0
           NtTib.StackLimit: f0821000
         NtTib.SubSystemTib: 00000000
              NtTib.Version: 00000000
          NtTib.UserPointer: 00000000
              NtTib.SelfTib: 00000000

                    SelfPcr: 81497000
                       Prcb: 81497120
                       Irql: 00000000
 IRR: 00000000
                        IDR: ffffffff
              InterruptMode: 00000000
                        IDT: 8149b0e8
 GDT: 8149b908
                        TSS: 81498000

              CurrentThread: 81496d28
                 NextThread: 00000000
                 IdleThread: 81496d28

                  DpcQueue: 
```

適切なプロセッサのコンテキストでは、 [ **! プロセス**](-process.md)拡張機能が現在実行中のプロセスを表示します。

プロセスのダンプの最も興味深い部分は次のとおりです。

-   時間 (高の値は、プロセスが原因であることを示します)。

-   ハンドル数 (これは、後にかっこで囲まれた番号**ObjectTable**最初のエントリで)。

-   (多くのプロセスがある複数のスレッド) スレッドの状態。 現在のプロセスがある場合*Idle*、いずれか、マシンが本当にアイドル状態か、通常とは異なる問題があるため、ハングしている可能性があります。

使用していますが、 **! 0 7 処理**拡張機能がハングしたシステム上の問題を検索する最善の方法で、フィルター処理する情報が多すぎる場合があります。 代わりに、使用、 **! process 0 0**をクリックし、 **! プロセス**CSRSS およびその他のすべての不審なプロセスのプロセスのハンドル。

使用する場合、 **! 0 7 処理**、多くのスレッドの可能性があります「カーネル スタックが存在しない」ため、設定、スタックをページ アウトします。これらのページがまだ移行されているキャッシュにある場合を使用して詳細を表示できます、 **.cache decodeptes**する前に **! 0 7 処理**:

```dbgcmd
kd> .cache decodeptes 
kd> !process 0 7 
```

失敗したプロセスを特定した場合は、使用 **! プロセス** *&lt;プロセス&gt;* **7**プロセスの各スレッドのカーネル スタックを表示します。 この出力では、カーネル モードでの問題を特定でき、問題のあるプロセスの呼び出しを表示することができます。

ほかに **! プロセス**、次の拡張機能が応答しないコンピューターの原因を特定するのに役立ちます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">拡張</th>
<th align="left">効果</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong><a href="-ready.md" data-raw-source="[!ready](-ready.md)">! 準備完了</a></strong></p></td>
<td align="left"><p>優先順位の順序で、実行する準備ができているスレッドを識別します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-locks---kdext--locks-.md" data-raw-source="[!kdext*.locks](-locks---kdext--locks-.md)">!kdext*.locks</a></strong></p></td>
<td align="left"><p>製品版のタイムアウトでデッドロックがある場合は、すべて保持されているリソースのロックを識別します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-vm.md" data-raw-source="[!vm](-vm.md)">!vm</a></strong></p></td>
<td align="left"><p>仮想メモリ使用量を確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-poolused.md" data-raw-source="[!poolused](-poolused.md)">! poolused</a></strong></p></td>
<td align="left"><p>プールの割り当ての 1 つの種類が過度に大きいかどうかを判断します (プールは、必要なタグ付け)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-memusage.md" data-raw-source="[!memusage](-memusage.md)">! memusage</a></strong></p></td>
<td align="left"><p>物理メモリの状態を確認します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong><a href="-heap.md" data-raw-source="[!heap](-heap.md)">! ヒープ</a></strong></p></td>
<td align="left"><p>ヒープの有効性を確認します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong><a href="-irpfind.md" data-raw-source="[!irpfind](-irpfind.md)">! irpfind</a></strong></p></td>
<td align="left"><p>アクティブな Irp の非ページ プールを検索します。</p></td>
</tr>
</tbody>
</table>

 

提供される情報が、異常な状態を表していない場合は、ブレークポイントを設定してください**ntoskrnl!。KiSwapThread**プロセッサが 1 つのプロセスでスタックしているかどうか、または他のプロセスをまだスケジュールはかどうかを判断します。 なっていない場合にブレークポイントを設定、共通の関数など**NtReadFile**コンピューターが特定のコード パスでスタックしているかどうかを決定します。

 

 





