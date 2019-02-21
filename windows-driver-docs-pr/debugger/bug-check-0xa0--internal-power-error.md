---
title: バグ チェック 0xA0 INTERNAL_POWER_ERROR
description: INTERNAL_POWER_ERROR のバグ チェックでは、0x000000A0 の値を持ちます。 このバグ チェックでは、電源ポリシー マネージャーに致命的なエラーが発生したことを示します。
ms.assetid: a763e865-8591-4ed3-b3cd-1cdaecad6e97
keywords:
- バグ チェック 0xA0 INTERNAL_POWER_ERROR
- INTERNAL_POWER_ERROR
ms.date: 12/27/2018
topic_type:
- apiref
api_name:
- INTERNAL_POWER_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b9fa7b8c565af865c0d51b1252d4c99dbafe57d5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556677"
---
# <a name="bug-check-0xa0-internalpowererror"></a>バグ チェック 0xA0 の。内部\_POWER\_エラー


内部\_POWER\_エラーのバグ チェックが 0x000000A0 の値を持ちます。 このバグ チェックでは、電源ポリシー マネージャーに致命的なエラーが発生したことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="internalpowererror-parameters"></a>内部\_POWER\_エラー パラメーター


パラメーター 1 では、違反の種類を示します。 その他のパラメーターの意味は、パラメーター 1 の値によって異なります。

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
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p><strong>1:</strong>デバイスは、参照カウントが最大数をオーバーランが。</p>
<p><strong>2、3、または 4:</strong>多すぎる突入 power Irp がキューに登録されました。</p>
<p><strong>5:</strong>電源 IRP がパッシブ レベルのデバイス オブジェクトに送信されました。</p>
<p><strong>6:</strong>システムは、必要なパワー IRP の割り当てに失敗しました。</p></td>
<td align="left"><p>パラメーター 2 では、1、許可されている参照の最大数の値を持ちます。 場合、</p>
<p>かどうか、パラメーター 2 は、2、3、または 4 の値を持つ、Irp の保留中の最大数を許可します。</p>
<p>パラメーター 2 では、6、ターゲット デバイス オブジェクトの値を持ちます。 場合、</p></td>
<td align="left">パラメーター 2 が 6 の値を持つ場合は、これはシステム (0x0) または (0x1) デバイスの電源 IRP かどうかを示します。</td>
<td align="left"><p>電源の I/O 要求パケット (IRP) の処理中にエラーが発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>電源イベントを処理中に内部エラーが発生しました。 詳細については、次を参照してください。<a href="#parameter-1-equals-0x2" data-raw-source="[Debugging bug check 0xA0 when parameter 1 equals 0x2](#parameter-1-equals-0x2)">デバッグ 0xA0 パラメーター 1 が 0x2 の場合のバグ チェック</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x3</p></td>
<td align="left"><p>予想されるチェックサム</p></td>
<td align="left"><p>実際のチェックサム</p></td>
<td align="left"><p>エラーの行番号</p></td>
<td align="left"><p>休止状態のコンテキスト ページのチェックサムの予想されるチェックサムが一致しません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x4</p></td>
<td align="left"><p>予想されるチェックサム</p></td>
<td align="left"><p>実際のチェックサム</p></td>
<td align="left"><p>エラーの行番号</p></td>
<td align="left"><p>休止状態ファイルに書き込まれるページのチェックサムの予想されるチェックサムが一致しません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>システムのシャット ダウン ハンドラーに、不明なシャット ダウン コードが送信されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x7</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ハンドルされない例外が発生しました。 詳細については、次を参照してください。<a href="#parameter-1-equals-0x7" data-raw-source="[Debugging bug check 0xA0 when parameter 1 equals 0x7](#parameter-1-equals-0x7)">デバッグ バグ チェックとパラメーター 1 に等しい 0x7 0xA0</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8</p></td>
<td align="left"><p>このパラメーターは、0x100 を常に設定されます。</p></td>
<td align="left"><p>デバイス オブジェクト</p></td>
<td align="left"><p>POWER_CHANNEL_SUMMARY</p>
<p></p></td>
<td align="left"><p>システム電源イベントの処理中に致命的なエラーが発生しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x9</p></td>
<td align="left"><p>状態コード</p></td>
<td align="left"><p>ミラーリングのフェーズ</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>休止状態ファイルを準備中に致命的なエラーが発生しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0 xa</p></td>
<td align="left"><p><strong>0:</strong>バグ チェックが再開するとすぐに要求されました。</p>
<p><strong>1:</strong>バグ チェックは、デバイスの電源投入されたがページング可能なすべての再開時に要求されました。</p>
<p><strong>2:</strong>バグ チェックがすべてのデバイスの電源投入がされた後再開時に要求されました。</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>デバッグのためにスリープ解除するときのバグ チェックが要求されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0 xb</p></td>
<td align="left"><p>休止状態ファイルのサイズ。</p></td>
<td align="left"><p>領域が不足する前に休止状態の進行状況</p>
<p><strong>0:</strong>HIBERFILE_PROGRESS_FREE_MAP</p>
<p><strong>1:</strong>HIBERFILE_PROGRESS_RESUME_CONTEXT</p>
<p><strong>2:</strong>HIBERFILE_PROGRESS_PROCESSOR_STATEE</p>
<p><strong>3:</strong>HIBERFILE_PROGRESS_MEMORY_RANGES</p>
<p><strong>4:</strong>HIBERFILE_PROGRESS_TABLE_PAGES</p>
<p><strong>5:</strong>HIBERFILE_PROGRESS_MEMORY_IMAGE</p></td>
<td align="left"><p>残りのメモリの範囲のサイズ。</p></td>
<td align="left"><p>休止状態ファイルが小さすぎます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0 xc</p></td>
<td align="left"><p>状態コード</p></td>
<td align="left"><p>ダンプのスタック コンテキスト</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ダンプ スタックは、初期化に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x101</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>例外のポインター。</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>システム電源イベントの処理中にハンドルされない例外が発生しました。 詳細については、次を参照してください。<a href="#parameter-1-equals-0x101" data-raw-source="[Debugging bug check 0xA0 when parameter 1 equals 0x101](#parameter-1-equals-0x101)">デバッグ バグ チェックとパラメーター 1 に等しい 0x101 0xA0</a>します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x102</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>DUMP_INITIALIZATION_CONTEXT</p></td>
<td align="left"><p>POP_HIBER_CONTEXT</p></td>
<td align="left"><p>バッファー サイズの操作の休止状態は、ページに合わせるではありません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x103</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>POP_HIBER_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>休止状態の処理中に考慮する作業のすべてのページが失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x104</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>POP_HIBER_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>内部のメモリ構造がロックされている間に休止状態の内部のメモリをマップしようとしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x105</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>POP_HIBER_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>フラグは、サポートされていないメモリ型フラグを使用して内部の休止状態のメモリをマップしようとしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x106</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>メモリの記述子のリスト (MDL)</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>メモリの記述子のリストは、ページに配置できないメモリについて説明しますが休止状態の処理中に作成されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x107</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>POP_HIBER_CONTEXT</p></td>
<td align="left"><p>PO_MEMORY_RANGE_ARRAY</p></td>
<td align="left"><p>休止状態の内部データ構造のデータの不一致が発生しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x108</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>POP_HIBER_CONTEXT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ディスク サブシステムは、休止状態ファイルの一部を正しく書き込めませんでした。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x109</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予期されるチェックサム</p></td>
<td align="left"><p>実際のチェックサム</p></td>
<td align="left"><p>プロセッサの状態データのチェックサムの予想されるチェックサムが一致しません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10A</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>POP_HIBER_CONTEXT</p></td>
<td align="left"><p>NTSTATUS</p></td>
<td align="left"><p>ディスク サブシステムは、正しくの読み取りまたは休止状態ファイルの一部の書き込みに失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x10B</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>現在休止状態の進行状況</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>PoSetHiberRange API を使用して不適切なタイミングで休止状態のブート フェーズのページをマークしようとしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10C</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>API に指定されたフラグ</p></td>
<td align="left"><p>長さをマーク</p></td>
<td align="left"><p>PoSetHiberRange API は、無効なパラメーターで呼び出されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x200</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>DEVICE_OBJECT</p></td>
<td align="left"><p>DEVICE_OBJECT_POWER_EXTENSION</p></td>
<td align="left"><p>アイドル状態になったため、不明なデバイスの種類をチェックしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x300</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>DEVICE_OBJECT</p></td>
<td align="left"><p>IRP</p></td>
<td align="left"><p>バッテリ電源 IRP から不明なステータスが返されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x301</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>DEVICE_OBJECT</p></td>
<td align="left"><p>IRP</p></td>
<td align="left"><p>バッテリが不明な状態を入力します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x400</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>IO_STACK_LOCATION</p></td>
<td align="left"><p>DEVICE_OBJECT</p></td>
<td align="left"><p>デバイスは、参照カウントが最大数をオーバーランが。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x401</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>保留中の IRP 一覧</p></td>
<td align="left"><p>DEVICE_OBJECT</p></td>
<td align="left"><p>多すぎる突入 power Irp がキューに登録されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x402</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>保留中の IRP 一覧</p></td>
<td align="left"><p>DEVICE_OBJECT</p></td>
<td align="left"><p>多すぎる突入 power Irp がキューに登録されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x403</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>保留中の IRP 一覧</p></td>
<td align="left"><p>DEVICE_OBJECT</p></td>
<td align="left"><p>多すぎる突入 power Irp がキューに登録されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x404</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>IO_STACK_LOCATION</p></td>
<td align="left"><p>DEVICE_OBJECT</p></td>
<td align="left"><p>電源 IRP がパッシブ レベルのデバイス オブジェクトに送信されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x500</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>IRP</p></td>
<td align="left"><p>DEVICE_OBJECT</p></td>
<td align="left"><p>熱 power IRP から不明なステータスが返されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x600</p></td>
<td align="left"><p>DEVICE_OBJECT PDO</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ドライバーは、電源のランタイム フレームワークの重複する登録しようとしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x601</p></td>
<td align="left"><p>POP_FX_DEVICE デバイス</p></td>
<td align="left"><p>PEP_DEVICE_REGISTER PEP</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>電源エンジン プラグインには、デバイスの登録は受け入れられません。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x602</p></td>
<td align="left"><p>DEVICE_NODE デバイス ノード</p></td>
<td align="left"><p>スリープの数</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>デバイス ノードのスリープ状態の数が、ライセンス認証カウントと一致しません。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x603</p></td>
<td align="left"><p>POP_FX_PLUGIN</p></td>
<td align="left"><p>要求の種類の作業</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>電源のエンジン プラグインでは、無効な作業要求が行われます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x605</p></td>
<td align="left"><p>通知 ID</p></td>
<td align="left"><p>POP_FX_PLUGIN</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>必須のデバイスの電源管理の通知を受け入れるように Power エンジン プラグインが失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x606</p></td>
<td align="left"><p>POP_FX_COMPONENT</p></td>
<td align="left"><p>POP_FX_COMPONENT_FLAGS</p></td>
<td align="left"><p>コンポーネントの新しい条件</p></td>
<td align="left"><p>電源のエンジン プラグインでは、アクティブ (またはアイドル状態)、リソースが既にアクティブ (またはアイドル) 状態に重要なシステム リソースのコンポーネントを移行しようとしています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x607</p></td>
<td align="left"><p>POP_FX_DEVICE</p></td>
<td align="left"><p>NTSTATUS</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>成功することが必要なとき、ランタイムの電源管理フレームワークのデバイスの削除ロックの取得に失敗しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x608</p></td>
<td align="left"><p>POP_FX_COMPONENT</p></td>
<td align="left"><p>POP_FX_COMPONENT_FLAGS</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>ドライバーは、コンポーネントを前のアクティブな要求なしのアイドル状態に移行するしようとしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x609</p></td>
<td align="left"><p>POP_FX_PLUGIN</p></td>
<td align="left"><p>POP_FX_DEVICE</p></td>
<td align="left"><p>要求の種類が重複しています</p>
<p><strong>0:</strong>DevicePowerRequired</p>
<p><strong>1:</strong>DevicePowerNotRequired</p></td>
<td align="left"><p>電源のエンジン プラグインには、いずれかデバイス電源必須またはデバイスの電源が反対側の型の間に要求されない必要ありませんが要求されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x610</p></td>
<td align="left"><p>POP_FX_PLUGIN</p></td>
<td align="left"><p>POP_FX_DEVICE</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>電源のエンジン プラグインには、デバイスの電源を前のデバイスの電源に必要な要求は保留状態中には必要ありませんが要求されました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x611</p></td>
<td align="left"><p>POP_FX_PLUGIN</p></td>
<td align="left"><p>POP_FX_DEVICE</p></td>
<td align="left"><p>インデックスのコンポーネントは無効です。</p></td>
<td align="left"><p>電源のエンジン プラグインには、無効なコンポーネントとの操作を要求しました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x612</p></td>
<td align="left"><p>POP_FX_PLUGIN PowerEnginePlugin</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>電源エンジン プラグインには、バッファーが指定されていません PO で要求のデバイスの通知のコンテキストで実行する追加の作業が必要です。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x613</p></td>
<td align="left"><p>POP_FX_DEVICE</p></td>
<td align="left"><p>コンポーネントのインデックス</p></td>
<td align="left"><p>操作</p>
<p><strong>0:</strong>完全なデバイスの電源は必要ありません。</p>
<p><strong>1:</strong>レポートのデバイスの電源オン</p>
<p><strong>2:</strong>完全なアイドル条件</p></td>
<td align="left"><p>ドライバーは、このような未処理の要求が保留中でない場合は、要求を完了しようとしています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x614</p></td>
<td align="left"><p>POP_FX_DEVICE</p></td>
<td align="left"><p>コンポーネントのインデックス</p></td>
<td align="left"><p>無効なパラメーター</p>
<p><strong>0:</strong>IRQL で使用される PO_FX_FLAG_BLOCKING &gt;= DISPATCH_LEVEL</p>
<p><strong>1:</strong>PO_FX_FLAG_BLOCKING と PO_FX_FLAG_ASYNC_ONLY 両方を指定します。</p>
<p><strong>2:</strong>インデックスのコンポーネントは無効です。</p></td>
<td align="left"><p>ドライバーは無効なパラメーターを持つコンポーネントのアクティブまたはアイドル状態の遷移を要求しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x615</p></td>
<td align="left"><p>POP_FX_PLUGIN</p></td>
<td align="left"><p>POP_FX_COMPONENT</p></td>
<td align="left"><p>無効なアクション</p>
<p><strong>0:</strong>アイドル状態 0 でないコンポーネント</p>
<p><strong>1:</strong>コンポーネントが既にアクティブ</p>
<p><strong>2:</strong>未処理のライセンス認証要求なし</p>
<p><strong>3:</strong>未処理のアイドル状態の移行</p></td>
<td align="left"><p>Power エンジン プラグインは、コンポーネントのアクティブ化の完了を不正に示しています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x616</p></td>
<td align="left"><p>POP_FX_PLUGIN</p></td>
<td align="left"><p>POP_FX_COMPONENT</p></td>
<td align="left"><p>無効なアクション</p>
<p><strong>0:</strong>アイドル状態が無効です。</p>
<p><strong>1:</strong>コンポーネントが既に要求された状態</p>
<p><strong>2:</strong>アイドル状態 0 を通過せず、0 以外のアイドル状態を要求</p></td>
<td align="left"><p>電源のエンジン プラグインが不正にコンポーネント アイドル状態の遷移を要求しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x666</p></td>
<td align="left"><p>PPOP_PEP_ACTIVITY</p></td>
<td align="left"><p>新しいアクティビティの種類</p>
<p><strong>0:</strong>DevicePowerOn</p>
<p><strong>1:</strong>ComponentIdleStateChange</p>
<p><strong>2:</strong>ComponentActivating</p>
<p><strong>3:</strong>ComponentActive</p>
<p><strong>4:</strong>DevicePowerOff</p>
<p><strong>5:</strong>DeviceSuspend</p></td>
<td align="left"><p>競合するアクティビティの種類</p>
<p><strong>0:</strong>DevicePowerOn</p>
<p><strong>1:</strong>ComponentIdleStateChange</p>
<p><strong>2:</strong>ComponentActivating</p>
<p><strong>3:</strong>ComponentActive</p>
<p><strong>4:</strong>DevicePowerOff</p>
<p><strong>5:</strong>DeviceSuspend</p></td>
<td align="left"><p>既定の電源エンジン プラグインは、他のアクティビティと競合する新しいアクティビティをトリガーするしようとしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x667</p></td>
<td align="left"><p>POP_PEP_ACTIVITY</p></td>
<td align="left"><p>アクティビティの種類</p>
<p><strong>0:</strong>DevicePowerOn</p>
<p><strong>1:</strong>ComponentIdleStateChange</p>
<p><strong>2:</strong>ComponentActivating</p>
<p><strong>3:</strong>ComponentActive</p>
<p><strong>4:</strong>DevicePowerOff</p>
<p><strong>5:</strong>DeviceSuspend</p></td>
<td align="left"><p>POP_PEP_ACTIVITY_STATUS</p></td>
<td align="left"><p>既定の電源エンジン プラグインが実行されていないアクティビティを実行しようとしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x700</p></td>
<td align="left"><p>PEPHANDLE</p></td>
<td align="left"><p>PEP_PPM_IDLE_SELECT</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>電源のエンジン プラグインが無効なプロセッサのアイドル状態の依存関係を指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x701</p></td>
<td align="left"><p>ハングしたプロセッサの選択のアイドル状態のインデックス</p></td>
<td align="left"><p>ハングしたプロセッサの PRCB アドレス</p></td>
<td align="left"><p>ハングしたプロセッサのインデックス</p></td>
<td align="left"><p>プロセッサは、割り当てられた時間内でアイドル状態の遷移を完了できませんでした。 これは、指定したプロセッサが停止していることを示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x702</p></td>
<td align="left"><p>プロセッサの選択されているアイドル状態のインデックス</p></td>
<td align="left"><p>プロセッサのアイドル状態の同期の状態</p></td>
<td align="left"><p>ハングしたプロセッサの PRCB アドレス</p></td>
<td align="left"><p>プロセッサは、OS (必要なの PPM アイドル状態の同期を使用)、PEP で明示的なスリープの状態の解除を開始することがなく、中断不可能な状態から復帰。</p></td>
</tr>
</tbody>
</table>





