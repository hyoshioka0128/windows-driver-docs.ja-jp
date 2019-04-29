---
title: 中間ドライバーのクエリおよび設定操作
description: 中間ドライバーのクエリおよび設定操作
ms.assetid: 68576241-20c1-4df4-ab2e-20ab89e67763
keywords:
- 中間ドライバー WDK ネットワー キング、クエリ操作
- NDIS 中間ドライバー WDK、クエリ操作
- 中間ドライバー WDK ネットワー キング、セットの操作
- NDIS ドライバー WDK、集合演算を中間します。
- クエリ操作 WDK NDIS 中間
- WDK NDIS 中間の設定操作
- Oid の WDK ネットワー キング、中間ドライバー クエリ、およびセット
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0113800dd9746a101f3a93687ffd08537978b82b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391655"
---
# <a name="intermediate-driver-query-and-set-operations"></a>中間ドライバーのクエリおよび設定操作





基になるミニポート アダプターにバインドが正常におよびその仮想ミニポートの初期化された後の中間のドライバーが基になるミニポート アダプタの運用特性を照会し、内部の状態を設定します。 必要に応じて、中間のドライバーも、基になるミニポート アダプターにバインドするための lookahead バッファー サイズとして、このようなパラメーターをネゴシエートします。 基になるミニポート アダプターに関連付けられている属性のほとんどで中間ドライバーに渡される、 *BindParameters*のパラメーター、 [ *ProtocolBindAdapterEx*](https://msdn.microsoft.com/library/windows/hardware/ff570220)関数。 中間ドライバーに渡される値を使用する必要があります*ProtocolBindAdapterEx*OID のクエリを発行するのではなく、可能な場合。 ただし、コネクションレスの下端と中間のドライバーは、呼び出すことによっての OID のクエリを発行できます[ **NdisOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff563710)します。 接続指向の下端と中間のドライバーが呼び出すことによって OID のクエリを発行できます[ **NdisCoOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561711)します。

中間のドライバーのクエリを受信して要求をより高いレベルのドライバーから設定できるもその[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)関数。 ドライバーするそれらの要求に応答か、基になるドライバーに渡したりします。 中間のドライバーがクエリとセットにどのように応答する方法は、実装によって異なります。

**注**  中間ドライバーの動作は、仮想ミニポートと基になるミニポート ドライバーの電源の状態によっても影響します。 クエリでの電源の状態の影響の詳細をセット操作では、次を参照してください。[設定 Power 要求を処理](handling-a-set-power-request.md)します。

 

ネットワークのリファレンス セクションには、および中間ドライバー開発者向けの必要なメディアに固有の Oid の nonmedia 固有の一般的な接続指向の Oid をすべてに関する情報が含まれています。

次のトピックは、発行し、クエリに応答してに関する追加情報を提供し、中間のドライバーの設定。

[発行元のセットと、中間ドライバーからのクエリ要求](issuing-set-and-query-requests-from-an-intermediate-driver.md)

[セットと、中間ドライバーでのクエリに応答して](responding-to-sets-and-queries-in-an-intermediate-driver.md)

 

 





