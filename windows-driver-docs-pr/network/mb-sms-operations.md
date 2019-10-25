---
title: MB SMS 操作
description: MB SMS 操作
ms.assetid: 9a21495c-ec3d-4277-b880-dbf5b081814a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ca8ac9c17bab9d39c653de8da6fc64aedd39c6f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844270"
---
# <a name="mb-sms-operations"></a>MB SMS 操作


このトピックでは、MB デバイスのショートメッセージサービス (SMS) 機能を使用して、メッセージを構成、読み取り/受信、送信、および削除する操作について説明します。

SMS サポートは必須です。 ミニポートドライバーは、wwan\_デバイスの**Wwansmscaps**メンバーで、 [OID\_wwan\_デバイス\_cap](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps)クエリ要求を処理するときにサポートされる、適切な送信および受信の SMS 機能フラグを設定する必要があり[ **@no__** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_device_caps)形式の CAPS 構造体。 ミニポートドライバーで SMS がサポートされていない場合は、すべての SMS 関連 Oid について、WWAN\_SMS\_CAP\_NONE を指定し、WWAN\_ステータス\_SMS\_不明な\_エラーを返す必要があります。

ミニポートドライバーは、 [OID\_WWAN\_準備完了\_情報](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ready-info)がデバイスの準備完了状態として**WwanReadyStateInitialize**を返す場合にのみ、SMS 操作を処理する必要があります。 ミニポートドライバーは、SMS メッセージの送信など、一部の SMS 操作を、デバイスがプロバイダーネットワークに登録された後にのみ処理する必要があります (ただし、データサービスの登録は必ずしも行われません)。

MB サービスは、デバイスで使用できるさまざまなメッセージストアを区別しません。 そのため、ミニポートドライバーは、すべてのメッセージストアを処理し、仮想インデックスを介してアクセスされる単一の仮想メッセージストアを射影する必要があります。 たとえば、デバイスに3つのメッセージストアがある場合、ミニポートドライバーはそれらすべてをまとめて処理し、サービスに1つのメッセージストアとして表示する必要があります。

MB ドライバーモデルでは、次の SMS 操作がサポートされています。

-   SMS 構成

-   SMS の読み取り

-   SMS の送信

-   SMS の削除

ミニポートドライバーは、SMS の構成、読み取り、送信、および削除の各操作をサポートすると共に、デバイスによって受信された新しい SMS メッセージをユーザーに通知することをお勧めします。

SMS 操作の詳細については、「Oid\_WWAN」を参照してください。 [\_sms\_構成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-configuration)、 [oid\_WWAN\_sms\_読み取り](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-read)、 [oid\_wwan\_sms\_送信](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-send)、 [Oid\_wwan\_sms\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-delete)、 [oid\_wwan\_SMS\_の状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-status)。

 

 





