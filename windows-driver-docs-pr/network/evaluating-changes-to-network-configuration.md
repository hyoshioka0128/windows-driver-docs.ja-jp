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
ms.openlocfilehash: c27a027f8bb286f3c9b8e8f8b3b0cd289d3d65fe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353777"
---
# <a name="evaluating-changes-to-network-configuration"></a>ネットワーク構成の変更の評価





通知オブジェクトのメソッドを呼び出して、サブシステム、ネットワークの構成後に[ **INetCfgComponentNotifyGlobal** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547733(v=vs.85))と[INetCfgComponentNotifyBinding](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff547730(v=vs.85))インターフェイス、通知オブジェクトは、サブシステムを送信するネットワーク構成で提案された変更を評価する必要があり、変更に関連する操作を実行する必要があります。 通知オブジェクトのメソッド**INetCfgComponentNotifyGlobal**と**INetCfgComponentNotifyBinding**を所有するコンポーネントに影響する変更のみを処理するインターフェイスを実装する必要がありますオブジェクト。

次のトピックでは、通知オブジェクトがネットワークの構成に対する変更を処理する方法の例について説明します。

[コンポーネントを追加します。](adding-a-component.md)

[コンポーネントのバインドを変更します。](changing-bindings-for-a-component.md)

 

 





