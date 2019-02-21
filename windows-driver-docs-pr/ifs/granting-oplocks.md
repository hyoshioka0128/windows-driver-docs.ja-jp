---
title: 各 Oplock の許可
description: 各 Oplock の許可
ms.assetid: 7faf17ef-1596-4952-9575-616f66b37ed6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee9daf785f1e5f9f3e2b309afe41027895f82afb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529053"
---
# <a name="granting-oplocks"></a>各 Oplock の許可


## <span id="ddk_network_redirector_design_and_performance_if"></span><span id="DDK_NETWORK_REDIRECTOR_DESIGN_AND_PERFORMANCE_IF"></span>


経由で要求された Oplock [FSCTL](https://go.microsoft.com/fwlink/p/?linkid=124238)秒。 次に、異なる oplock の種類 (ユーザー モード アプリケーションとカーネル モード ドライバーを発行) できる FSCTLs を示します。

-   FSCTL\_要求\_OPLOCK\_レベル\_1

-   FSCTL\_要求\_OPLOCK\_レベル\_2

-   FSCTL\_要求\_バッチ\_OPLOCK

-   FSCTL\_要求\_フィルター\_OPLOCK

-   FSCTL\_要求\_OPLOCK

一覧で最初の 4 つ FSCTLs は、従来の各 oplock の要求に使用されます。 最後 FSCTL が要求で Windows 7 の各 oplock を要求に使用される\_OPLOCK\_入力\_フラグ\_要求に指定されたフラグ、**フラグ**メンバー要求の\_OPLOCK\_入力\_として渡された、バッファーの構造体、 *lpInBuffer*パラメーターの[DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=124239)します。 同様の方法で[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)カーネル モードから Windows 7 の各 oplock を要求するために使用できます。 ファイル システム ミニフィルターを使用する必要があります[ **FltAllocateCallbackData** ](https://msdn.microsoft.com/library/windows/hardware/ff541703)と[ **FltPerformAsynchronousIo** ](https://msdn.microsoft.com/library/windows/hardware/ff543420)を Windows 7 oplock を要求します。 4 つの Windows 7 の各 oplock の中に指定するために必要な 1 つまたは複数のフラグの OPLOCK の\_レベル\_キャッシュ\_読み取り、OPLOCK\_レベル\_キャッシュ\_ハンドル、または OPLOCK\_レベル\_キャッシュ\_で書き込みが設定されて、 **RequestedOplockLevel**メンバー要求の\_OPLOCK\_入力\_バッファーの構造体。 詳細については、次を参照してください。 [ **FSCTL\_要求\_OPLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff545530)します。

ファイル システムのステータスを返します oplock と oplock を許可できるため、要求が行われると、\_PENDING (このため、oplock は与えない同期 I/O の)。 FSCTL IRP では、oplock が切断されるまでは完了しません。 Oplock が認められない場合は、適切なエラー コードが返されます。 特に一般的なエラー コードは、状態が返されます\_OPLOCK\_いない\_GRANTED と状態\_無効な\_パラメーター (および、類似するユーザー モードのと同じです)。

前述のように、フィルター oplock では「取り消し」その他のアプリケーション/クライアントが同じストリームにアクセスしようとするアプリケーション。 このメカニズムでは、ストリームを開こうとしたときに、共有違反を受信するストリームの他のアクセサーを発生させることがなく、ストリームにアクセスするアプリケーション。 共有違反を避けるためには、フィルター oplock を要求する特別な 3 つの手順の手順を使用する必要があります (FSCTL\_要求\_フィルター\_OPLOCK)。

1.  ファイルの必要なアクセス権を持つファイルを開く\_読み取り\_属性とファイルの共有モード\_共有\_読み取り |ファイル\_共有\_書き込み |ファイル\_共有\_を削除します。

2.  手順 1 からハンドル フィルター oplock を要求します。

3.  読み取りアクセス用にもう一度ファイルを開きます。

手順 1. で開いたハンドルでのみ属性へのアクセスで開かれているために、共有の違反を受信するには、他のアプリケーションは発生しません (ファイル\_読み取り\_属性)、およびデータ アクセスは含まれません (ファイル\_読み取り\_データ)。 このハンドルは、適切なデータ ストリームで実際の I/O の実行ではなくフィルター oplock を要求するためです。 手順 3 で開かれたハンドルは、ストリームにアクセスしようとしています。 別のアプリケーションに共有違反を発生させることがなく手順 2 で付与された oplock できます「の取得」を oplock の所有者、ストリームでの I/O を実行する、oplock の所有者を使用します。

NTFS ファイル システム ファイルでこの手順の最適化を提供する\_予約\_OPFILTER オプション フラグを作成します。 状態要求の作成に失敗するファイル システムがこのフラグは、前の手順の手順 1. で指定されて場合、\_OPLOCK\_いない\_付与のかどうか、ファイル システムがステップ 2 が失敗を判断することができます。 ありますに注意して手順 1. が成功すると、手順 2 の保証が成功しない場合でもファイル\_予約\_OPFILTER 作成要求が指定されました。

次の表は、oplock を許可するために必要な必要な条件を識別します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">要求の種類</th>
<th align="left">条件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>レベル 1</p>
<p>フィルター</p>
<p>Batch (バッチ)</p></td>
<td align="left"><p>すべての次の条件に該当するかどうかにのみ許可します。</p>
<ul>
<li>ファイルの指定したストリーム用の要求です。
<ul>
<li>ディレクトリを探しますが返されます。</li>
</ul></li>
<li>非同期アクセス用には、ストリームを開きます。
<ul>
<li>同期アクセスを開くと、STATUS_OPLOCK_NOT_GRANTED が返されます (oplock は同期 I/O 要求は付与されません)。</li>
</ul></li>
<li>あるない<a href="https://msdn.microsoft.com/library/windows/hardware/ff565748" data-raw-source="[TxF](https://msdn.microsoft.com/library/windows/hardware/ff565748)">TxF</a>ファイルの任意のストリームでのトランザクション。
<ul>
<li>他の STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li>その他が表示されます (同じスレッド) でも、ストリームではありません。
<ul>
<li>他の STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
</ul>
<p>対応する場合に現在の oplock の状態は。</p>
<ul>
<li><p>ない Oplock:要求が付与されます。</p></li>
<li><p>レベル 2:レベル 2 の元の要求は、FILE_OPLOCK_BROKEN_TO_NONE で分割されます。 要求された排他 oplock が付与されます。</p></li>
<li><p>レベル 1、バッチ、フィルター、読み取り、読み取りハンドル、読み取り/書き込みまたは読み取り-書き込みハンドル。STATUS_OPLOCK_NOT_GRANTED が返されます。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>レベル 2</p></td>
<td align="left"><p>すべての次の条件に該当するかどうかにのみ許可します。</p>
<ul>
<li>ファイルの指定したストリーム用の要求です。
<ul>
<li>ディレクトリを探しますが返されます。</li>
</ul></li>
<li>非同期アクセス用には、ストリームを開きます。
<ul>
<li>同期アクセスを開くと、STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li>TxF トランザクション ファイルではありません。
<ul>
<li>他の STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li>ありません現在バイト範囲ロックのストリーム。
<ul>
<li>他の STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
<li>Windows 7 では、前に、オペレーティング システムを検証するかどうか、バイト範囲ロック以前存在していた、ストリームで開かれたし、要求が失敗した場合は、前回に注意します。</li>
</ul></li>
</ul>
<p>対応する場合に現在の oplock の状態は。</p>
<ul>
<li><p>ない Oplock:要求が付与されます。</p></li>
<li>第 2 レベルや読み取り:要求が付与されます。 複数のレベル 2 がある/と同時に同じストリームで許可されている oplock を読み取ることができます。 複数のレベル 2 (ただし、未読) の各 oplock は、同じハンドルも存在できます。
<ul>
<li>読み取り oplock が既にには読み取り oplock を最初の読み取り oplock を許可するハンドルで要求された場合&#39;IRP が完了した 2 つ目の読み取り前に STATUS_OPLOCK_SWITCHED_TO_NEW_HANDLE oplock が与えられます。</li>
</ul></li>
<li><p>レベル 1、バッチをフィルター処理、読み取りハンドル、読み取り/書き込み、読み取り、書き込みハンドル。STATUS_OPLOCK_NOT_GRANTED が返されます。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p>Read</p></td>
<td align="left"><p>すべての次の条件に該当するかどうかにのみ許可します。</p>
<ul>
<li>ファイルの指定したストリーム用の要求です。
<ul>
<li>ディレクトリを探しますが返されます。</li>
</ul></li>
<li>非同期アクセス用には、ストリームを開きます。
<ul>
<li>同期アクセスを開くと、STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li>TxF トランザクション ファイルではありません。
<ul>
<li>他の STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li>ありません現在バイト範囲ロックのストリーム。
<ul>
<li>他の STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
</ul>
<p>対応する場合に現在の oplock の状態は。</p>
<ul>
<li><p>ない Oplock:要求が付与されます。</p></li>
<li>第 2 レベルや読み取り:要求が付与されます。 複数のレベル 2 がある/と同時に同じストリームで許可されている oplock を読み取ることができます。
<ul>
<li>さらに、既存の oplock がある、新しい要求と同じ oplock キー、IRP は STATUS_OPLOCK_SWITCHED_TO_NEW_HANDLE で完了します。</li>
</ul></li>
<li>読み取りハンドルと既存の oplock 新しい要求からの oplock の異なるキーがあります。要求が付与されます。 同じストリームで複数の読み取りと読み取りハンドル oplock が共存できます (この表の次の注を参照してください)。
<ul>
<li>その他 (oplock キーは同じです) STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li><p>レベル 1、バッチをフィルター処理、読み取り/書き込み、読み取り、書き込みハンドル。STATUS_OPLOCK_NOT_GRANTED が返されます。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>読み取りハンドル</p></td>
<td align="left"><p>すべての次の条件に該当するかどうかにのみ許可します。</p>
<ul>
<li>ファイルの指定したストリーム用の要求です。
<ul>
<li>ディレクトリを探しますが返されます。</li>
</ul></li>
<li>非同期アクセス用には、ストリームを開きます。
<ul>
<li>同期アクセスを開くと、STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li>TxF トランザクション ファイルではありません。
<ul>
<li>他の STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li>ありません現在バイト範囲ロックのストリーム。
<ul>
<li>他の STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
</ul>
<p>対応する場合に現在の oplock の状態は。</p>
<ul>
<li><p>Oplock: 要求が付与されません。</p></li>
<li>読む: 要求が付与されます。
<ul>
<li>読み取り oplock が同じ oplock を持つ既存の場合、新しい要求とキー、その IRP が完了しました。 STATUS_OPLOCK_SWITCHED_TO_NEW_HANDLE します。 つまり、読み取りハンドルを oplock が読み取りからアップグレードします。</li>
<li>新しい要求と同じ oplock キーがない任意の既存の読み取り oplock は変更されません。</li>
</ul></li>
<li><p>レベル 2、レベル 1、バッチをフィルター処理、読み取り/書き込み、読み取り、書き込みハンドル。STATUS_OPLOCK_NOT_GRANTED が返されます。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p>読み取り/書き込み</p></td>
<td align="left"><p>すべての次の条件に該当するかどうかにのみ許可します。</p>
<ul>
<li>ファイルの指定したストリーム用の要求です。
<ul>
<li>ディレクトリを探しますが返されます。</li>
</ul></li>
<li>非同期アクセス用には、ストリームを開きます。
<ul>
<li>同期アクセスを開くと、STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li>TxF トランザクション ファイルではありません。
<ul>
<li>他の STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li>他が表示されます (同じスレッド) でも、ストリームがある場合、同じ oplock キーが必要です。
<ul>
<li>他の STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
</ul>
<p>対応する場合に現在の oplock の状態は。</p>
<ul>
<li><p>Oplock: 要求が付与されません。</p></li>
<li>読み取りまたは読み取り/書き込み、および既存の oplock が要求と同じ oplock キー: 既存の oplock&#39;、要求が許可される s STATUS_OPLOCK_SWITCHED_TO_NEW_HANDLE IRP が完了しました。
<ul>
<li>他の STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li><p>レベル 2、レベル 1、バッチ、フィルター、ハンドルの読み取り、書き込みハンドルの読み取り。STATUS_OPLOCK_NOT_GRANTED が返されます。</p></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p>書き込みハンドルの読み取り</p></td>
<td align="left"><p>次のすべてに該当するかどうかにのみ許可。</p>
<ul>
<li>ファイルの指定したストリーム用の要求です。
<ul>
<li>ディレクトリを探しますが返されます。</li>
</ul></li>
<li>非同期アクセス用には、ストリームを開きます。
<ul>
<li>同期アクセスを開くと、STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li>TxF トランザクション ファイルではありません。
<ul>
<li>他の STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li>(同じスレッド) でも、ストリームに他のオープン要求がある場合、同じ oplock キーが必要です。
<ul>
<li>他の STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
</ul>
<p>対応する場合に現在の oplock の状態は。</p>
<ul>
<li><p>Oplock: 要求が付与されません。</p></li>
<li>ハンドルの読み取り、読み取り/書き込みまたは読み取り-書き込みハンドルを読み取るし、既存の oplock が要求と同じ oplock キー: 既存の oplock&#39;s STATUS_OPLOCK_SWITCHED_TO_NEW_HANDLE IRP が完了しました、要求が許可されます。
<ul>
<li>他の STATUS_OPLOCK_NOT_GRANTED が返されます。</li>
</ul></li>
<li><p>レベル 2、レベル 1、バッチ フィルター:STATUS_OPLOCK_NOT_GRANTED が返されます。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

**注**  読み取りと第 2 レベルの各 oplock が、同じストリームでは、上に共存させることがありますと読み取りと読み取りハンドル oplocks に共存させることがありますがレベル 2 と読み取りハンドル oplock が共存可能性があります。

 

 

 




