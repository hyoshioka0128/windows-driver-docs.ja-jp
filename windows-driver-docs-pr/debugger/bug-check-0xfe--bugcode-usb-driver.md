---
title: バグ チェック 0 xfe BUGCODE_USB_DRIVER
description: BUGCODE_USB_DRIVER のバグ チェックでは、0x000000FE の値を持ちます。 これは、ユニバーサル シリアル バス (USB) ドライバーでエラーが発生したことを示します。
ms.assetid: 830f9d11-4b16-41a9-a804-6d689a779278
keywords:
- バグ チェック 0 xfe BUGCODE_USB_DRIVER
- BUGCODE_USB_DRIVER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BUGCODE_USB_DRIVER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 268e31eb353f6ec817a0842d3a5244b6a6d75875
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518713"
---
# <a name="bug-check-0xfe-bugcodeusbdriver"></a>バグ チェック 0xFE:BUGCODE\_USB\_ドライバー


BUGCODE\_USB\_ドライバーのバグ チェックが 0x000000FE の値を持ちます。 これは、ユニバーサル シリアル バス (USB) ドライバーでエラーが発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="bugcodeusbdriver-parameters"></a>BUGCODE\_USB\_ドライバーのパラメーター


バグ チェック停止画面と使用可能なを使用して、4 つのバグ チェック パラメーターが表示されます。 分析します。 パラメーター 1 では、違反の種類を識別します。

| パラメーター 1 | パラメータ 2 | 3 番目のパラメーター | パラメーター 4 | エラーの原因                            | 
|-------------|-------------|-------------|-------------|-------------------------------------------|
| 0x1 | 予約済み | 予約済み | 予約済み | USB スタックで内部エラーが発生しました。 |
| 0x2 | 保留中の IRP のアドレス | 渡された IRP のアドレス| エラーの原因となった USB 要求ブロック (URB) のアドレス | USB クライアント ドライバーでは、バス ドライバーで保留中の別の IRP にまだ接続されている URB を送信しました。| 
|0x3| 予約済み | 予約済み| 予約済み| USB ミニポート ドライバーには、バグ チェックが生成されます。 これは、通常、ハードウェアの障害への応答で発生します。|
| 0x4 | IRP のアドレス| URB のアドレス| 予約済み| 呼び出し元が保留になっている IRP を送信、USB バス ドライバー。| 
| 0x5| ホスト コント ローラーのデバイスの拡張機能のポインター| PCI の仕入先、コント ローラーの製品 id| エンドポイントのデータ構造体へのポインター| ハードウェアのデータ構造で検出された不正な物理アドレスのため、ハードウェア障害が発生しました。| 
| 0x6 | オブジェクトのアドレス| 署名が必要です。| 予約済み | 内部データ構造 (オブジェクト) が壊れています。|
| 0x7 | Usbport.sys デバッグ ログへのポインター | メッセージ文字列 | ファイル名 | 詳細については、指定されたメッセージ文字列を参照してください。|
| 0x8 | 1 | 予約済み | 予約済み | 予約済み |
| | 2 | デバイス オブジェクト  | IRP | 予期しないまたはが登録されていないハブ ドライバーが IRP を受信しました。 |
| | 3 | 予約済み | 予約済み | 予約済み
| | 4 | PDO パラメーター 3 が NULL でない場合。 コンテキスト パラメーターが NULL の場合。 | コンテキストまたは NULL | 致命的な PDO トラップ
| | 5 | 予約済み | 予約済み | 予約済み |
| | 6 | タイムアウト コードです。 次の表を参照してください。 | タイムアウト コード コンテキスト: データの移植 | 致命的なタイムアウト

パラメーター 1 が 8 の値を持つ、パラメーター 2 が 6 の値を持つ場合は、パラメーター 3、タイムアウト コード。 タイムアウト コードに指定できる値は、次の表に付与されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">タイムアウト コード</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>致命的でないタイムアウト</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>中断されているポートを再開できませんでした。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>ポートを中断する前に完了する、クライアント ドライバーによって開始された、リセットの待機中にタイムアウトしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>これを中断する前の再開を完了するポートを待機中にタイムアウトになりました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>ポートを中断する前に無効にするポートの変更のステート マシンの待機中にタイムアウトします。</p></td>
</tr>
<tr class="even">
<td align="left"><p>5</p></td>
<td align="left"><p>ポートの中断要求が完了するを待機中にタイムアウトになりました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"><p>ポートの変更のステート マシンを無効にするを待機中にタイムアウトになりました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>7</p></td>
<td align="left"><p>終了するポートの変更のステート マシンの待機中にタイムアウトします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8</p></td>
<td align="left"><p>選択的から再開するハブの待機中にタイムアウトを中断します。</p></td>
</tr>
<tr class="even">
<td align="left"><p>9</p></td>
<td align="left"><p>選択的から再開するハブの待機中にタイムアウト システムの前に中断を中断します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p>アイドル状態になるポートの変更のステート マシンの待機中にタイムアウトします。</p></td>
</tr>
</tbody>
</table>

## <a name="resolution"></a>解決方法

[ **! 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるに役に立ちます。
 
 

 




