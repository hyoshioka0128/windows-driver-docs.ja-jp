---
title: ドライバー スタック管理
description: ドライバー スタック管理
ms.assetid: 61d17e92-a1bf-42d9-b241-400b43b0ec0a
keywords:
- ドライバー スタックの WDK ネットワーク、管理します。
- ミニポート アダプタの WDK ネットワー キング、ドライバー スタック
- ミニポート ドライバー WDK ネットワー キング、ミニポート アダプター
- NDIS ミニポート ドライバー WDK、ミニポート アダプター
- プロトコル バインド WDK ネットワーク
- プロトコル ドライバー WDK net
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49fe5bd1e91088a1f61d86930d0c426f58dac966
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372666"
---
# <a name="driver-stack-management"></a>ドライバー スタック管理





NDIS 6.0 には、一時停止してドライバー スタックを再開する機能が導入されました。 NDIS 6.0 では、stack 管理の機能をサポートするには、従来のドライバーを書き換える必要があります。

NDIS 6.0 には、NDIS フィルター ドライバーも導入されました。 フィルター ドライバーは、監視し、プロトコルおよびミニポートのドライバーの間の相互作用を変更できます。 フィルター ドライバーは、簡単に実装して、少ない処理 NDIS 5 よりもオーバーヘッドがあります。*x*中級レベルのドライバーです。 これらの理由から、中間のフィルター ドライバーではなくフィルター ドライバーを使用する必要があります。

ドライバー スタックには、次の論理要素が含まれています。

<a href="" id="miniport-adapter"></a>ミニポート アダプタ  
A*ミニポート アダプター* NDIS ミニポート ドライバーまたは中間ドライバーのアダプター インスタンスです。 中間のドライバーの仮想ミニポート、ミニポート アダプターです。 NDIS は、デバイスが使用可能なになった後に、ミニポート アダプタ上でドライバー スタックの他の要素を構成します。

<a href="" id="protocol-binding"></a>プロトコルのバインド  
A*プロトコル バインド*プロトコル ドライバーのバインディング インスタンスします。 プロトコル バインドでは、NDIS プロトコル ドライバーをミニポート アダプターにバインドします。 複数のプロトコル ドライバーは、ミニポート アダプターにバインドできます。

<a href="" id="filter-module"></a>モジュールをフィルター処理します。  
A*フィルター モジュール*フィルター ドライバーのインスタンスです。 NDIS は、挿入、削除、またはフィルター モジュールを再構成するドライバー スタックを一時停止できます。 フィルター モジュールでは、監視でき、ミニポート アダプターの動作を変更することができます。

ドライバー スタック、ドライバーの状態、およびドライバー スタック操作の詳細については、以下のトピックです。

-   [NDIS ドライバー スタック](ndis-driver-stack.md)
-   [ミニポート ドライバーのアダプターの状態](adapter-states-of-a-miniport-driver.md)
-   [バインディング プロトコル ドライバーの状態](binding-states-of-a-protocol-driver.md)
-   [フィルター ドライバーのモジュール状態](module-states-of-a-filter-driver.md)
-   [NDIS スタック操作](ndis-stack-operations.md)

## <a name="related-topics"></a>関連トピック


[NDIS フィルター ドライバー](ndis-filter-drivers.md)

[NDIS 中間ドライバ](ndis-intermediate-drivers.md)

 

 






