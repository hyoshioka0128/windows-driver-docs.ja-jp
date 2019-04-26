---
title: KSPROPSETID\_接続
description: KSPROPSETID\_接続
ms.assetid: 1be062ab-7396-4876-ab28-8a03e55df1d3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64d73eff27563ce37aad3448f888b8530b765857
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349127"
---
# <a name="kspropsetidconnection"></a>KSPROPSETID\_接続


## <span id="ddk_kspropsetid_connection_ks"></span><span id="DDK_KSPROPSETID_CONNECTION_KS"></span>


クライアントが、KSPROPSETID でプロパティを使用して\_接続プロパティを設定または確認したり、pin での接続の状態を設定します。 暗証番号 (pin) のインスタンスは、これらのプロパティを処理します。

Stream クラス ミニドライバーを処理する必要はありません[ **KSPROPERTY\_接続\_状態**](ksproperty-connection-state.md)または[ **KSPROPERTY\_接続\_PROPOSEDATAFORMAT** ](ksproperty-connection-proposedataformat.md)プロパティに直接します。 ストリーム クラス ドライバーは、ブロックを使用してストリーム要求 (SRB) クエリの詳細については必要に応じて、それを処理します。

KSPROPSETID\_接続プロパティのセットが含まれています。

[**KSPROPERTY\_接続\_ALLOCATORFRAMING**](ksproperty-connection-allocatorframing.md)

[**KSPROPERTY\_接続\_ALLOCATORFRAMING\_例**](ksproperty-connection-allocatorframing-ex.md)

[**KSPROPERTY\_接続\_ACQUIREORDERING**](ksproperty-connection-acquireordering.md)

[**KSPROPERTY\_接続\_DATAFORMAT**](ksproperty-connection-dataformat.md)

[**KSPROPERTY\_接続\_優先順位**](ksproperty-connection-priority.md)

[**KSPROPERTY\_接続\_PROPOSEDATAFORMAT**](ksproperty-connection-proposedataformat.md)

[**KSPROPERTY\_接続\_STARTAT**](ksproperty-connection-startat.md)

[**KSPROPERTY\_接続\_状態**](ksproperty-connection-state.md)

 

 





