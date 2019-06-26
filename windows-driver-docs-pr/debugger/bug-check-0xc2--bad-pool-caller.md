---
title: バグ チェック 0xC2 BAD_POOL_CALLER
description: BAD_POOL_CALLER のバグ チェックでは、0x000000C2 の値を持ちます。 これは、現在のスレッドが不正なプールの要求を行っていることを示します。
ms.assetid: 64803335-ab93-4c4d-9b30-2ec15a13303f
keywords:
- (開発者向けコンテンツ)バグ チェック 0xC2 BAD_POOL_CALLER
- BAD_POOL_CALLER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BAD_POOL_CALLER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f50c89583a104abfcd0f2acf76f31503607a2aaa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367188"
---
# <a name="developer-content-bug-check-0xc2-badpoolcaller"></a>(開発者向けコンテンツ)バグ チェック 0xC2 の。不適切な\_プール\_呼び出し元


不適切な\_プール\_呼び出し元のバグ チェックが 0x000000C2 の値を持ちます。 これは、現在のスレッドが不正なプールの要求を行っていることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="badpoolcaller-parameters"></a>不適切な\_プール\_呼び出し元のパラメーター


**パラメーター 1**違反の種類を示します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 1</th>
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">パラメーター 4</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>プールの種類</p></td>
<td align="left"><p>プール タグ</p></td>
<td align="left"><p>現在のスレッドは、ゼロ バイトのプール割り当てを要求します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x01,</p>
<p>0x02、</p>
<p>0x04</p></td>
<td align="left"><p>プールのヘッダーへのポインター</p></td>
<td align="left"><p>プールのヘッダーの内容の最初の部分</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>プールのヘッダーが破損しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x06</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>プールのヘッダーへのポインター</p></td>
<td align="left"><p>プールのヘッダーの内容</p></td>
<td align="left"><p>現在のスレッドが既に解放されていると、プールを解放しようとしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x07</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>プールのヘッダーの内容</p></td>
<td align="left"><p>解放されてプールのブロックのアドレス</p></td>
<td align="left"><p>現在のスレッドが既に解放されていると、プールを解放しようとしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x08</p></td>
<td align="left"><p>現在の IRQL</p></td>
<td align="left"><p>プールの種類</p></td>
<td align="left"><p>(バイト単位) の割り当てのサイズ</p></td>
<td align="left"><p>現在のスレッドが、無効な IRQL でプールを割り当てるしようとしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x09</p></td>
<td align="left"><p>現在の IRQL</p></td>
<td align="left"><p>プールの種類</p></td>
<td align="left"><p>プールのアドレス</p></td>
<td align="left"><p>現在のスレッドが、無効な IRQL でプールを解放しようとしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>プールのアドレス</p></td>
<td align="left"><p>アロケーターのタグ</p></td>
<td align="left"><p>使用されているタグで、実行しようとした無料</p></td>
<td align="left"><p>現在のスレッドが、間違ったタグを使用してプールのメモリを解放しようとしました。</p>
<p>(メモリは、別のコンポーネントに属している可能性があります)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x0B、</p>
<p>0x0C、</p>
<p>または 0x0D</p></td>
<td align="left"><p>プールのアドレス</p></td>
<td align="left"><p>プールの割り当てのタグ</p></td>
<td align="left"><p>クォータの不適切なプロセスのポインター</p></td>
<td align="left"><p>現在のスレッドでは、破損したプールの割り当てに、クォータを解放しようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x40</p></td>
<td align="left"><p>開始アドレス</p></td>
<td align="left"><p>システムのアドレス空間の開始</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>現在のスレッドでは、ユーザー モード アドレスでカーネルのプールを解放しようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41</p></td>
<td align="left"><p>開始アドレス</p></td>
<td align="left"><p>物理ページ フレーム</p></td>
<td align="left"><p>物理ページの最上位フレーム</p></td>
<td align="left"><p>現在のスレッドでは、非ページ プールの非に割り当てられたアドレスを解放しようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x42</p>
<p>または 0x43</p></td>
<td align="left"><p>解放されているアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>すべてプールには存在しない仮想のアドレスを解放するため、現在のスレッドしようとしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x44</p></td>
<td align="left"><p>開始アドレス</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>現在のスレッドでは、非ページ プールの非に割り当てられたアドレスを解放しようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x46</p></td>
<td align="left"><p>開始アドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>現在のスレッド プールが無効なアドレスを解放しようとしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x47</p></td>
<td align="left"><p>開始アドレス</p></td>
<td align="left"><p>物理ページ フレーム</p></td>
<td align="left"><p>物理ページの最上位フレーム</p></td>
<td align="left"><p>現在のスレッドでは、非ページ プールの非に割り当てられたアドレスを解放しようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x48</p></td>
<td align="left"><p>開始アドレス</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>現在のスレッドに割り当てられた非ページ プールのアドレスを解放しようとしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x50 です。</p></td>
<td align="left"><p>開始アドレス</p></td>
<td align="left"><p>ページ プールの先頭からのページ内のオフセットを開始します。</p></td>
<td align="left"><p>(バイト単位) のページ プールのサイズ</p></td>
<td align="left"><p>現在のスレッドに割り当てられた非ページ プールのアドレスを解放しようとしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x60 です。</p></td>
<td align="left"><p>開始アドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>現在のスレッドが、無効な連続したメモリ アドレスを解放しようとしました。</p>
<p>(呼び出し元の<strong>MmFreeContiguousMemory</strong>無効なポインターを渡すことができます)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x99</p></td>
<td align="left"><p>対象となるアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>現在のスレッドが、無効なアドレス プールを解放しようとしました。</p>
<p>(このコードは、プールのヘッダーの破損を示すことができますも)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9A</p></td>
<td align="left"><p>プールの種類</p></td>
<td align="left"><p>要求されたバイト数</p></td>
<td align="left"><p>プール タグ</p></td>
<td align="left"><p>現在のスレッドでは、割り当て要求 must_succeed とマークされています。</p>
<p>(このプールの種類はサポート終了)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9B</p></td>
<td align="left"><p>プールの種類</p></td>
<td align="left"><p>要求されたバイト数</p></td>
<td align="left"><p>呼び出し元のアドレス</p></td>
<td align="left"><p>現在のスレッドが、0 のタグを持つプールを割り当てるしようとしています。</p>
<p>(これは、追跡できないし、タグの既存のテーブルが破損する可能性があります。)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9C</p></td>
<td align="left"><p>プールの種類</p></td>
<td align="left"><p>要求されたバイト数</p></td>
<td align="left"><p>呼び出し元のアドレス</p></td>
<td align="left"><p>現在のスレッドは、「大きい」タグを使用して、プールを割り当てようとしました。</p>
<p>(この追跡できなくなるし、既存のタグ テーブルが破損する可能性がある可能性があります。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9D</p></td>
<td align="left"><p>不適切なプール タグの使用</p></td>
<td align="left"><p>プールの種類</p></td>
<td align="left"><p>呼び出し元のアドレス</p></td>
<td align="left"><p>現在のスレッドは、任意の文字または数字が含まれていないタグを使用して、プールの割り当てにしようとしました。 などを使用してタグ付けは困難なプールの問題を追跡します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41286</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ページ プール、ページの先頭からの開始オフセット</p></td>
<td align="left"><p>現在のスレッドが、割り当ての途中でページ プールのアドレスを解放しようとしました。</p></td>
</tr>
</tbody>
</table>

 

\_プール\_Ntddk.h の種類のコードが列挙されます。 具体的には、非ページ プールは 0 し、1 ページ プールをことを示します。

<a name="cause"></a>原因
-----

現在のスレッドで、無効なプールの要求をしました。 通常これは不適切な IRQL レベルまたは double と同じメモリの割り当てなどを解放します。

<a name="resolution"></a>解決方法
----------

メモリ プールのオプションが有効な場合、これらのエラーに関する詳細情報を取得し、エラーが発生したドライバーを検索すると、ドライバーの検証ツールを有効にします。

**ドライバーの検証ツール**

Driver Verifier は、ドライバーの動作を確認するのにはリアルタイムで実行されているツールです。 ドライバー コードの実行でエラーが参照してください、さらに細かく検証するドライバー コードの部分を許可する例外が事前に作成されます。 ドライバー検証マネージャーは、Windows に組み込まれているしはすべての Windows Pc で使用できます。 ドライバー検証マネージャーを起動する入力*Verifer*コマンド プロンプトでします。 確認するにはどのドライバーを構成することができます。 ドライバーを検証するコードは実行時にオーバーヘッドを追加、のでお試しくださいし、可能なドライバーの最小数を確認します。 詳細については、次を参照してください。 [Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)します。

**Windows メモリ診断**

具体的には、メモリ プールの破損の場合は、原因として、物理メモリを特定して、Windows メモリ診断ツールを実行します。 コントロール パネルの検索ボックスには、メモリを入力し、クリックして **、コンピューターのメモリの問題を診断**します。テストの実行後は、イベント ビューアーを使用して、システム ログで結果を表示します。 探して、 *MemoryDiagnostics 結果*結果を表示するエントリ。

 

 




