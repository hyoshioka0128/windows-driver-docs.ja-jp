---
title: Hyper-V 拡張可能スイッチ OID 要求
description: Hyper-V 拡張可能スイッチ OID 要求
ms.assetid: 0B6D1628-DD83-4EA6-B5D5-33D74AD45EFD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 447a4aaf2898c9f089067f3d43c8b4b20eaf1529
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349547"
---
# <a name="hyper-v-extensible-switch-oid-requests"></a>Hyper-V 拡張可能スイッチ OID 要求


HYPER-V 拡張可能スイッチのインターフェイスには、次の方法で使用されるオブジェクト識別子 (OID) 要求が含まれています。

-   拡張可能スイッチの現在の構成を照会する拡張可能スイッチ拡張機能によって発行される OID に要求します。 フィルター ドライバーなど (とも呼ばれる、 *HYPER-V 拡張可能スイッチの拡張機能*) の OID クエリ要求を発行できます[OID\_スイッチ\_NIC\_配列](https://msdn.microsoft.com/library/windows/hardware/hh598261)に配列を取得します。 配列内の各要素には、拡張可能スイッチ ポートに関連付けられているネットワーク アダプターの構成パラメーターを指定します。

    詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチの構成を照会](querying-the-hyper-v-extensible-switch-configuration.md)します。

-   OID は、拡張可能スイッチの構成の変更点について、基になる拡張機能を通知する拡張可能スイッチのインターフェイスによって発行される要求します。 拡張可能スイッチのプロトコルの端での OID セット要求を発行するなど、 [OID\_切り替える\_ポート\_作成](https://msdn.microsoft.com/library/windows/hardware/hh598272)に拡張可能スイッチのポートの作成に関する拡張機能を通知します。

    詳細については、次を参照してください。 [Hyper-v 拡張可能スイッチ構成の変更に関する OID 要求を受信](receiving-oid-requests-about-hyper-v-extensible-switch-configuration-changes.md)します。

-   OID は、拡張機能を拡張可能スイッチのインターフェイスで拡張可能スイッチ コントロールのパス経由で転送される HYPER-V 子パーティションを要求します。 これにより、パーティションで使用されているネットワーク インターフェイスに関する構成情報を取得する拡張機能です。

    機能拡張インターフェイスで拡張可能スイッチのプロトコルのエッジがの OID セット要求を転送するなど、 [OID\_802\_3\_追加\_マルチキャスト\_アドレス](https://msdn.microsoft.com/library/windows/hardware/ff569068)、子パーティションを拡張可能スイッチの管理パスから。 これにより、そのパーティション内のネットワーク インターフェイスで使用されるマルチキャスト アドレス構成を取得する拡張機能です。

    詳細については、次を参照してください。 [Hyper-v 子パーティションから OID の要求を転送](forwarding-oid-requests-from-a-hyper-v-child-partition.md)します。

拡張機能と NDIS フィルター ドライバーの詳細については、OID 要求を処理しを参照してください[フィルター モジュールの OID 要求](filter-module-oid-requests.md)します。

 

 





