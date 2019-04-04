---
title: コール マネージャーによって実行される接続指向操作
description: コール マネージャーによって実行される接続指向操作
ms.assetid: 6df23eb2-df02-4d24-88b3-c02b87edb38b
keywords:
- 接続指向 NDIS WDK、コール マネージャー
- いる CoNDIS WDK、ネットワー キング コール マネージャー
- マネージャーの WDK は、ネットワーク接続指向の操作を呼び出す
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7025de9d07fc53fbeacbb66112366389992b8e2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572221"
---
# <a name="connection-oriented-operations-performed-by-call-managers"></a>コール マネージャーによって実行される接続指向操作





コール マネージャーを実行します。

-   **登録し、1 つまたは複数のアドレス ファミリ (AFs) の登録を解除します。**

    コール マネージャー [1 つまたは複数のアドレス ファミリを登録します](registering-and-opening-an-address-family.md)NDIS にします。 アドレス ファミリを登録することでは、コール マネージャーは、クライアントの接続指向のバインドのコール マネージャー (具体的には、シグナリング プロトコル) サービスをアドバタイズします。 NDIS にエントリ ポイントを登録する方法の詳細については、[いる CoNDIS 登録](condis-registration.md)を参照してください。

-   **登録し、接続指向のクライアントの要求での Sap の登録を解除します。**

    コール マネージャーは、バインドされた接続指向クライアントの要求を受信[SAPs を登録](registering-a-sap.md)と[SAPs を登録解除](deregistering-a-sap.md)します。 コール マネージャーは、クライアントに代わって SAPs を登録または登録解除をネットワーク経由でのシグナリング メッセージを送信します。

-   **接続指向のクライアントの要求で発信呼び出しを設定します。**

    クライアントが接続指向ときに[発信呼び出しを行う](making-a-call.md)、コール マネージャーは、接続を作成するのには、必要に応じてコントロールのネットワーク デバイスと (シグナリング メッセージの交換) を通信します。 呼び出しはコール マネージャー、リモート側によって受け入れられます[VC をアクティブに](activating-a-vc.md)呼び出し用に作成されます。

-   **設定し、接続指向のクライアントに着信呼び出しを示します。**

    コール マネージャーは、バインドされた接続指向のクライアントにクライアントが登録されている SAP 宛てのすべての呼び出しを示します。 前に[着信呼び出しを示す](indicating-an-incoming-call.md)コール マネージャーを開始する、クライアント[VC の作成](creating-a-vc.md)の呼び出しを開始し、 [VC のアクティブ化](activating-a-vc.md)。

-   **Qos の変更要求を通信します。**

    コール マネージャーが通信できる信号のプロトコルによって、[ローカル クライアントからの要求を送信または受信呼び出しの QoS を変更する](client-initiated-request-to-change-call-parameters.md)または[呼び出しQoSを変更するリモートパーティからの要求](incoming-request-to-change-call-parameters.md).

-   **要求を追加および削除の当事者に伝えます。**

    コール マネージャーへのローカル クライアントの要求の通信[パーティの追加](adding-a-party-to-a-multipoint-call.md)にまたは[パーティにドロップ](dropping-a-party-from-a-multipoint-call.md)ポイント ツー マルチポイント呼び出しから。 コール マネージャー、リモート パーティは、通信も[受信要求、ポイント ツー マルチポイント呼び出しから自体を削除する](incoming-request-to-drop-a-party-from-a-multipoint-call.md)します。

-   **呼び出しを涙します。**

    接続指向のクライアントの要求、コール マネージャーがネットワークにデバイスの制御と通信して呼び出しを閉じます[接続終了](client-initiated-request-to-close-a-call.md)します。 リモート パーティの要求、コール マネージャーを示します接続指向のローカル クライアントに、リモート パーティの[の呼び出しを閉じる要求](incoming-request-to-close-a-call.md)します。 呼び出し、コール マネージャーの破棄中[VC を非アクティブ化](deactivating-a-vc.md)呼び出しに使用されます。 コール マネージャーこともできます (着信) の VC を作成して、コール マネージャー場合[削除 VC](deleting-a-vc.md)します。

-   **クエリまたは情報を設定します。**

    コール マネージャーできます[情報の照会または](querying-or-setting-information.md)接続指向のバインドされているクライアントによって管理されます。 コール マネージャーは、クエリし、バインドされた接続指向のクライアントからの設定操作にも応答できます。

    さらに、コール マネージャーはクエリか、または連結 MCM ドライバーのミニポート ドライバー部分によってバインドされているミニポート ドライバーによって管理されている情報を設定できます。

-   **Inputsminiport ドライバーの状態のインジケーター。**

    呼び出しの manager 入力[バインドされた接続指向のミニポート ドライバーからの状態インジケーター](indicating-miniport-driver-status.md)します。

 

 