<a name="resolution"></a>解決方法
----------

**一般的な注意事項**

上の表では、構造体へのポインター パラメーターのいくつかは。 たとえば、パラメーター 2 はデバイスとして表示\_オブジェクトをパラメーター 2 は、デバイスへのポインター\_オブジェクトの構造体。 構造体の一部は、Windows Driver Kit に含まれている、wdm.h で定義されます。 たとえば、次の構造は、wdm.h で定義されます。

-   例外\_ポインター
-   デバイス\_オブジェクト
-   IO\_スタック\_場所
-   PEP\_デバイス\_登録

前の表に表示される構造体の一部は、任意のパブリック ヘッダー ファイルで定義されていません。 使用してこれらの構造体の定義を確認できます、 [ **dt** ](dt--display-type-.md)デバッガー コマンド。 次の例は、使用する方法を示します、 **dt**コマンドを参照してください、**デバイス\_オブジェクト\_POWER\_拡張子**構造体。

```dbgcmd
3: kd> dt nt!DEVICE_OBJECT_POWER_EXTENSION
   +0x000 IdleCount        : Uint4B
   +0x004 BusyCount        : Uint4B
   +0x008 BusyReference    : Uint4B
   +0x00c TotalBusyCount   : Uint4B
   +0x010 ConservationIdleTime : Uint4B
   +0x014 PerformanceIdleTime : Uint4B
   +0x018 DeviceObject     : Ptr64 _DEVICE_OBJECT
   +0x020 IdleList         : _LIST_ENTRY
   +0x030 IdleType         : _POP_DEVICE_IDLE_TYPE
   +0x034 IdleState        : _DEVICE_POWER_STATE
   +0x038 CurrentState     : _DEVICE_POWER_STATE
   +0x040 Volume           : _LIST_ENTRY
   +0x050 Specific         : <unnamed-tag>
```

