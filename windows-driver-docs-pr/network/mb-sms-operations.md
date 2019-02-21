---
title: SMS の操作の MB
description: SMS の操作の MB
ms.assetid: 9a21495c-ec3d-4277-b880-dbf5b081814a
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9afc71d278c03252a49703f8f81422a56f2d16d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538266"
---
# <a name="mb-sms-operations"></a>SMS の操作の MB


このトピックでは、構成、読み取り/受信、送信、および MB デバイスのショート メッセージ サービス (SMS) 機能を使用してメッセージを削除する操作について説明します。

SMS のサポートは必須です。 ミニポート ドライバーが適切な送信設定し、処理するときにサポートされる SMS 機能フラグを受け取る必要があります[OID\_WWAN\_デバイス\_CAP](https://msdn.microsoft.com/library/windows/hardware/ff569824)クエリで要求、 **WwanSmsCaps**のメンバー、 [ **WWAN\_デバイス\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff571204)構造体。 ミニポート ドライバーは SMS をサポートしていない場合は WWAN を指定する必要があります\_SMS\_CAP\_NONE 戻って WWAN\_状態\_SMS\_不明な\_SMS に関連するすべての Oid のエラー。

ミニポート ドライバーは、SMS の操作の後にのみ処理する必要があります[OID\_WWAN\_準備\_情報](https://msdn.microsoft.com/library/windows/hardware/ff569833)返します**WwanReadyStateInitialize**デバイスの準備完了状態として。 ミニポート ドライバーでは、(ただし、必ずしもデータ サービスの登録) プロバイダーのネットワーク上のデバイスの登録後にのみ、SMS メッセージの送信など、一部の SMS 操作を処理する必要があります。

MB サービスは、デバイスで利用できるさまざまなメッセージ ストアで違いはありません。 したがって、ミニポート ドライバーはすべてのメッセージ ストアを処理し、プロジェクトの 1 つの仮想メッセージ ストアが仮想のインデックスを使用してアクセスする必要があります。 たとえば、デバイスに 3 つのメッセージ ストアがある場合は、ミニポート ドライバーする必要がありますそれらすべてをまとめて処理し、1 つのメッセージとして、サービスへのストア。

MB ドライバー モデルには、次の SMS 操作がサポートされています。

-   SMS の構成

-   SMS の読み取り

-   SMS を送信します。

-   SMS を削除します。

ミニポート ドライバー SMS 構成をサポートして、読み取り、送信、および新しい SMS メッセージを受信デバイスでのユーザーに通知するほか、操作を削除することをお勧めします。

SMS の操作の詳細については、次を参照してください[OID\_WWAN\_SMS\_構成](https://msdn.microsoft.com/library/windows/hardware/ff569837)、 [OID\_WWAN\_SMS\_読み取り。](https://msdn.microsoft.com/library/windows/hardware/ff569839)、 [OID\_WWAN\_SMS\_送信](https://msdn.microsoft.com/library/windows/hardware/ff569840)、 [OID\_WWAN\_SMS\_削除](https://msdn.microsoft.com/library/windows/hardware/ff569838)、および[OID\_WWAN\_SMS\_状態](https://msdn.microsoft.com/library/windows/hardware/ff569841)します。

 

 





