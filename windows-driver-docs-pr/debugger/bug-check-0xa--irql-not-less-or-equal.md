---
title: バグ チェック 0 xa IRQL_NOT_LESS_OR_EQUAL
description: IRQL_NOT_LESS_OR_EQUAL のバグ チェックでは、0x0000000A の値を持ちます。
ms.assetid: a32b80f5-9822-41af-8668-836a70b05c0f
keywords:
- バグ チェック 0 xa IRQL_NOT_LESS_OR_EQUAL
- IRQL_NOT_LESS_OR_EQUAL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- IRQL_NOT_LESS_OR_EQUAL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 690a62bee6b12046c57ef4bf430d7de4b6564758
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "59239463"
---
# <a name="bug-check-0xa-irqlnotlessorequal"></a>バグ チェック 0xA:IRQL\_いない\_少ない\_または\_と等しい


IRQL\_いない\_少ない\_または\_等しいバグ チェックが 0x0000000A の値を持ちます。 これは、Microsoft Windows またはカーネル モード ドライバーにアクセスが発生した割り込み要求レベル (IRQL) で、無効なアドレスのメモリをページングを示します。 これは通常、不正なポインターまたは pageability 問題のいずれか。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="irqlnotlessorequal-parameters"></a>IRQL\_いない\_少ない\_または\_等しいパラメーター


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
<td align="left"><p>仮想メモリ アドレスは、アクセスできませんでした。</p>
<p>使用 <strong><a href="-pool.md" data-raw-source="[!pool](-pool.md)">! プール</a></strong>ページ プールがあるかどうかを確認するには、このアドレスでします。 これらのコマンドの場合、エラーに関する情報の収集に役立ちますもあります <strong><a href="-pte.md" data-raw-source="[!pte](-pte.md)">! pte</a></strong>、  <strong><a href="-address.md" data-raw-source="[!address](-address.md)">! アドレス</a></strong>、および<strong>。<a href="ln--list-nearest-symbols-.md" data-raw-source="[ln (List Nearest Symbols)](ln--list-nearest-symbols-.md)">ln (一番近いシンボル リスト)</a></strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>IRQL の障害時にします。</p>
<p>値:</p>
<p>2 :IRQL は、障害の時点で DISPATCH_LEVEL をしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>エラーの原因となった操作を示すビット フィールド。</p>
<p><strong>ビット 0:</strong></p>
<p>値:</p>
<p>0:読み取り操作</p>
<p>1:書き込み操作</p>
<p><strong>ビット 3:</strong>(このレベルのレポートをサポートするチップセットでは使用のみ)。</p>
<p>値:</p>
<p>0:Execute 操作ではありません。</p>
<p>1:操作を実行します。</p>
<strong>ビット 0、ビット 3 は、合計の値を取得します。</strong>
<p>0x0 :パラメーター 1 でアドレスからの読み取り専用にしようとしてエラー。</p>
<p>0x1:パラメーター 1 のアドレスに書き込みをしようとしてエラー。</p>
<p>0x8:パラメーター 1 でアドレスからコードを実行しようとするエラー。</p>
<p>この値は、通常に発生します。</p>
<ul>
<li>関数を呼び出すことは、DISPATCH_LEVEL しながら DISPATCH_LEVEL で呼び出すことができません。</li>
<li>スピンロックを解放し忘れた</li>
<li>ページング可能としてコードをマークする (例: コード、スピンロックが獲得または DPC で呼び出される) ため、非ページングされる必要があります。</li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>エラーの時点で、命令ポインター。</p>
<p>使用して、 <strong><a href="ln--list-nearest-symbols-.md" data-raw-source="[ln (List Nearest Symbols)](ln--list-nearest-symbols-.md)">ln (最も近いシンボルの一覧)</a></strong>関数の名前を表示するには、このアドレスでコマンド。</p></td>
</tr>
</tbody>
</table>

<a name="cause"></a>原因
-----

0 xa のバグ チェックは通常、不適切なアドレスを使用してカーネル モード デバイス ドライバーが原因です。

このバグ チェックでは、発生した割り込み要求レベル (IRQL) で、無効なアドレスにアクセスしようとすることを示します。 これは、不良メモリのポインターまたはデバイス ドライバーのコードに pageability 問題のいずれか。

使用できるいくつかの一般的なガイドラインを示します。 catergorize をコーディング エラー tha の種類のバグ チェック原因となった。

- パラメーター 1 が 0x1000 未満の場合は、これが NULL ポインターの逆参照する可能性があります。

- 場合[! プール](-pool.md)パラメーター 1 がページ プール (またはその他の種類のページング可能なメモリ)、し、このデータにアクセスするには、IRQL が大きすぎることをレポートします。 下の IRQL で実行するか、NonPagedPool 内のデータを割り当てます。

- 3 番目のパラメーターは、ページング可能なコードを実行しようとしたこのことを示している場合は、IRQL がこの関数を呼び出す高すぎます。 低い IRQL で実行するか、コードをページング可能としてマークを付けないでください。

- それ以外の場合、無効なポインターは、無料使用後に、またはビットの反転である可能性があります。 パラメーター 1 での有効性を調査[ **! pte**](-pte.md)、 [ **! アドレス**](-address.md)、および[ **ln (リスト最も近いシンボルの除去)**](ln--list-nearest-symbols-.md)します。


<a name="resolution"></a>解決方法
----------

カーネル デバッガーを使用できる場合は、スタック トレースを取得します、 [ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)デバッグ拡張機能を、根本原因を突き止めるのに役立ちますし、、のいずれかを入力できますとバグチェックに関する情報が表示されます。[**k (Display Stack Backtrace)** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-)呼び出し履歴を表示するコマンド。

