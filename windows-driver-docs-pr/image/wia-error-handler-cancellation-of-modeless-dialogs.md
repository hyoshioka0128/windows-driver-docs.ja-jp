---
title: モードレス ダイアログの WIA エラー ハンドラーのキャンセル
description: モードレス ダイアログの WIA エラー ハンドラーのキャンセル
ms.assetid: eca6c3a3-c196-4d28-925a-c8f5d5d8601b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e303e750fa61e0a48e72e05f56b8c71a57b5d7d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392544"
---
# <a name="wia-error-handler-cancellation-of-modeless-dialogs"></a>モードレス ダイアログの WIA エラー ハンドラーのキャンセル


キャンセルとモードレス ダイアログ ボックスのジョンソンの処理方法中心とエラー ハンドラーの複雑さの多くとします。

具体的には、WIA プロキシ コードにより、下位レベルのエラー ハンドラー (つまりは、そのアプリケーションのエラー ハンドラー以外ハンドラー) が、ドライバーにモードレス ダイアログ ボックスからキャンセル要求をやり取りすることを取得します。これにより、下位レベルのハンドラーがそのモードレス ダイアログ ボックスを破棄する機会を取得します。

モードレス ダイアログからのデータ転送操作をキャンセルするエラー ハンドラーを許可するには、ドライバーが送信を続けます WIA\_転送\_MSG\_デバイス\_のステータス メッセージを同じ *。hrErrorStatus*コード、更新、 *lPercentComplete*パラメーター エラー ハンドラーに進行状況を表示する UI を許可します。 例: ドライバーが時間の長い方法の推定値を与えることができる場合「ウォーミング アップ」は本当に、、さまざまなデバイス メッセージを送信できる*hrErrorStatus* WIA に設定\_状態\_WARMING\_をします。 これにより、このダイアログ ボックスからの転送をキャンセルする機会をユーザーに提供に加えて、進行状況ダイアログを表示するエラー ハンドラーが許可されます。 *LPercentComplete*パラメーターに渡す[ **IWiaErrorHandler::ReportStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff543909)は同じ正確な*lPercentComplete*ドライバーに設定するパラメーター、 **IWiaTransferCallback::WiaTransferParams**メソッド。 これの例は、WDK の CD に収録 WIA モンスターの拡張ドライバーを参照してください。

モードレス ダイアログ ボックスを消去するエラー ハンドラーを許可するのには、Microsoft はデバイスの状態コード WIA を導入しました。\_状態\_クリアします。 このメッセージは、WIA プロキシは、現在表示されている 1 つから別のデバイス メッセージを受信するときに、モードレスの UI を現在表示されているエラー ハンドラーに WIA プロキシによって送信されます。 また、WIA が送信され、プロキシ\_状態\_オフ メッセージします。

ドライバーを送信する、WIA\_転送\_メッセージ\_、ステータス メッセージ

呼び出し中に、 **IWiaTransferCallback::GetNextStream**メソッド

ストリーム転送 (モードレスの UI を表示するエラー ハンドラーが現在) 場合の最後にします。

ドライバーは、WIA を送信しないでください\_状態\_オフ メッセージの送受信自体。

**IWiaTransferCallback**インターフェイスは、Microsoft Windows SDK ドキュメントで説明します。

 

 