このバグ チェックの特定のインスタンスをデバッグするには、次の手順が役立ちます。

<span id="parameter-1-equals-0x2"></span><span id="PARAMETER-1-EQUALS-0X2"></span>
**バグ チェック 0xA0 パラメーター 1 が 0x2 の場合のデバッグ**

1.  スタックを調べます。 探して、 **ntoskrnl!PopExceptionFilter**関数。 この関数には、最初の引数として、次のコードが含まれています。

    ```cpp
     (error_code << 16) | _LINE_
    ```

    呼び出し元が場合**PopExceptionFilter**、この関数に最初の引数が型 PEXCEPTION の\_ポインター。 この引数の値に注意してください。

2.  使用して、 [ **dt (表示の種類)** ](dt--display-type-.md)コマンドし、として前の手順で検出された値を指定*引数*します。

    ```dbgcmd
    dt nt!_EXCEPTION_POINTERS argument 
    ```

    このコマンドは、構造を表示します。 コンテキスト レコードのアドレスに注意してください。

3.  使用して、 [ **.cxr (コンテキスト レコードの表示)** ](-cxr--display-context-record-.md)コマンドし、として前の手順で検出されたコンテキスト レコードを指定して*レコード*します。

    ```dbgcmd
    .cxr record 
    ```

    このコマンドは、レジスタのコンテキストを適切な値に設定します。