**情報を収集します。**

ブルー スクリーンに表示されている場合は、ドライバーの名前を確認します。

デバイスまたはエラーの原因となっているドライバーの特定に役立つ可能性がある追加のエラー メッセージをイベント ビューアーのシステム ログを確認します。 詳細については、次を参照してください。[イベント ビューアーを開く](https://windows.microsoft.com/windows/what-information-event-logs-event-viewer#1TC=windows-7)します。 ブルー スクリーンに同じ期間に発生したシステム ログの重大なエラーを探します。

**ドライバーの検証ツール**

Driver Verifier は、ドライバーの動作を確認するのにはリアルタイムで実行されているツールです。 たとえば、Driver Verifier は、メモリ プールなどのメモリ リソースの使用を確認します。 ドライバー コードの実行でエラーが表示される、さらに細かく検証するドライバー コードの部分を許可する例外が事前に作成されます。 ドライバー検証マネージャーは、Windows に組み込まれているしはすべての Windows Pc で使用できます。 ドライバー検証マネージャーを起動する入力*Verifer*コマンド プロンプトでします。 確認するにはどのドライバーを構成することができます。 ドライバーを検証するコードは実行時にオーバーヘッドを追加、のでお試しくださいし、可能なドライバーの最小数を確認します。 詳細については、次を参照してください。 [Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)します。

デバッグの例を次に示します。

```dbgcmd
kd> .bugcheck       [Lists bug check data.]
Bugcheck code 0000000a
Arguments 00000000 0000001c 00000000 00000000

kd> kb [Lists the stack trace.]
ChildEBP RetAddr  Args to Child
8013ed5c 801263ba 00000000 00000000 e12ab000 NT!_DbgBreakPoint
8013eecc 801389ee 0000000a 00000000 0000001c NT!_KeBugCheckEx+0x194
8013eecc 00000000 0000000a 00000000 0000001c NT!_KiTrap0E+0x256
8013ed5c 801263ba 00000000 00000000 e12ab000
8013ef64 00000246 fe551aa1 ff690268 00000002 NT!_KeBugCheckEx+0x194

kd> kv [Lists the trap frames.]
ChildEBP RetAddr  Args to Child
8013ed5c 801263ba 00000000 00000000 e12ab000 NT!_DbgBreakPoint (FPO: [0,0,0])
8013eecc 801389ee 0000000a 00000000 0000001c NT!_KeBugCheckEx+0x194
8013eecc 00000000 0000000a 00000000 0000001c NT!_KiTrap0E+0x256 (FPO: [0,0] TrapFrame @ 8013eee8)
8013ed5c 801263ba 00000000 00000000 e12ab000
8013ef64 00000246 fe551aa1 ff690268 00000002 NT!_KeBugCheckEx+0x194

kd> .trap 8013eee8 [Gets the registers for the trap frame at the time of the fault.]
eax=dec80201 ebx=ffdff420 ecx=8013c71c edx=000003f8 esi=00000000 edi=87038e10
eip=00000000 esp=8013ef5c ebp=8013ef64 iopl=0         nv up ei pl nz na pe nc
cs=0008  ss=0010  ds=0023  es=0023  fs=0030  gs=0000             efl=00010202
ErrCode = 00000000
00000000 ???????????????    [The current instruction pointer is NULL.]

kd> kb       [Gives the stack trace before the fault.]
ChildEBP RetAddr  Args to Child
8013ef68 fe551aa1 ff690268 00000002 fe5620d2 NT!_DbgBreakPoint
8013ef74 fe5620d2 fe5620da ff690268 80404690
NDIS!_EthFilterIndicateReceiveComplete+0x31
8013ef64 00000246 fe551aa1 ff690268 00000002 elnkii!_ElnkiiRcvInterruptDpc+0x1d0
```

<a name="remarks"></a>コメント
-------

通常、このバグの確認を生成するエラーは、障害のあるデバイス ドライバー、システム サービス、または BIOS のインストール後に発生します。

以降のバージョンの Windows へのアップグレード中のバグ チェック 0 xa、発生した場合、このエラーは、デバイス ドライバーやシステム サービス、ウイルス スキャナーでは、新しいバージョンと互換性のないバックアップ ツールで発生する可能性があります。

**障害のあるハードウェアの問題を解決するには。** システム ハードウェアが最近追加された場合は、エラーが再発するかどうかに表示することを削除します。 既存のハードウェアが失敗した場合は、削除または障害のあるコンポーネントの交換します。 システム製造元から提供されたハードウェア診断を実行する必要があります。 詳細については、これらの手順は、コンピューターの製造元のマニュアルを参照してください。

**障害のあるシステム サービスの問題を解決するには。** サービスを無効にし、これによって、エラーが解決することを確認します。 そうである場合は、可能な更新プログラムのシステム サービスの製造元にお問い合わせください。 システムの起動中にエラーが発生する場合は、Windows の修復オプションを調査します。 詳細については、次を参照してください。 [Windows 10 での回復オプション](https://windows.microsoft.com/windows-10/windows-10-recovery-options)します。

**ウイルス対策ソフトウェアの問題を解決するには。** プログラムを無効にし、これによって、エラーが解決することを確認します。 その場合、可能な更新プログラムのプログラムの製造元に問い合わせてください。

一般的なブルー スクリーンがトラブルシューティング情報について、次を参照してください。 [**青い画面データ**](blue-screen-data.md)します。
