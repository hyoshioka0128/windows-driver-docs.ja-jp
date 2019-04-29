---
title: I2S および SCO リソースの管理
description: 管理の I2S と SCO リソースのトピックでは、Bluetooth バイパス オーディオの Windows 8.1 では、ストリーミングのサポートの設計で行われた前提条件について説明します。
ms.assetid: C6CA73D9-0DCC-496D-8306-CB1625B86AC9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d93401243ac280e5c5ff344f6f39e047fac7e3dc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332391"
---
# <a name="management-of-i2s-and-sco-resources"></a>I2S および SCO リソースの管理


管理の I2S と SCO リソースのトピックでは、Bluetooth バイパス オーディオの Windows 8.1 では、ストリーミングのサポートの設計で行われた前提条件について説明します。

Windows はこの時点で、1 つだけの Bluetooth ホスト コント ローラーがあることを前提とします。 また、接続と、HFP 同期指向 (SCO) バイパス サポートには、バイパスの 1 つだけ接続があるし、その 1 つの接続に関連付けられて、HFP デバイス ドライバー インターフェイス、任意のチャネルが開かれている、ことが前提としています。

オーディオ ドライバーは、このチャネルを判別する必要があり、1 つは最初は先着ごとに 1 つのコンシューマーの接続をバイパスします。 これを実現する最も簡単な方法は、そのピン ACQUIRE 状態を遷移する 1 つのフィルターのみを許可するドライバーです。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[操作の理論を概説します。](theory-of-operation.md)  



