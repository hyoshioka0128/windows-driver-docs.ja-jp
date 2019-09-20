---
title: Microsoft ドライバーの測定に関する辞書の付録
description: Microsoft ドライバーの測定に関する辞書の補足資料集
ms.topic: article
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: dbaff20d8857aaac03331fd3df5a403fc008e07b
ms.sourcegitcommit: b33dff0fc9b5b90ee8bd07f62713c58c5f60b40f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/16/2019
ms.locfileid: "71016984"
---
# <a name="appendix-for-the-microsoft-driver-measure-dictionary"></a>Microsoft ドライバーの測定に関する辞書の付録

## <a name="top-microsoft-apps-example"></a>Microsoft のトップ アプリの例

|アプリケーション|アプリケーションの種類|
|----|----|
|Devenv.exe|開発者ツール|
|MS ペイント|エンターテイメント|
|Microsoft Skype アプリ|通信とコラボレーション|
|Microsoft Windows フォト|メディア|
|Microsoft Windows 通信アプリ|生産性|
|Microsoft ペイント|クリエイティブ|
|Microsoft Solitaire Collection|ゲーム|
|OneDrive|クラウドの記憶域|
|Windows コンポーネント|Windows コンポーネント|
|Microsoft Edge|Browser|
|Microsoft Windows DVD プレーヤー|エンターテイメント|
|Microsoft Zune Video|メディア|
|Msaccess.exe|開発者ツール|
|Outlook|生産性|
|Excel|生産性|
|Internet Explorer|Browser|
|Msvsmon.exe|開発者ツール|
|Minecraft: Windows 10 Edition Beta|ゲーム|
|Powershell_Ise.exe|開発者ツール|
|Skype|通信とコラボレーション|
|Winword.exe|生産性|
|Lync.exe|通信とコラボレーション|
|Msosync.exe|クラウドの記憶域|
|Microsoft One Connect|生産性|
|Windbg.exe|開発者ツール|
|Microsoft Office OneNote|生産性|
|Microsoft Mahjong|ゲーム|
|Power Point|生産性|
|Windbg.exe|開発者ツール|
|Microsoft Office OneNote|生産性|
|Microsoft Zune Music|メディア|
|Microsoft Mahjong|ゲーム|
|PowerPoint|生産性|
|Minecraft|ゲーム|
|Microsoft メッセージング|通信とコラボレーション|
|Microsoft Microsoft SkyDrive|クラウドの記憶域|
|Moviemaker.exe|クリエイティブ|

## <a name="creative-applications-example"></a>クリエイティブ アプリケーションの例

|アプリケーション|
|----|
|MSPaint.exe|
|Photoshop.eve|
|SnagitEditor.exe|
|Adobe Premiere Pro.exe|
|LightRoom.exe|
|AfterFX.eve|
|ClipStudioPaint.exe|
|Audacity.exe|
|SAI.exe|
|FL.exe|

## <a name="display-issues"></a>ディスプレイの問題

|アプリケーション|
|----|
|不適切な解像度でディスプレイが実行されている|
|画面がちらつく|
|ディスプレイが機能しない|
|想定外の向き|
|最適ではないディスプレイの設定が有効になっている|

## <a name="audio-initialization-benign-failure-codes"></a>オーディオ初期化に関する良性エラー コード

### <a name="common-benign-errors"></a>一般的な良性エラー

AEERR_E_EXISTING_DIRECTKS_CLIENT

AEERR_E_EXISTING_EXCLUSIVE_CLIENT

AEERR_E_EXISTING_SHARED_CLIENT

AEERR_E_PIN_LOCKED

AEERR_NO_CONVERTERS_FOUND

AEERR_POLICY_ACCESS_DENIED

AUDCLNT_E_DEVICE_INVALIDATED

### <a name="aeerr_device_in_use-benign-errors"></a>AEERR_DEVICE_IN_USE Benign Errors

HResult == AEERR_DEVICE_IN_USE

Platform == Windows.Mobile

OffloadRequested == 1

同じ AudioClientGuidId で、OffloadRequested == 0 および HResult == SUCCESS である別の AudioClientInitialize イベントも存在します。

### <a name="benign-race-condition-errors"></a>良性の競合状態エラー

HResult == ERROR_PATH_NOT_FOUND または ERROR_NOT_FOUND または ERROR_NOT_CONNECTED

App == Windows Explorer または Windows Shell Experience Host

### <a name="benign-parameter-error"></a>良性のパラメーター エラー

アプリ "videoeditor(plus)"、"screenrecorder"、"neilsenonline" から ERROR_INVALID_PARAMETER をフィルター処理します。
