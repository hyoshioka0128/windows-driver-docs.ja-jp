---
title: ボタンの動作
description: このトピックでは、ハードウェアボタンの予想される動作について説明します。
ms.assetid: 057A4F21-3514-4CCA-BCE2-279E8228B5A9
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 948d355fa315ce028e8befb6eb3e24c426db2b00
ms.sourcegitcommit: a2d1c389f0f413cc967068cbde22a5598e5a5d57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/01/2020
ms.locfileid: "80516774"
---
# <a name="button-behavior"></a>ボタンの動作

このトピックでは、ハードウェアボタンの予想される動作について説明します。

## <a name="required-and-optional-buttons-in-windows10"></a>Windows 10 の必須ボタンとオプションボタン

|オペレーティングシステム/デバイス|電力|ボリュームのアップ/ボリュームダウン|開始|戻る/検索|カメラ|回転ロック|
|---|---|---|---|---|---|---|
|Windows 10 Mobile|必須|必須|WVGA ディスプレイを使用する電話に必要です。 その他のデバイスの場合は省略可能|WVGA ディスプレイを使用する電話に必要です。 その他のデバイスの場合は省略可能|［オプション］|サポートされない|
|デスクトップエディション用 Windows 10 (Home、Pro、Enterprise、および教育)/タブレット|必須|必須|［オプション］|サポートされない|サポートされない|［オプション］|
|デスクトップエディション/その他のデバイス用の Windows 10|必須|キーボードが取り外し可能なデバイスの場合は必須。 他のすべてのデバイスでは省略可能。|［オプション］|サポートされない|サポートされない|［オプション］|

ボタンの要件の詳細については、次を参照してください。

- Windows 10 Mobile については、ハードウェアの[最小要件](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview)に関するセクション2.6 を参照してください。
- Windows 10 for desktop のエディションについては、[ハードウェアの最小要件](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview)に関するセクション3.6 を参照してください。

## <a name="button-behavior-in-windows10"></a>Windows 10 でのボタンの動作

### <a name="single-button-behavior-in-windows10"></a>Windows 10 の単一ボタンの動作

|ボタン|[利用状況]|Windows 10 デスクトップ エディション|Windows 10 Mobile|
|---|---|---|---|
|電力|プレスアンドリリース|オン/オフの切り替え|オン/オフの切り替え|
|電力|プレス アンド ホールド|Shutdown Curtain を起動する|Shutdown Curtain を起動する|
|電力|長いプレスアンドホールド|ハードシャットダウン|ハードウェアのリセット|
|検索|プレスアンドリリース|サポートされない|Cortana (有効な市場)/検索を開始する|
|検索|プレス アンド ホールド|サポートされない|Cortana を起動する、または音声を使用して検索する|
|音量アップ|プレスアンドリリース|ボリュームの増分|ボリュームの増分|
音量アップ|プレス アンド ホールド|ボリューム増分の自動繰り返し|ボリューム増分の自動繰り返し|
|音量を下げる|プレスアンドリリース|ボリュームの降格|ボリュームの降格|
|音量を下げる|プレス アンド ホールド|自動繰り返しボリュームのデクリメント|自動繰り返しボリュームのデクリメント|
|戻る|プレスアンドリリース|前のアプリページ/アプリを閉じる|前のアプリページ/アプリを閉じる|
|戻る|プレス アンド ホールド|タスクスイッチャーの起動|スイッチャー UI を起動する|
|開始||スタート画面の切り替え|スタート画面を表示する|
|回転ロック||サポートされない|サポートされていません (UI オプションがあります)|
|カメラのフォーカス||カメラアプリケーションの起動|カメラアプリで処理 (フォーカス)|
|カメラシャッター||カメラアプリケーションによって処理される|カメラアプリの起動/画像の撮影|

### <a name="button-combination-behavior-in-windows10"></a>Windows 10 でのボタンの組み合わせ動作

前述のように、Windows 10 の一部のボタンの組み合わせは、 [windows 10 のボタンのアーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/hid/buttons)または Windows 8.1 ボタンのアーキテクチャに適用されます。 Windows 10 のその他すべてのボタンの組み合わせは、いずれのボタンのアーキテクチャにも適用されます。 Windows 10 アーキテクチャを使用してハードウェアボタンを記述することをお勧めします。

|ボタンの組み合わせ|Windows 10 デスクトップ エディション|Windows 10 Mobile|
|---|---|---|
|開始 + ボリュームアップ|画面上のナレーターの切り替え|画面に表示されるナレーターの切り替え (対応する [アクセスしやすさ] 設定が有効になっている場合)|
|開始 + 音量を下げる|スクリーンショットを撮る|サポートされない|
|開始 + 電源|Ctrl + Alt + Del (Windows 8.1 ボタンのアーキテクチャを使用する場合のみ)|サポートされない|
|電力 + ボリュームアップ|スクリーンショットを撮る (Windows 10 のボタンアーキテクチャを使用している場合のみ)|スクリーンショットを撮る|
|電源 + 音量ダウン|Ctrl + Alt + Del (Windows 10 のボタンアーキテクチャを使用する場合のみ)|Windows フィードバックアプリを起動します。 ハードウェアのリセット (10 秒後)|

## <a name="button-behavior-in-windows-81"></a>Windows 8.1 でのボタンの動作

### <a name="single-button-behavior-in-windows-81"></a>Windows 8.1 での1つのボタンの動作

|ボタン|操作|Windows 8.1|Windows 8.1 Phone|
|---|---|---|---|
|電力|プレスアンドリリース|オン/オフの切り替え|オン/オフの切り替え|
|電力|プレス アンド ホールド|Shutdown Curtain を起動する|Shutdown Curtain を起動する|
|電力|長いプレスアンドホールド|ハードシャットダウン|ハードウェアのリセット|
|検索|プレスアンドリリース|サポートされない|Cortana を起動する|
|検索|プレス アンド ホールド|サポートされない|音声を使用して Cortana を起動する|
|音量アップ|プレスアンドリリース|ボリュームの増分|ボリュームの増分|
|音量アップ|プレス アンド ホールド|ボリューム増分の自動繰り返し|ボリューム増分の自動繰り返し|
|音量を下げる|プレスアンドリリース|ボリュームの降格|ボリュームの降格|
|音量を下げる|プレス アンド ホールド|自動繰り返しボリュームのデクリメント|自動繰り返しボリュームのデクリメント|
|戻る||サポートされない|サポートされない|
|開始||スタート画面の切り替え|スタート画面の切り替え|
|回転ロック||リリース: ロックのローテーション|ロックのローテーション|
|カメラのフォーカス||サポートされない|該当なし|
|カメラシャッター||サポートされない|該当なし|

### <a name="button-combination-behavior-in-windows-81"></a>Windows 8.1 でのボタンの組み合わせ動作

|ボタンの組み合わせ|Windows 8.1|Windows 8.1 Phone|
|---|---|---|
|開始 + ボリュームアップ|画面上のナレーターの切り替え|サポートされない|
|開始 + 音量を下げる|スクリーンショットを撮る|サポートされない|
|開始 + 電源|Ctrl+Alt+Del|サポートされない|
|電力 + ボリュームアップ|サポートされない|スクリーンショットを撮る|
|電源 + 音量ダウン|サポートされない|ハードウェアのリセット (10 秒後)|

## <a name="related-topics"></a>関連トピック

[Windows 10 のボタンのアーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/hid/buttons)  
[最小ハードウェア要件](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview)  