4.  さまざまなコマンドを使用すると、エラーの原因を分析できます。 始まり[ **kb (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)します。

<span id="parameter-1-equals-0x7"></span><span id="PARAMETER-1-EQUALS-0X7"></span>
**バグ チェック 0xA0 0x7 がパラメーター 1 の場合のデバッグ**

1.  スタックを調べます。 探して、 **ntoskrnl!PopExceptionFilter**関数。 この関数の最初の引数は型 PEXCEPTION\_ポインター。 この引数の値に注意してください。

2.  使用して、 [ **dt (表示の種類)** ](dt--display-type-.md)コマンドし、として前の手順で検出された値を指定*引数*します。

    ```dbgcmd
    dt nt!_EXCEPTION_POINTERS argument 
    ```

    このコマンドは、構造を表示します。 コンテキスト レコードのアドレスに注意してください。

3.  使用して、 [ **.cxr (コンテキスト レコードの表示)** ](-cxr--display-context-record-.md)コマンドし、として前の手順で検出されたコンテキスト レコードを指定して*レコード*します。

    ```dbgcmd
    .cxr record 
    ```

    このコマンドは、レジスタのコンテキストを適切な値に設定します。

4.  さまざまなコマンドを使用すると、エラーの原因を分析できます。 始まり[ **kb (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)します。

<span id="parameter-1-equals-0x101"></span><span id="PARAMETER-1-EQUALS-0X101"></span>
**バグ チェック 0xA0 0x101 がパラメーター 1 の場合のデバッグ**

1.  使用して、 [ **dt (表示の種類)** ](dt--display-type-.md)コマンドし、パラメーター 3 としての値を指定*引数*します。

    ```dbgcmd
    dt nt!_EXCEPTION_POINTERS argument 
    ```

    このコマンドは、構造を表示します。 コンテキスト レコードのアドレスに注意してください。

2.  使用して、 [ **.cxr (コンテキスト レコードの表示)** ](-cxr--display-context-record-.md)コマンドし、前の手順として検出されたコンテキスト レコードを指定して*レコード*します。

    ```dbgcmd
    .cxr record 
    ```

    このコマンドは、レジスタのコンテキストを適切な値に設定します。

3.  さまざまなコマンドを使用すると、エラーの原因を分析できます。 始まり[ **kb (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)します。

 

 




