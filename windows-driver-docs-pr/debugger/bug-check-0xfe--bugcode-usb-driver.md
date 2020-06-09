---
title: バグチェック 0xFE BUGCODE_USB_DRIVER
description: BUGCODE_USB_DRIVER バグチェックの値は、0x000000FE です。 これは、ユニバーサルシリアルバス (USB) ドライバーでエラーが発生したことを示します。
ms.assetid: 830f9d11-4b16-41a9-a804-6d689a779278
keywords:
- バグチェック 0xFE BUGCODE_USB_DRIVER
- BUGCODE_USB_DRIVER
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- BUGCODE_USB_DRIVER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 48005be82b35a9ec3e3979395cc044c05192f282
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534511"
---
# <a name="bug-check-0xfe-bugcode_usb_driver"></a>バグチェック 0xFE: バグコード \_ USB \_ ドライバー


バグコードの \_ USB \_ ドライバーのバグチェックの値は、0x000000fe です。 これは、ユニバーサルシリアルバス (USB) ドライバーでエラーが発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="bugcode_usb_driver-parameters"></a>バグコードの \_ USB \_ ドライバーパラメーター


4つのバグチェックパラメーターがバグチェックの停止画面に表示され、! analyze を使用して使用できます。 パラメーター1は違反の種類を識別します。

| パラメーター 1 | パラメータ 2 | パラメーター3 | パラメーター4 | エラーの原因                            | 
|-------------|-------------|-------------|-------------|-------------------------------------------|
| 0x1 | 予約済み | 予約済み | 予約済み | USB スタックで内部エラーが発生しました。 |
| 0x2 | 保留中の IRP のアドレス | 渡された IRP のアドレス| エラーの原因となった USB 要求ブロック (URB) のアドレス | USB クライアントドライバーは、バスドライバーで保留中の別の IRP にまだ接続されている URB を送信しました。| 
|0x3| 予約済み | 予約済み| 予約済み| USB ミニポートドライバーにより、バグチェックが生成されました。 これは通常、ハードウェア障害が発生した場合に発生します。|
| 0x4 | IRP のアドレス| URB のアドレス| 予約済み| 呼び出し元は、USB バスドライバーで既に保留になっている IRP を送信しました。| 
| 0x5| ホストコントローラーのデバイス拡張機能ポインター| PCI ベンダー、コントローラーの製品 id| エンドポイントデータ構造へのポインター| ハードウェアのデータ構造に不良な物理アドレスがあるため、ハードウェア障害が発生しました。| 
| 0x6 | オブジェクトのアドレス| 必要な署名| 予約済み | 内部データ構造 (オブジェクト) が破損しています。|
| 0x7 | Usbport デバッグログへのポインター | メッセージ文字列 | ファイル名 | 詳細については、提供されているメッセージ文字列を参照してください。|
| 0x8 | 1 | 予約済み | 予約済み | 予約済み |
| | 2 | デバイス オブジェクト  | IRP | IRP は、予期しない、または登録されていないハブドライバーによって受信されました。 |
| | 3 | 予約済み | 予約済み | 予約済み
| | 4 | パラメーター3が NULL でない場合は PDO。 パラメーター3が NULL の場合のコンテキスト。 | コンテキストまたは NULL | 致命的な PDO トラップ
| | 5 | 予約済み | 予約済み | 予約済み |
| | 6 | タイムアウトコード。 次の表を参照してください。 | タイムアウトコードコンテキスト: ポートデータ | 致命的なタイムアウト

パラメーター1の値が8で、パラメーター2の値が6の場合、パラメーター3はタイムアウトコードです。 タイムアウトコードに指定できる値を次の表に示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">タイムアウトコード</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>致命的でないタイムアウト</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>中断されたポートの再開に失敗しました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>クライアントドライバーによって開始されたリセットが完了するのを待機中にタイムアウトになり、ポートが中断されました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>ポートを中断する前に、ポートが再開されるのを待機中にタイムアウトしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>ポート変更ステートマシンが無効になるのを待機しているときに、ポートを中断する前にタイムアウトしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>5</p></td>
<td align="left"><p>中断ポート要求の完了を待機中にタイムアウトしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"><p>ポート変更ステートマシンが無効になるのを待機中にタイムアウトしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>7</p></td>
<td align="left"><p>ポート変更ステートマシンが閉じられるのを待機中にタイムアウトしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>8</p></td>
<td align="left"><p>ハブが選択的中断から再開されるのを待機中にタイムアウトしました。</p></td>
</tr>
<tr class="even">
<td align="left"><p>9</p></td>
<td align="left"><p>システムの中断の前に、選択的中断からハブが再開されるのを待機中にタイムアウトしました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>10</p></td>
<td align="left"><p>ポート変更ステートマシンがアイドル状態になるのを待機中にタイムアウトになりました。</p></td>
</tr>
</tbody>
</table>

## <a name="resolution"></a>解像度

! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。
 
 

 




