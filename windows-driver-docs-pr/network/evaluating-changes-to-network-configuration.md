---
title: ネットワーク構成の変更の評価
description: ネットワーク構成の変更の評価
ms.assetid: 7e73fbb4-8d7d-44fb-96c9-aa748c207553
keywords:
- オブジェクトの WDK ネットワークへの通知、変更処理
- ネットワーク WDK のオブジェクトへの通知、変更処理
- ネットワーク構成 WDK への変更
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 742ebfb2c94a8251845416b4bfa6455be670b0dd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368300"
---
# <a name="evaluating-changes-to-network-configuration"></a>ネットワーク構成の変更の評価





通知オブジェクトのメソッドを呼び出して、サブシステム、ネットワークの構成後に[ **INetCfgComponentNotifyGlobal** ](https://msdn.microsoft.com/library/windows/hardware/ff547733)と[INetCfgComponentNotifyBinding](https://msdn.microsoft.com/library/windows/hardware/ff547730)インターフェイス、通知オブジェクトは、サブシステムを送信するネットワーク構成で提案された変更を評価する必要があり、変更に関連する操作を実行する必要があります。 通知オブジェクトのメソッド**INetCfgComponentNotifyGlobal**と**INetCfgComponentNotifyBinding**を所有するコンポーネントに影響する変更のみを処理するインターフェイスを実装する必要がありますオブジェクト。

次のトピックでは、通知オブジェクトがネットワークの構成に対する変更を処理する方法の例について説明します。

[コンポーネントを追加します。](adding-a-component.md)

[コンポーネントのバインドを変更します。](changing-bindings-for-a-component.md)

 

 





