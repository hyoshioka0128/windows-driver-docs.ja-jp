---
title: RPC 状態情報の表示
description: RPC 状態情報の表示
ms.assetid: 9931cf62-a7c2-4270-8664-a77a82207aa9
keywords:
- RPC デバッグ、RPC 状態情報を表示します。
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4391d3286be2d33b5c0843d39fb9c5047fe78171
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363927"
---
# <a name="displaying-rpc-state-information"></a>RPC 状態情報の表示


## <span id="ddk_displaying_rpc_state_information_dbg"></span><span id="DDK_DISPLAYING_RPC_STATE_INFORMATION_DBG"></span>


すべての RPC ランタイム状態情報は、セルに含まれます。 セルは、個別に更新および表示が可能な情報の最小単位です。 させるためのツールと RPC デバッガー拡張機能の両方を許可する特定の任意のセルの内容を表示したり、高度なクエリを実行します。

RPC ランタイムの各キー オブジェクトの状態に関する情報の 1 つまたは複数のセルが維持されます。 各セルはセルの ID を持つ オブジェクトは、別のオブジェクトが参照されている場合はそのオブジェクトのセルの ID を指定します。

RPC ランタイムは、に関する情報を維持できる主要なオブジェクトは、エンドポイント、スレッド、接続オブジェクト、サーバーを呼び出す (SCALL) オブジェクト、およびクライアントの呼び出し (CCALL) オブジェクト。 Server オブジェクトの呼び出しは、単と呼ばれる通常*オブジェクトを呼び出す*します。

RPC 状態情報のクエリは、同じ情報を生成させるためのツールまたは RPC デバッガー拡張機能を使用しているかどうか。 次のセクションでは、各車両でクエリを使用する方法について説明します。

[RPC デバッガー拡張機能の使用](using-the-rpc-debugger-extensions.md)

[させるためのツールを使用します。](using-the-dbgrpc-tool.md)

最も基本的なクエリには、個々 のセルだけが表示されます。

[RPC のセルの情報を取得します。](get-rpc-cell-information.md)

次の高度なクエリ サポートされています。

[RPC エンドポイント情報を取得します。](get-rpc-endpoint-information.md)

[RPC スレッド情報を取得します。](get-rpc-thread-information.md)

[RPC 呼び出し情報を取得します。](get-rpc-call-information.md)

[RPC クライアント呼び出し情報を取得します。](get-rpc-client-call-information.md)

 

 





