---
title: NDIS ネットワーク インターフェイス
description: NDIS ネットワーク インターフェイス
ms.assetid: a1d062d4-3d4b-4244-b851-667d708810db
keywords:
- NDIS WDK、ネットワーク インターフェイス
- WDK の NDIS ネットワーク インターフェイス
- WDK のネットワーク インターフェイス
- ネットワーク NDISIF WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac4c312b31feb1872a999fc43a2c5245f142c1cd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378296"
---
# <a name="ndis-network-interfaces"></a>NDIS ネットワーク インターフェイス





管理情報ベース (MIB) をサポートするためには、NDIS は、ローカル コンピューターのネットワーク インターフェイスの情報のコレクションを管理します。 NDIS インターフェイス プロバイダーでは、NDIS をいくつかのネットワーク インターフェイスに関する情報を提供します。 インターフェイスを登録するインターフェイスのプロバイダーのプロキシを提供する NDIS およびハンドル ミニポート アダプター プロバイダーの要求をインターフェイスしモジュールをフィルター処理します。 そのため、ネットワーク インターフェイスのプロバイダーを使用する NDIS ドライバーは必要ありません。

ただし、NDIS ネットワーク ドライバーのすべての型は、インターフェイスのプロバイダーとして登録できます。 このようなドライバーは、ネットワーク インターフェイスを登録し、インターフェイスの OID 要求に応答するコールバック関数を提供します。 NDIS インターフェイス プロバイダーは、通常は NDIS に直接アクセスできないと、NDIS プロキシ インターフェイス プロバイダーでサポートされていないインターフェイスに関する情報を提供します。 たとえば、MUX 中間ドライバーでは、仮想ミニポートと基になるアダプターの間の内部インターフェイスことができます。

このセクションの内容:

[NDIS ネットワーク インターフェイスの概要](overview-of-ndis-network-interfaces.md)

[インターフェイスをプロバイダーとして登録します。](registering-as-an-interface-provider.md)

[NDIS ネットワーク インターフェイスの管理](managing-ndis-network-interfaces.md)

[OID のクエリを行い、NDIS インターフェイス プロバイダーのセット要求を処理します。](handling-oid-query-and-set-requests-in-an-ndis-interface-provider.md)

[NDIS Oid に NDIS ネットワーク インターフェイスのマッピング](mapping-of-ndis-network-interfaces-to-ndis-oids.md)

 

 





