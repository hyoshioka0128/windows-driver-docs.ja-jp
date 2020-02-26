---
title: バグチェック 0xC2 BAD_POOL_CALLER
description: BAD_POOL_CALLER バグチェックの値は0x000000C2 です。 これは、現在のスレッドが無効なプール要求を行っていることを示します。
ms.assetid: 64803335-ab93-4c4d-9b30-2ec15a13303f
keywords:
- バグチェック 0xC2 BAD_POOL_CALLER
- BAD_POOL_CALLER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BAD_POOL_CALLER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2a73283dc4f97acf51c13be7a7bc10e609f31a08
ms.sourcegitcommit: a54b96c52b0c7009dfa05bcc68d210b13711f2ea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/25/2020
ms.locfileid: "77601718"
---
# <a name="bug-check-0xc2-bad_pool_caller"></a>バグチェック 0xC2: 無効な\_プール\_呼び出し元

無効な\_プール\_呼び出し元のバグチェックには、値0x000000C2 が指定されています。 これは、現在のスレッドが無効なプール要求を行っていることを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

## <a name="bad_pool_caller-parameters"></a>\_プール\_呼び出し元のパラメーターが正しくありません

**パラメーター 1**は違反の種類を示します。

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
<th align="left">パラメーター1</th>
<th align="left">パラメータ 2</th>
<th align="left">パラメーター3</th>
<th align="left">パラメーター4</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>プールの種類</p></td>
<td align="left"><p>プールタグ</p></td>
<td align="left"><p>現在のスレッドは、ゼロバイトプール割り当てを要求しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x01</p>
<p>除く</p>
<p>0x04</p></td>
<td align="left"><p>プールヘッダーへのポインター</p></td>
<td align="left"><p>プールヘッダーの内容の最初の部分</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>プールヘッダーが破損しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x06</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>プールヘッダーへのポインター</p></td>
<td align="left"><p>プールヘッダーの内容</p></td>
<td align="left"><p>現在のスレッドは、既に解放されているプールを解放しようとしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x07</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>プールヘッダーの内容</p></td>
<td align="left"><p>解放されているプールのブロックのアドレス</p></td>
<td align="left"><p>現在のスレッドは、既に解放されているプールを解放しようとしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x08</p></td>
<td align="left"><p>現在の IRQL</p></td>
<td align="left"><p>プールの種類</p></td>
<td align="left"><p>割り当てのサイズ (バイト単位)</p></td>
<td align="left"><p>現在のスレッドは、無効な IRQL でプールを割り当てようとしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x09</p></td>
<td align="left"><p>現在の IRQL</p></td>
<td align="left"><p>プールの種類</p></td>
<td align="left"><p>プールのアドレス</p></td>
<td align="left"><p>現在のスレッドは、無効な IRQL でプールを解放しようとしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x0A</p></td>
<td align="left"><p>プールのアドレス</p></td>
<td align="left"><p>アロケーターのタグ</p></td>
<td align="left"><p>無料試用版で使用されているタグ</p></td>
<td align="left"><p>現在のスレッドは、間違ったタグを使用してプールメモリを解放しようとしました。</p>
<p>(メモリは別のコンポーネントに属している可能性があります)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0X0B</p>
<p>0x0C,</p>
<p>または0x0D</p></td>
<td align="left"><p>プールのアドレス</p></td>
<td align="left"><p>プール割り当てのタグ</p></td>
<td align="left"><p>無効なクォータ処理ポインター</p></td>
<td align="left"><p>現在のスレッドは、破損したプール割り当てのクォータを解放しようとしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x40</p></td>
<td align="left"><p>開始アドレス</p></td>
<td align="left"><p>システムアドレス空間の開始</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>現在のスレッドは、ユーザーモードアドレスでカーネルプールを解放しようとしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x41</p></td>
<td align="left"><p>開始アドレス</p></td>
<td align="left"><p>物理ページフレーム</p></td>
<td align="left"><p>物理ページの最上位フレーム</p></td>
<td align="left"><p>現在のスレッドは、割り当てられていない非ページプールアドレスを解放しようとしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x42</p>
<p>または0x43</p></td>
<td align="left"><p>解放されるアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>現在のスレッドは、どのプールにも存在しない仮想アドレスを解放しようとしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x44</p></td>
<td align="left"><p>開始アドレス</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>現在のスレッドは、割り当てられていない非ページプールアドレスを解放しようとしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x46</p></td>
<td align="left"><p>開始アドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>現在のスレッドが、無効なプールアドレスを解放しようとしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x47</p></td>
<td align="left"><p>開始アドレス</p></td>
<td align="left"><p>物理ページフレーム</p></td>
<td align="left"><p>物理ページの最上位フレーム</p></td>
<td align="left"><p>現在のスレッドは、割り当てられていない非ページプールアドレスを解放しようとしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x48</p></td>
<td align="left"><p>開始アドレス</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>現在のスレッドは、割り当てられていないページングプールアドレスを解放しようとしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x50</p></td>
<td align="left"><p>開始アドレス</p></td>
<td align="left"><p>ページプールの先頭からの開始オフセット (ページ単位)</p></td>
<td align="left"><p>ページプールのサイズ (バイト単位)</p></td>
<td align="left"><p>現在のスレッドは、割り当てられていないページングプールアドレスを解放しようとしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x60</p></td>
<td align="left"><p>開始アドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>現在のスレッドで、無効な連続したメモリアドレスが解放されようとしました。</p>
<p>( <strong>MmFreeContiguousMemory</strong>の呼び出し元は、正しくないポインターを渡しています)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x99 (</p></td>
<td align="left"><p>解放されているアドレス</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>現在のスレッドは、無効なアドレスでプールを解放しようとしました。</p>
<p>(このコードでは、プールヘッダーの破損を示すこともできます)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9A</p></td>
<td align="left"><p>プールの種類</p></td>
<td align="left"><p>要求されたバイト数</p></td>
<td align="left"><p>プールタグ</p></td>
<td align="left"><p>割り当て要求としてマークされている現在のスレッド MUST_SUCCEED。</p>
<p>(このプールの種類はサポートされなくなりました。)</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9B</p></td>
<td align="left"><p>プールの種類</p></td>
<td align="left"><p>要求されたバイト数</p></td>
<td align="left"><p>呼び出し元のアドレス</p></td>
<td align="left"><p>現在のスレッドは、0のタグでプールを割り当てようとしました</p>
<p>(これは追跡不可能であり、既存のタグテーブルが破損する可能性があります)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9C</p></td>
<td align="left"><p>プールの種類</p></td>
<td align="left"><p>要求されたバイト数</p></td>
<td align="left"><p>呼び出し元のアドレス</p></td>
<td align="left"><p>現在のスレッドは、"BIG" というタグを持つプールを割り当てようとしました。</p>
<p>(これは追跡不可能であり、既存のタグテーブルが破損する可能性があります)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9D</p></td>
<td align="left"><p>無効なプールタグが使用されています</p></td>
<td align="left"><p>プールの種類</p></td>
<td align="left"><p>呼び出し元のアドレス</p></td>
<td align="left"><p>現在のスレッドは、文字または数字が含まれていないタグを使用してプールを割り当てようとしました。 このようなタグを使用すると、追跡プールの問題が困難になります。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x41286</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ページプールの先頭からの開始オフセット (ページ単位)</p></td>
<td align="left"><p>現在のスレッドは、割り当ての途中でページプールアドレスを解放しようとしました。</p></td>
</tr>
</tbody>
</table>

\_プール\_型コードは Ntddk で列挙されます。 特に、0は非ページプールを示し、1はページプールを示します。

## <a name="cause"></a>原因

現在のスレッドによって無効なプール要求が行われました。 通常、これは無効な IRQL レベルであるか、同じメモリ割り当てを2つ解放しています。

## <a name="resolution"></a>解決方法

メモリプールオプションが有効になっているドライバーの検証ツールをアクティブ化して、これらのエラーに関する詳細情報を取得し、障害が発生しているドライバーを特定します。

**ドライバーの検証ツール**

ドライバーの検証ツールは、ドライバーの動作を確認するためにリアルタイムで実行されるツールです。 ドライバーコードの実行中にエラーが発生した場合は、ドライバーコードのその部分をさらに詳しく調べることを許可する例外が事前に作成されています。 Driver verifier マネージャーは Windows に組み込まれており、すべての Windows Pc で使用できます。 ドライバー検証マネージャーを起動するには、コマンドプロンプトで「 *Verifer* 」と入力します。 確認するドライバーを構成できます。 ドライバーを検証するコードは、実行中のオーバーヘッドを追加するので、可能な限り最小のドライバー数を試してみてください。 詳細については、「 [Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)」を参照してください。

**Windows メモリ診断**

特に、メモリプールが破損している状況では、Windows メモリ診断ツールを実行して、物理メモリを原因として特定します。 コントロールパネルの検索ボックスに「Memory」と入力し、 **[コンピューターのメモリの問題を診断する]** をクリックします。テストの実行後、イベントビューアーを使用して、システムログの下に結果を表示します。 結果を表示するには、 *Memorydiagnostics-results*エントリを探します。
