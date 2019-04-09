---
title: バグ チェック 0x7A KERNEL_DATA_INPAGE_ERROR
description: KERNEL_DATA_INPAGE_ERROR のバグ チェックでは、0x0000007A の値を持ちます。 このバグ チェックでは、メモリにカーネル データ ページング ファイルからの要求されたページを読み取れなかったことを示します。
ms.assetid: 466d4864-8840-47b2-9a9a-302a125bf095
keywords:
- バグ チェック 0x7A KERNEL_DATA_INPAGE_ERROR
- KERNEL_DATA_INPAGE_ERROR
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_DATA_INPAGE_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c18f0ba0bdbb37f7649681218f521949eb371afd
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238799"
---
# <a name="bug-check-0x7a-kerneldatainpageerror"></a>バグ チェック 0x7A:カーネル\_データ\_インページ\_エラー


カーネル\_データ\_インページ\_エラーのバグ チェックが 0x0000007A の値を持ちます。 このバグ チェックでは、メモリにカーネル データ ページング ファイルからの要求されたページを読み取れなかったことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="kerneldatainpageerror-parameters"></a>カーネル\_データ\_インページ\_エラー パラメーター


メッセージに記載されている 4 つのパラメーターは、次の 3 つの可能性のある意味でことができます。 最初のパラメーターが 1 または 2、3、3 番目のパラメーターが 0、パラメーターは、次の定義にあります。

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
<td align="left"><p>(1、2、または 3) に保持されたロックの種類</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>エラー状態 (通常は、I/O 状態コード)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>ロックの種類が 1 の場合:</strong>現在のプロセス</p>
<p><strong>ロックの種類が 2 または 3 の場合。</strong>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>仮想アドレスをメモリへページングされない可能性があります。</p></td>
</tr>
</tbody>
</table>

 

かどうか、最初のパラメーターは 3 (、3 番目のパラメーターが 0 以外)、または 4 パラメーターは、次の定義を指定します。

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
<td align="left"><p>(3 または 4) に保持されたロックの種類</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>エラー状態 (通常は、I/O 状態コード)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>InPageSupport 構造体のアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>エラーが発生したアドレス</p></td>
</tr>
</tbody>
</table>

 

それ以外の場合、パラメーターには、次の定義があります。

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
<td align="left"><p>ページ テーブル エントリ (PTE) のアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>エラー状態 (通常は、I/O 状態コード)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>PTE 内容</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>エラーが発生したアドレス</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

カーネルの原因を特定する多くの場合、\_データ\_インページ\_エラー状態 (パラメーター 2) からのエラーのバグ チェックします。 一般的なステータス コードを以下に示します。

-   0xC000009A、または状態\_不十分\_リソースの非ページ プールのリソースが不足していることを示します。

-   0xC000009C、または状態\_デバイス\_データ\_エラー、通常、ハード_ディスク上の不良ブロック (セクター) を示します。

-   0xC000009D、または状態\_デバイス\_いない\_接続 は、障害があるか疎ケーブル、ターミネータ、またはハード ディスクをコント ローラーが表示されなくなることを示します。

-   0xc000016a の場合、または状態\_ディスク\_操作\_FAILED、ハード_ディスク上の不良ブロック (セクター) を示します。

-   0xC0000185、または状態\_IO\_デバイス\_エラー、不適切な終了を示す、または同じ IRQ を使用しようとしている障害のある SCSI デバイスまたはその 2 つのデバイスのケーブル接続します。

-   0xC000000E、または状態\_いいえ\_かかる\_デバイスは、ハードウェア障害、または正しくないドライブ構成を示します。 ケーブルを確認し、ドライブの製造元から使用可能な診断ユーティリティを使用したドライブをチェックします。 古い PATA (IDE) のドライブを使用している場合、この状態コードは、マスター/下位ドライブが正しくない構成を指定できます。

これらのステータス コードは、具体的な原因である最も一般的なものです。 返されるその他の可能な状態コードの詳細については、Microsoft Windows Driver Kit (WDK) で Ntstatus.h ファイルを参照してください。

このエラー メッセージの別の一般的な原因は、欠陥のあるハードウェアや RAM の失敗です。

このバグ チェックもウイルスの感染があります。

<a name="resolution"></a>解決方法
----------

**不適切なブロックの問題を解決するには。** 0xC000009C または 0xc000016a の場合、I/O ステータス コードでは、通常、データがでした不良ブロック (機関) のため、ディスクからいない読み取りすることを示します。 コンピューターを再起動するには、エラーの発生後、Autochk は自動的に実行され、今後使用されるを防ぐために不良セクターをマップしようとします。

Autochk がハード ディスクのエラーをスキャンしない場合は、ディスクのスキャナーを手動で開始できます。 実行**Chkdsk/f/r**システム パーティションにします。 ディスクのスキャンを開始する前に、コンピューターを再起動する必要があります。 回復コンソールを使用して、実行場合は、エラーのため、コンピューターを起動することはできません、 **Chkdsk/r**します。

**警告**  システム パーティションが FAT ファイル システムでフォーマットされている場合、長いファイル名を Windows の整合性を確認するスキャンまたは別のハード_ディスクを ms-dos ツールを使用する場合は、オペレーティング システムの使用を破損している可能性がありますMS-DOS からハード_ディスク。 常に Windows のバージョンに Chkdsk のバージョンを使用します。

 

**欠陥のあるハードウェアの問題を解決するには。** I/O の状態が C0000185 で、ページング ファイルが、SCSI ディスクにある場合は、場合は、ディスクのケーブル配線および問題の SCSI の終了を確認します。

**問題の RAM、失敗した場合の解決。** メモリ スキャナーでは特に、システムの製造元が提供、ハードウェア診断を実行します。 これらの手順の詳細については、コンピューターの製造元のマニュアルを参照してください。

コンピューターのすべてのアダプター カードが正しく取り付けられていることを確認します。 インクの削除や、電気連絡先処理、サプライの電器店でご利用いただけますを使用して、アダプター カードの連絡先がクリーンであることを確認します。

エラーの原因となっているデバイスを識別するのに役立つ追加のエラー メッセージをイベント ビューアーのシステム ログを確認します。 このエラーを解決しようとする BIOS のメモリ キャッシュ無効にすることもできます。

最新の Windows Service Pack がインストールされていることを確認します。

上記の手順でエラーが解決しない場合、診断をテストするための修復機能をシステムのマザーボードを実行します。 亀裂、傷のトレース、またはマザーボード上の欠陥があるコンポーネントは、このエラーを発生できます。

**ウイルスの感染を解決するには。** ハード_ディスクのマスター ブート レコードを調査するソフトウェアをスキャン、商用の最新のウイルスを使用してコンピューターのウイルスを確認します。 すべての Windows ファイル システムは、ウイルスに感染することができます。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**バグ チェック 0x77 (カーネル\_スタック\_インページ\_エラー)**](bug-check-0x77--kernel-stack-inpage-error.md)

 

 




