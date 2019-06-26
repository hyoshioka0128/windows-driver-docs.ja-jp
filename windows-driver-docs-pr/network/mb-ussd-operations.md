---
title: MB USSD 操作
ms.assetid: 49D106BD-F938-4BF8-88EE-A4D0F0E2722A
description: MB デバイスの非構造化補助サービス データ (USSD) 機能を使用してメッセージを送受信する操作について説明します
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 82b097b5b1d14a9c575e61b751a5e3cd595eb507
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374008"
---
# <a name="mb-ussd-operations"></a>MB USSD 操作


このトピックでは、MB デバイスの非構造化補助サービス データ (USSD) 機能を使用してメッセージを送受信する操作について説明します。

USSD サポートは省略可能と GSM ネットワークで使用可能なはサポートされています。 USSD をサポートするミニポート ドライバーで、WWAN を設定する必要があります\_CTRL\_CAP\_USSD 機能フラグの一部として、 **WwanControlCaps**のメンバー、 [ **WWAN\_デバイス\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_device_caps)構造の処理時に[OID\_WWAN\_デバイス\_CAP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps)要求。 ミニポート ドライバーは USSD をサポートしていない場合は、このフラグを設定する必要があり、WWAN を返す必要があります\_状態\_いいえ\_デバイス\_USSD に関連するすべての Oid をサポートします。

MB ドライバー モデルには、次の USSD 操作がサポートされています。デバイスは、操作を開始します。

-   新しく作成された USSD セッションで USSD メッセージを送信

-   新しく作成された USSD セッションで USSD メッセージを送信

-   既存の USSD セッションで USSD メッセージを送信

-   USSD セッションを終了しています

デバイスが開始した操作の詳細については、次を参照してください。 [OID\_WWAN\_USSD](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ussd)します。

開始された操作をネットワークします。

-   新しく作成された USSD セッションで USSD メッセージを受け取る

-   既存の USSD セッションで USSD メッセージの受信

-   USSD セッションの終了

ネットワークが開始した操作の詳細については、次を参照してください。 [ **NDIS\_状態\_WWAN\_USSD**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd)します。

USSD プロトコルは、いつでも 1 つの USSD セッションのみを許可します。 デバイスの操作を開始、 **RequestType**のメンバー、 [ **WWAN\_USSD\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_ussd_request)構造の目的を示す、OID の要求:

-   **WwanUssdRequestInitiate**新しい USSD セッションを作成し、ネットワークに指定された USSD 文字列を送信するために使用します。 ドライバーとイベントの種類の要求は失敗する必要があります、USSD セッションは既に存在する場合、 **WwanUssdEventOtherLocalClient**します。 USSD 文字列は、存在する必要があります。 たとえば、長さが 1 ~ 160 バイトあります。

-   **WwanUssdRequestContinue** USSD 文字列を既存のセッションに送信するために使用します。 USSD 文字列は、存在する必要があります。 たとえば、長さが 1 ~ 160 バイトあります。

-   **WwanUssdRequestCancel**既存のセッションを終了するために使用します。 ドライバーが型のイベントに応答する必要があります**WwanUssdEventTerminated**(これは、ネットワークとローカル クライアントからのセッションの同時リリース中に発生する可能性があります) をどのセッションも存在していない場合でも、します。 この要求の USSD 文字列の内容を無視する必要があります。文字列の長さは、USSD 文字列がないことを示す 0 に設定されます。

ネットワークの操作を開始、 **EventType**のメンバー、 [ **WWAN\_USSD\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_ussd_event)構造が高レベルの目的を示します表示。

-   イベント**WwanUssdEventNoActionRequired**ネットワーク USSD の通知を開始するため、またはモバイルでの運用が開始された後に詳細な情報は必要ありませんに使用します。 イベント**WwanUssdEventActionRequired**ネットワーク開始 USSD 要求、またはモバイルでの運用が開始された後にさらに情報が必要なときに使用されます。 両方のイベントには、空でない USSD 文字列に存在する必要があります。 **SessionState** USSD 文字列が USSD セッションの最初のメッセージを示すメンバーが使用される以外設定する必要があります**WwanUssdSessionStateNew**のネットワークの最初のメッセージには、USSD セッションが開始しました。および**WwanUssdSessionStateExisting**それ以外の場合。

-   イベント**WwanUssdEventActionRequired**も、セッションがまだ開かれていることを示します。 その他のすべてのイベントは、セッションが閉じられたことを示しています。

-   イベント**WwanUssdEventNoActionRequired**と**WwanUssdEventActionRequired** USSD 文字列が含まれるイベントのみが。 その他のすべてのイベントは、文字列が存在しないことを示す 0 に USSD 文字列の長さを設定する必要があります。 値、 **SessionState**文字列が存在しない場合、メンバーは無視されます。

-   イベント**WwanUssdEventTerminated** USSD セッションが終了されたことを示すために使用されます。

-   イベント**WwanUssdEventOtherLocalClient**を既に開かれたセッションがあるため、新しい USSD セッションを確立できないことを示すために使用します。 これには、SIM で USSD セッションの終了など MB のスタックに表示されるセッションが含まれます。

-   イベント**WwanUssdEventOperationNotSupported**ドライバーまたはデバイスでは、前の要求がサポートされていないことを示すために使用されます。

-   イベント**WwanUssdEventNetworkTimeOut**ネットワークによって、またはローカルのセッション タイムアウトのため、セッションが閉じられたことを示すために使用されます。 ドライバーまたはデバイスは、実装固有のタイムアウト後の非アクティブの USSD セッション タイムアウトを担当します。

 

 





