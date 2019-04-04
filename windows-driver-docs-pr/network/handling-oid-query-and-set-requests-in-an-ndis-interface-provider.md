---
title: NDIS インターフェイス プロバイダーでの OID クエリおよび設定要求の処理
description: NDIS インターフェイス プロバイダーでの OID クエリおよび設定要求の処理
ms.assetid: 9ce51fc8-426f-4d36-8ee7-0a93b7b8439c
keywords:
- NDIS ネットワーク インターフェイス、WDK インターフェイス プロバイダー
- ネットワーク インターフェイス、WDK インターフェイス プロバイダー
- インターフェイス プロバイダー WDk のネットワーク インターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 75832430bcdff619985f577b6e59fa5b632149e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573340"
---
# <a name="handling-oid-query-and-set-requests-in-an-ndis-interface-provider"></a>NDIS インターフェイス プロバイダーでの OID クエリおよび設定要求の処理





NDISIF インターフェイスは、クエリを実行または RFC 2863 内の情報に対応する設定が可能な (統計カウンターを含む) 複数のインターフェイス パラメーターを定義します。 NDIS エントリでこれらのインターフェイスのパラメーターにアクセスする呼び出し時にインターフェイス プロバイダーを定義するポイント、 [ **NdisIfRegisterProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff562716)関数。 インターフェイスをプロバイダーとして登録の詳細については、[インターフェイス プロバイダーとして登録](registering-as-an-interface-provider.md)を参照してください。

インターフェイスのパラメーターは、オブジェクト識別子 (Oid) によって識別されます。 いくつかの Oid は、インターフェイスのプロバイダーに固有です。

次のトピックでは、クエリを処理し、要求インターフェイスのパラメーターを設定する方法について説明します。

[インターフェイス オブジェクト クエリ要求の処理](handling-an-interface-object-query-request.md)

[要求の設定、インターフェイス オブジェクトの処理](handling-an-interface-object-set-request.md)

 

 





