---
title: RPC のデバッグの概要
description: RPC のデバッグの概要
ms.assetid: 21db61fe-a4a1-45d3-9026-f58aecd3a3bc
keywords:
- RPC デバッグの概要
- リモート プロシージャ コール (RPC)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b9632cb274dcc8b2658c111e31e883f30dce57c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580104"
---
# <a name="overview-of-rpc-debugging"></a>RPC のデバッグの概要


## <span id="ddk_overview_of_rpc_debugging_dbg"></span><span id="DDK_OVERVIEW_OF_RPC_DEBUGGING_DBG"></span>


Microsoft リモート プロシージャ コール (RPC) を簡単にプロセスやコンピューターの境界を越えるし、データを実行します。 このネットワーク プログラミング標準では、Microsoft Windows を使用したネットワークが非常に強力な理由の 1 つです。

ただし、RPC に個別のプロセスからのネットワーク呼び出しが非表示にするためのコンピューター間の相互作用の詳細わかりにくきます。 これは、ため、困難にする理由のスレッドの実行を行っている--、確認または、すべきは何を行うに失敗することができます。 その結果、デバッグとトラブルシューティングの RPC エラー困難になります。 さらに、RPC エラーのように表示される問題の大半は、実際に構成の問題、またはネットワーク接続の問題、またはその他のコンポーネントの問題です。

デバッグ ツールの Windows には、デバッガーのも、RPC に関連する拡張機能としてさせるためをという名前のツールが含まれます。 これらは、以降のバージョンの Windows および Windows XP で RPC の問題のさまざまな分析に使用できます。

これらの Windows バージョンは、RPC ランタイム状態情報の保存を構成できます。 異なる量の状態情報を保存できます。これにより、コンピューターには大きな負担をかけることがなく必要な情報を取得することができます。 参照してください[RPC 状態情報を有効にする](enabling-rpc-state-information.md)詳細についてはします。

この情報は、デバッガーまたはさせるためのツールを通じてアクセスできます。 各ケースでは、クエリのコレクションは使用できます。 参照してください[RPC 状態情報を表示する](displaying-rpc-state-information.md)詳細についてはします。

多くの場合で説明されたテクニックを使用して問題をトラブルシューティングできます[RPC の一般的なデバッグ手法](common-rpc-debugging-techniques.md)します。

参照してください、状態情報の分析のための独自の手法を検討する場合、この情報の格納方法のしくみを確認する場合または[RPC 状態情報の内部](rpc-state-information-internals.md)します。

これらのツールと手法は、Windows 2000 では機能しません。

 

 





