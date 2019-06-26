---
title: MB SMS 操作
description: MB SMS 操作
ms.assetid: 9a21495c-ec3d-4277-b880-dbf5b081814a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4166dc22efad9b0f99b61266647ccc0343396c91
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374014"
---
# <a name="mb-sms-operations"></a>MB SMS 操作


このトピックでは、構成、読み取り/受信、送信、および MB デバイスのショート メッセージ サービス (SMS) 機能を使用してメッセージを削除する操作について説明します。

SMS のサポートは必須です。 ミニポート ドライバーが適切な送信設定し、処理するときにサポートされる SMS 機能フラグを受け取る必要があります[OID\_WWAN\_デバイス\_CAP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-caps)クエリで要求、 **WwanSmsCaps**のメンバー、 [ **WWAN\_デバイス\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_device_caps)構造体。 ミニポート ドライバーは SMS をサポートしていない場合は WWAN を指定する必要があります\_SMS\_CAP\_NONE 戻って WWAN\_状態\_SMS\_不明な\_SMS に関連するすべての Oid のエラー。

ミニポート ドライバーは、SMS の操作の後にのみ処理する必要があります[OID\_WWAN\_準備\_情報](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ready-info)返します**WwanReadyStateInitialize**デバイスの準備完了状態として。 ミニポート ドライバーでは、(ただし、必ずしもデータ サービスの登録) プロバイダーのネットワーク上のデバイスの登録後にのみ、SMS メッセージの送信など、一部の SMS 操作を処理する必要があります。

MB サービスは、デバイスで利用できるさまざまなメッセージ ストアで違いはありません。 したがって、ミニポート ドライバーはすべてのメッセージ ストアを処理し、プロジェクトの 1 つの仮想メッセージ ストアが仮想のインデックスを使用してアクセスする必要があります。 たとえば、デバイスに 3 つのメッセージ ストアがある場合は、ミニポート ドライバーする必要がありますそれらすべてをまとめて処理し、1 つのメッセージとして、サービスへのストア。

MB ドライバー モデルには、次の SMS 操作がサポートされています。

-   SMS の構成

-   SMS の読み取り

-   SMS を送信します。

-   SMS を削除します。

ミニポート ドライバー SMS 構成をサポートして、読み取り、送信、および新しい SMS メッセージを受信デバイスでのユーザーに通知するほか、操作を削除することをお勧めします。

SMS の操作の詳細については、次を参照してください[OID\_WWAN\_SMS\_構成](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-configuration)、 [OID\_WWAN\_SMS\_読み取り。](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-read)、 [OID\_WWAN\_SMS\_送信](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-send)、 [OID\_WWAN\_SMS\_削除](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-delete)、および[OID\_WWAN\_SMS\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-status)します。

 

 





