---
title: バグチェックの 0xA IRQL_NOT_LESS_OR_EQUAL
description: IRQL_NOT_LESS_OR_EQUAL バグチェックの値は0x0000000A です。
ms.assetid: a32b80f5-9822-41af-8668-836a70b05c0f
keywords:
- バグチェックの 0xA IRQL_NOT_LESS_OR_EQUAL
- IRQL_NOT_LESS_OR_EQUAL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- IRQL_NOT_LESS_OR_EQUAL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9e7b2f40d71117ec273d399700d55f03dd1fda4e
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534579"
---
# <a name="bug-check-0xa-irql_not_less_or_equal"></a>バグチェックの 0xA: IRQL が \_ \_ 少ない \_ か \_ 等しい


IRQL が \_ \_ 低い \_ か \_ 等しいバグチェックの値は、0x0000000a です。 これは、Microsoft Windows またはカーネルモードドライバーが、発生した割り込み要求レベル (IRQL) で、無効なアドレスのページメモリにアクセスしたことを示します。 これは通常、無効なポインターまたは pageability の問題の結果です。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="irql_not_less_or_equal-parameters"></a>IRQL \_ が \_ 少ない \_ か \_ 等しいパラメーター


<table>
<colgroup>
<col width="20%" />
<col width="80%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td align="left"><p>アクセスできなかった仮想メモリアドレス。</p>
<p>このアドレスで<strong><a href="-pool.md" data-raw-source="[!pool](-pool.md)">! pool</a></strong>を使用して、ページプールであるかどうかを確認してください。 これらのコマンドは、エラーに関する情報の収集にも役立ちます。 <strong><a href="-pte.md" data-raw-source="[!pte](-pte.md)">! pte</a></strong>、 <strong><a href="-address.md" data-raw-source="[!address](-address.md)">! address</a></strong>、および <strong> <a href="ln--list-nearest-symbols-.md" data-raw-source="[ln (List Nearest Symbols)](ln--list-nearest-symbols-.md)">ln </strong> (最も近いシンボルの一覧表示)</a>。</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td align="left"><p>障害発生時の IRQL。</p>
<p>値</p>
<ul><li><p><strong>2</strong>: IRQL は、エラー発生時に DISPATCH_LEVEL されました。</p></li></ul></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td align="left"><p>エラーの原因となった操作を説明するビットフィールド。 ビット3は、このレベルのレポートをサポートするチップセットでのみ使用できます。</p>
<p><strong>ビット0の値:</strong></p>
<ul><li><p>0: 読み取り操作</p></li>
<li><p>1-書き込み操作</p></li></ul>
<p><strong>ビット3の値:</strong></p>
<ul>
<li><p>0-実行操作ではありません</p></li>
<li><p>1-操作の実行</p></li>
</ul>
<p><strong>ビット0とビット3の結合された値:</strong></p>
<ul>
<li><p>0x0-パラメーター1のアドレスから読み取ろうとしてエラーが発生しました。</p></li>
<li><p>0x1-パラメーター1のアドレスへの書き込み中にエラーが発生しました。</p></li>
<li><p>0x8-パラメーター1のアドレスからコードを実行しようとしてエラーが発生しました。</p></li>
</ul>
<p>この値は通常、次のような場合に発生します。</p>
<ul>
<li>DISPATCH_LEVEL 時に DISPATCH_LEVEL で呼び出すことができない関数を呼び出しています。</li>
<li>スピンロックの解放を忘れています。</li>
<li>コードを非ページングにする必要がある場合に、コードをページング可能としてマークする (たとえば、コードがスピンロックを取得したり、遅延プロシージャ呼び出しで呼び出されたりするなど)。</li>
</ul>
</td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td align="left"><p>エラー発生時の命令ポインター。</p>
<p><strong>関数の名前を確認するには、このアドレスに対して<a href="ln--list-nearest-symbols-.md" data-raw-source="[ln (List Nearest Symbols)](ln--list-nearest-symbols-.md)">ln </strong> (一番近いシンボルの一覧表示)</a>コマンドを使用します。</p></td>
</tr>
</tbody>
</table>


<a name="cause"></a>原因
-----

このバグチェックは通常、不適切なアドレスを使用するカーネルモードデバイスドライバーによって発生します。

このバグチェックは、発生した割り込み要求レベル (IRQL) で、無効なアドレスにアクセスしようとしたことを示します。 これは、不適切なメモリポインターまたはデバイスドライバーコードに関する pageability の問題のいずれかです。

