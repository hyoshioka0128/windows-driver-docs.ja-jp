---
title: クライアントによって実行される接続指向操作
description: クライアントによって実行される接続指向操作
ms.assetid: 342f534e-d203-4823-a4d8-a8a51b7ff0bd
keywords:
- クライアントの接続指向 WDK
- クライアントの操作を WDK いる CoNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51f6d6b0820d31deb0a1ef0594c96634e90428f8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374958"
---
# <a name="connection-oriented-operations-performed-by-clients"></a>クライアントによって実行される接続指向操作





接続指向のクライアント:

-   **開き、アドレス ファミリを閉じます。**

    接続指向のドライバーができる、コール マネージャーまたは MCM ドライバーは、アドレス ファミリで登録が NDIS から通知を受け取る[そのアドレス ファミリを開く](registering-and-opening-an-address-family.md)呼び出し manager または MCM のドライバーを使用します。 クライアントは、コール マネージャーまたは MCM ドライバーによって提供されるコール マネージャー サービスを使用できます。 クライアントと自体、コール マネージャーまたはで MCM ドライバーの間の関連付けを解放する[アドレス ファミリを閉じる](closing-an-address-family.md)します。

-   **登録し、SAPs の登録を解除します。**

    接続指向のクライアントができるコール マネージャーまたは MCM ドライバーでは、アドレス ファミリを開いたら、 [SAPs の 1 つまたは複数の登録](registering-a-sap.md)コール マネージャーまたは MCM ドライバーにします。 コール マネージャーまたは MCM ドライバーしは、クライアントに登録済みの SAPs 宛ての着信呼び出し。 クライアントのリリースで、SAP [、SAP の登録を解除](deregistering-a-sap.md)します。

-   **追加し、Pvc を削除します。**

    ときに、演算子を手動で構成または永続的な VC (PVC) では、接続指向のクライアントを監視できます。 このようなアクションに応答してで、クライアントを PVC を構成済み Pvc の一覧に追加したり、PVC をこの一覧から削除するコール マネージャーまたは MCM ドライバー要求できます (を参照してください[OID\_CO\_追加\_PVC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-add-pvc)と[OID\_CO\_削除\_PVC](https://docs.microsoft.com/windows-hardware/drivers/network/oid-co-delete-pvc))。

-   **発信呼び出しを使用します。**

    発信通話を行う前にクライアントを実行する必要があります、 [VC の作成](creating-a-vc.md)の呼び出し。 クライアントは、[発信通話](making-a-call.md)します。 ポイント ツー マルチポイント呼び出しをするためには、クライアントは、呼び出し時に、パーティを指定します。

-   **パーティを追加するか、ポイント ツー マルチポイント呼び出しからパーティを削除します。**

    クライアントは[ポイント ツー マルチポイント呼び出しにパーティの追加](adding-a-party-to-a-multipoint-call.md)と[ポイント ツー マルチポイント呼び出しからパーティを削除](dropping-a-party-from-a-multipoint-call.md)します。 クライアントは、受信メッセージに応答できるも[ポイント ツー マルチポイント呼び出しからパーティを削除する要求](incoming-request-to-drop-a-party-from-a-multipoint-call.md)します。

-   **着信呼び出しを受け入れるか拒否します。**

    クライアントは[を承認または拒否の着信通話を](indicating-an-incoming-call.md)コール マネージャーまたは MCM のドライバーに、クライアントが以前に登録される SAP に解決されます。

-   **Active の VC の呼び出しのパラメーターをネゴシエートします。**

    シグナリングのプロトコルによって許可されている内容に応じて、クライアントは、アクティブな VC の呼び出しのパラメーターをネゴシエートできます。 クライアントは[サービスの品質 (QoS) の変更を要求](client-initiated-request-to-change-call-parameters.md)active の VC の QoS を変更する着信要求に応答するとします。 クライアントは応答することも、[リモート パーティからの呼び出しの QoS の変更要求](incoming-request-to-change-call-parameters.md)します。

-   **パケットを送受信します。**

    クライアントは、接続指向のミニポート ドライバーまたは MCM ドライバーを介してパケットを送信できます。 クライアントは、接続指向のミニポート ドライバーまたは MCM ドライバーを介してパケットも受信できます。

-   **VC の削除を開始します。**

    クライアントを実行できる、 [VC の削除](deleting-a-vc.md)を作成することです。

-   **呼び出しの破棄を開始します。**

    クライアント[発信通話の終了処理を開始](client-initiated-request-to-close-a-call.md)行われたことまたは、使用できる呼び出しを受信します。

-   **クエリまたは情報を設定します。**

    クライアントでは、クエリを実行したり、バインドされた呼び出しマネージャーまたは MCM ドライバーのコール マネージャー部分によって管理されている情報を設定することができます。 クライアントは応答できるも[クエリを実行し、設定](querying-or-setting-information.md)からバインドされたコール マネージャーまたは MCM ドライバー。

    さらに、クライアントは、クエリまたはバインドされているミニポート ドライバーまたはバインドされた MCM ドライバーのミニポート ドライバー部分によって管理されている情報を設定します。

-   **Inputsminiport ドライバーの状態のインジケーター。**

    クライアントが入力できる[接続指向のミニポート ドライバーによって示される状態](indicating-miniport-driver-status.md)または MCM ドライバー。

 

 





