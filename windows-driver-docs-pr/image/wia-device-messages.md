---
title: WIA デバイス メッセージ
description: WIA デバイス メッセージ
ms.assetid: b498a75d-1252-4f13-ae62-9a53491c2bde
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d27a47b4988e4168f9f0e20685a0b4275599ebe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355075"
---
# <a name="wia-device-messages"></a>WIA デバイス メッセージ


次の一覧には、現在定義されているすべての WIA デバイス メッセージが表示されます。 中にこれらのメッセージを送信できる**IWiaTransfer::Download**と**IWiaTransfer::Upload**します。 **IWiaTransfer**インターフェイスは、Microsoft Windows SDK ドキュメントで説明します。

### <a name="device-status-messages"></a>デバイスのステータス メッセージ:

-   WIA\_状態\_WARMING\_を

-   WIA\_状態\_キャリブレーション

-   WIA\_状態\_RESERVING\_ネットワーク\_デバイス

-   WIA\_状態\_ネットワーク\_デバイス\_予約済み

-   WIA\_状態\_クリア

### <a name="device-error-messages"></a>デバイスのエラー メッセージ:

-   WIA\_エラー\_全般\_エラー

-   WIA\_エラー\_用紙\_詰まり

-   WIA\_エラー\_用紙\_空

-   WIA\_エラー\_用紙\_問題

-   WIA\_エラー\_オフライン

-   WIA\_エラー\_ビジー

-   WIA\_エラー\_WARMING\_を

-   WIA\_エラー\_ユーザー\_介入

-   WIA\_エラー\_項目\_削除済み

-   WIA\_エラー\_デバイス\_通信

-   WIA\_エラー\_無効な\_コマンド

-   WIA\_エラー\_正しくない\_ハードウェア\_設定

-   WIA\_エラー\_デバイス\_ロック

-   WIA\_エラー\_例外\_IN\_ドライバー

-   WIA\_エラー\_無効な\_ドライバー\_応答

-   WIA\_エラー\_カバー\_開く

-   WIA\_エラー\_LAMP\_OFF

-   WIA\_エラー\_変換先

-   WIA\_エラー\_ネットワーク\_予約\_失敗

WIA の既定のエラー ハンドラー

現在、WIA の既定のエラー ハンドラーは、次のデバイス メッセージをサポートします。

-   WIA\_状態\_WARMING\_を

-   WIA\_状態\_キャリブレーション

-   WIA\_状態\_RESERVING\_ネットワーク\_デバイス

-   WIA\_状態\_ネットワーク\_デバイス\_予約済み

-   WIA\_エラー\_用紙\_詰まり

-   WIA\_エラー\_デバイス\_ロック

-   WIA\_エラー\_ネットワーク\_予約\_失敗

-   WIA\_エラー\_カバー\_開く

-   WIA\_エラー\_LAMP\_OFF

-   WIA\_エラー\_変換先

-   WIA\_エラー\_用紙\_空

 

 




