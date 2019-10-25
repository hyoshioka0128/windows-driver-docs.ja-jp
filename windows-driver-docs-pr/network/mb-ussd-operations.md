---
title: MB USSD 操作
ms.assetid: 49D106BD-F938-4BF8-88EE-A4D0F0E2722A
description: MB デバイスの非構造化補助サービスデータ (USSD) 機能を使用してメッセージを送受信する操作について説明します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba3c33cdf2eb67f50eeb3662df99c4c7c1f61526
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844267"
---
# <a name="mb-ussd-operations"></a>MB USSD 操作


このトピックでは、MB デバイスの非構造化補助サービスデータ (USSD) 機能を使用してメッセージを送受信する操作について説明します。

USSD サポートはオプションであり、サポートされている場合は GSM ネットワークでのみ使用できます。 USSD をサポートするミニポートドライバーでは、OID を処理するときに、wwan [ **\_デバイス\_caps**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_device_caps)構造体の**Wwancontrolcaps**メンバーの一部として、WWAN\_CTRL\_caps\_USSD 機能フラグを設定する必要があり[\_WWAN\_デバイス\_CAP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps)要求。 ミニポートドライバーで USSD がサポートされていない場合は、このフラグを設定しないでください。また、USSD に関連付けられているすべての Oid に対して\_デバイス\_サポートされていない場合は、WWAN\_\_ステータスを返します。

MB ドライバーモデルは、デバイスによって開始される操作である、次の USSD 操作をサポートしています。

-   新しく作成された USSD セッションで USSD メッセージを送信する

-   新しく作成された USSD セッションで USSD メッセージを送信する

-   既存の USSD セッションでの USSD メッセージの送信

-   USSD セッションを終了しています

デバイスによって開始される操作の詳細については、「 [OID\_WWAN\_USSD](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ussd)」を参照してください。

ネットワークによって開始される操作:

-   新しく作成された USSD セッションで USSD メッセージを受信する

-   既存の USSD セッションで USSD メッセージを受信する

-   USSD セッションを終了します。

ネットワークによって開始される操作の詳細については、「 [**NDIS\_STATUS\_WWAN\_USSD**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd)」を参照してください。

USSD プロトコルでは、一度に1つの USSD セッションのみが許可されます。 デバイスが開始した操作の場合、 [**WWAN\_USSD\_要求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_ussd_request)構造の**RequestType**メンバーは、要求 OID の目的を示します。

-   **Wwanussdrequestinitiate**は、新しい USSD セッションを作成し、指定された USSD 文字列をネットワークに送信するために使用されます。 USSD セッションが既に存在する場合、ドライバーは、種類が**Wwanussdeventoole client**のイベントで要求を失敗させる必要があります。 USSD 文字列が存在する必要があります。 たとえば、長さは1から160バイトの範囲である必要があります。

-   **Wwanussdrequestcontinue**は、既存のセッションで USSD 文字列を送信するために使用されます。 USSD 文字列が存在する必要があります。 たとえば、長さは1から160バイトの範囲である必要があります。

-   既存のセッションを終了するには、 **Wwanussdrequestcancel**を使用します。 ドライバーは、 **WwanUssdEventTerminated**型のイベントで応答する必要があります (これは、ネットワークとローカルクライアントからのセッションの同時リリース時に発生する可能性があります)。 この要求では、USSD 文字列の内容を無視する必要があります。文字列の長さは0に設定され、USSD 文字列が存在しないことを示します。

ネットワークによって開始される操作については、 [**WWAN\_USSD\_イベント**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_ussd_event)構造の**EventType**メンバーは、次のように指示の高レベルの目的を示します。

-   Event **WwanUssdEventNoActionRequired**は、ネットワークによって開始される USSD 通知に使用されるか、またはモバイルで開始された操作の後に追加情報が必要ない場合に使用されます。 Event **WwanUssdEventActionRequired**は、ネットワークによって開始される USSD 要求に使用されます。または、モバイルで開始された操作の後にさらに情報が必要な場合に使用します。 どちらのイベントでも、空でない USSD 文字列が存在する必要があります。 **SessionState**メンバーは、USSD 文字列が USSD セッションの最初のメッセージであるかどうかを示すために使用されます。ネットワークによって開始された USSD セッションの最初のメッセージの場合は**WwanUssdSessionStateNew**に設定し、それ以外の場合は**WwanUssdSessionStateExisting**に設定する必要があります。

-   また、イベント**WwanUssdEventActionRequired**は、セッションが開いたままであることも示します。 他のすべてのイベントは、セッションが閉じられていることを示します。

-   イベント**WwanUssdEventNoActionRequired**と**WWANUSSDEVENTACTIONREQUIRED**は、USSD 文字列を含む唯一のイベントです。 他のすべてのイベントでは、文字列が存在しないことを示すために、USSD 文字列の長さを0に設定する必要があります。 文字列が存在しない場合、 **SessionState**メンバーの値は無視されます。

-   Event **WwanUssdEventTerminated**は、USSD セッションが終了したことを示すために使用されます。

-   イベント**Wwanussdeventoole client**は、セッションが既に開かれているため、新しい USSD セッションを確立できないことを示すために使用されます。 これには、SIM の USSD セッションの終了など、MB スタックから見えないセッションが含まれます。

-   Event **WwanUssdEventOperationNotSupported**は、以前の要求がドライバーまたはデバイスでサポートされていないことを示すために使用されます。

-   Event **WwanUssdEventNetworkTimeOut**は、セッションがネットワークまたはローカルのいずれかによってタイムアウトしたためにセッションが閉じられたことを示すために使用されます。 ドライバーまたはデバイスは、実装固有のタイムアウト後に、非アクティブな USSD セッションをタイムアウトさせます。

 

 





