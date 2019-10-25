---
title: モードレスダイアログの WIA エラーハンドラーのキャンセル
description: モードレスダイアログの WIA エラーハンドラーのキャンセル
ms.assetid: eca6c3a3-c196-4d28-925a-c8f5d5d8601b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a4f71fd5122fbd8f36f4c182b3cf6b2f9869271
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840698"
---
# <a name="wia-error-handler-cancellation-of-modeless-dialogs"></a>モードレスダイアログの WIA エラーハンドラーのキャンセル


エラーハンドラーの複雑さの多くは、モードレスダイアログボックスのキャンセルと無視がどのように処理されるかを中心にしています。

特に、WIA プロキシコードは、低レベルのエラーハンドラー (つまり、そのアプリケーションのエラーハンドラー以外のハンドラー) が、モードレスダイアログからドライバーに取り消し要求を返信する機会を持つことを保証します。これにより、下位レベルのハンドラーが、モードレスダイアログボックスを閉じる機会を得ることができます。

エラーハンドラーがモードレスダイアログからデータ転送操作をキャンセルできるようにするには、ドライバーは、同じ*hrErrorStatus*コードを使用して、\_MSG\_デバイス\_ステータスメッセージを\_送信します。*Lpercentcomplete*率パラメーターを更新して、エラーハンドラー UI で進行状況を表示できるようにします。 たとえば、ドライバーが "ウォームアップ" にかかる時間を見積もることができる場合、 *hrErrorStatus*が WIA に設定されている複数のデバイスメッセージを送信して、\_状態\_ウォームアップ\_を行うことができます。 これにより、エラーハンドラーは進行状況ダイアログを表示できるだけでなく、ユーザーがこのダイアログボックスから転送を取り消す機会を与えることができます。 [**IWiaErrorHandler:: ReportStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wia_lh/nf-wia_lh-iwiaerrorhandler-reportstatus)に渡される*lpercentcomplete*パラメーターは、ドライバーが**Iwiatransfercallback:: Wiatranstarparams**メソッドで設定するのとまったく同じ*lranパラメーター*です。 この例については、WDK CD の Extended WIA モンスタードライバーを参照してください。

エラーハンドラーがモードレスダイアログを閉じることを許可するために、Microsoft はデバイスの状態コード WIA\_状態\_クリアを導入しました。 このメッセージは、現在表示されているものとは別のデバイスメッセージを WIA プロキシが受信したときに、現在モードレス UI を表示しているエラーハンドラーに、WIA プロキシによって送信されます。 また、次の場合に、プロキシは WIA\_状態\_クリアメッセージを送信します。

ドライバーは、WIA\_TRANSFER\_メッセージ\_ステータスメッセージを送信します。

**Iwiatransfercallback:: GetNextStream**メソッドの呼び出し中

ストリーム/転送の最後 (モードレス UI を表示しているエラーハンドラーがある場合)。

ドライバーは、WIA\_状態\_クリアメッセージを送信しないようにする必要があります。

**Iwiatransのコールバック**インターフェイスについては、Microsoft Windows SDK のドキュメントを参照してください。

 

 