次に、バグチェックの原因となったコードエラーの種類を分類するために使用できる一般的なガイドラインをいくつか示します。

- パラメーター1が0x1000 未満の場合、問題は NULL ポインターの逆参照である可能性があります。

- [**! Pool**](-pool.md)によってパラメーター1がページングプール (または他の種類のページング可能なメモリ) であることが報告された場合、IRQL が大きすぎてこのデータにアクセスできません。 低い IRQL で実行するか、データを非ページプールに割り当てます。

- パラメーター3で、これがページング可能なコードを実行しようとしたことを示している場合、IRQL は高すぎるため、この関数を呼び出すことができません。 低い IRQL で実行するか、コードをページング可能としてマークしません。

- それ以外の場合、これは不適切なポインターである可能性があります。これは、使用が不要な場合や、ビットを反転する場合に発生する可能性があります。 パラメーター1で[**! pte**](-pte.md)、 [**! address**](-address.md)、および[ **ln** (最も近いシンボルを一覧表示)](ln--list-nearest-symbols-.md)の有効性を調べます。


<a name="resolution"></a>解像度
----------

カーネルデバッガーが使用可能な場合は、スタックトレースを取得します。 まず、 [**! analyze**](-analyze.md)デバッガー拡張機能を実行して、バグチェックに関する情報を表示します。 ( **! Analyze**拡張機能は、根本原因を特定するのに役立ちます)。次に、いずれかの[ **k \* ** (スタックバックトレースの表示)](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンドを入力して、呼び出し履歴を表示します。

### <a name="gather-information"></a>情報を集める

青い画面にドライバーが表示されている場合は、その名前を確認します。

エラーの原因となっているデバイスまたはドライバーの特定に役立つ可能性のある追加のエラーメッセージについては、イベントビューアーのシステムログを確認してください。 ブルースクリーンと同じ時間枠内に発生したシステムログの重大なエラーを探します。

### <a name="driver-verifier"></a>ドライバーの検証ツール

ドライバーの検証ツールは、ドライバーの動作を確認するためにリアルタイムで実行されるツールです。 たとえば、ドライバーの検証ツールは、メモリプールなどのメモリリソースの使用を確認します。 ドライバーコードの実行中に発生したエラーを特定する場合は、ドライバーコードのその部分をさらに詳しく調査できるように、例外を事前に作成します。 Driver Verifier Manager は、Windows に組み込まれており、すべての Windows Pc で使用できます。 

ドライバー検証マネージャーを起動するには、コマンドプロンプトで「 **verifier** 」と入力します。 検証するドライバーを構成できます。 ドライバーを検証するコードは、実行中のオーバーヘッドを追加するので、可能な限り最小のドライバーを確認してみてください。 詳細については、「 [Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)」を参照してください。

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

<a name="remarks"></a>注釈
-------

このバグチェックを生成するエラーは、通常、障害が発生したデバイスドライバー、システムサービス、または BIOS のインストール後に発生します。

新しいバージョンの Windows へのアップグレード中にバグチェックの0xA が発生した場合は、デバイスドライバー、システムサービス、ウイルス検索プログラム、または新しいバージョンと互換性のないバックアップツールが原因である可能性があります。

**欠陥のあるハードウェアの問題の解決:** ハードウェアが最近システムに追加されている場合は、それを削除して、エラーが引き続き発生するかどうかを確認します。 既存のハードウェアに障害が発生した場合は、問題のあるコンポーネントを削除または交換します。 システムの製造元から提供されているハードウェア診断を実行します。 これらの手順の詳細については、コンピューターの所有者のマニュアルを参照してください。

**障害が発生しているシステムサービスの問題の解決:** サービスを無効にし、それによってエラーが解決されるかどうかを確認します。 その場合は、システムサービスの製造元に連絡して、可能性のある更新プログラムを入手してください。 システムの起動中にエラーが発生した場合は、Windows の修復オプションを調べてください。 詳細については、「 [Windows 10 の回復オプション](https://support.microsoft.com/help/12415/windows-10-recovery-options)」を参照してください。

**ウイルス対策ソフトウェアの問題の解決:** プログラムを無効にして、それによってエラーが解決されるかどうかを確認します。 更新されている場合は、プログラムの製造元に問い合わせてください。

バグチェックのトラブルシューティングに関する一般的な情報については、「 [Blue screen data](blue-screen-data.md)」を参照してください。
