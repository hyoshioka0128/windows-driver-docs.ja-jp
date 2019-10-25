---
title: NDIS インターフェイス プロバイダーでの OID クエリおよび設定要求の処理
description: NDIS インターフェイス プロバイダーでの OID クエリおよび設定要求の処理
ms.assetid: 9ce51fc8-426f-4d36-8ee7-0a93b7b8439c
keywords:
- NDIS ネットワークインターフェイス WDK、インターフェイスプロバイダー
- ネットワークインターフェイス WDK、インターフェイスプロバイダー
- インターフェイスプロバイダーの WDk ネットワークインターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97a517111c9f25105ae97a5c3aeecf1fda78b4e8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842576"
---
# <a name="handling-oid-query-and-set-requests-in-an-ndis-interface-provider"></a>NDIS インターフェイス プロバイダーでの OID クエリおよび設定要求の処理





NDISIF インターフェイスは、RFC 2863 の情報に対応するクエリまたは設定が可能な、いくつかのインターフェイスパラメーター (統計カウンターを含む) を定義します。 NDIS は、 [**NdisIfRegisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterprovider)関数を呼び出すときにインターフェイスプロバイダーによって定義されるエントリポイントを介して、これらのインターフェイスパラメーターにアクセスします。 をインターフェイスプロバイダーとして登録する方法の詳細については、「[インターフェイスプロバイダーとし](registering-as-an-interface-provider.md)ての登録」を参照してください。

インターフェイスパラメーターは、オブジェクト識別子 (Oid) によって識別されます。 一部の Oid は、インターフェイスプロバイダーに固有のものです。

次のトピックでは、インターフェイスパラメーターのクエリと set 要求を処理する方法について説明します。

[インターフェイスオブジェクトクエリ要求の処理](handling-an-interface-object-query-request.md)

[インターフェイスオブジェクトセットの要求の処理](handling-an-interface-object-set-request.md)

 

 





