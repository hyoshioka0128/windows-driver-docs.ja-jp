---
title: NDIS ネットワークインターフェイスの概要
description: NDIS ネットワークインターフェイスの概要
ms.assetid: a1d062d4-3d4b-4244-b851-667d708810db
keywords:
- NDIS WDK、ネットワークインターフェイス
- NDIS ネットワークインターフェイス WDK
- ネットワークインターフェイス WDK
- NDISIF WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68388b8b41bb44897cdb193f6afefa9c243a9451
ms.sourcegitcommit: fec48fa5342d9cd4cd5ccc16aaa06e7c3d730112
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/17/2019
ms.locfileid: "69565748"
---
# <a name="introduction-to-ndis-network-interfaces"></a>NDIS ネットワークインターフェイスの概要

管理情報ベース (MIB) をサポートするために、NDIS はローカルコンピューターのネットワークインターフェイス情報のコレクションを管理します。 NDIS インターフェイスプロバイダーは、NDIS にいくつかのネットワークインターフェイスに関する情報を提供します。 NDIS には、インターフェイスを登録し、ミニポートアダプターおよびフィルターモジュールに対するインターフェイスプロバイダー要求を処理するプロキシインターフェイスプロバイダーが用意されています。 そのため、ネットワークインターフェイスプロバイダーとして NDIS ドライバーは必要ありません。

ただし、すべての NDIS ネットワークドライバーの種類は、インターフェイスプロバイダーとして登録できます。 このようなドライバーは、ネットワークインターフェイスを登録し、インターフェイス OID 要求に応答するコールバック関数を提供します。 Ndis インターフェイスプロバイダーは、通常、NDIS に直接アクセスできず、NDIS プロキシインターフェイスプロバイダーでサポートされていないインターフェイスに関する情報を提供します。 たとえば、MUX 中間ドライバーは、その仮想ミニポートと基になるアダプターの間に内部インターフェイスを持つことができます。

このセクションの内容:

[NDIS ネットワークインターフェイスの概要](overview-of-ndis-network-interfaces.md)

[インターフェイスプロバイダーとして登録する](registering-as-an-interface-provider.md)

[NDIS ネットワークインターフェイスの管理](managing-ndis-network-interfaces.md)

[NDIS インターフェイスプロバイダーでの OID クエリおよび Set 要求の処理](handling-oid-query-and-set-requests-in-an-ndis-interface-provider.md)

[Ndis ネットワークインターフェイスから NDIS Oid へのマッピング](mapping-of-ndis-network-interfaces-to-ndis-oids.md)

 

 





