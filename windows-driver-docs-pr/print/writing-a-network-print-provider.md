---
title: ネットワーク印刷プロバイダーの作成
description: ネットワーク印刷プロバイダーの作成
ms.assetid: 9dbe8a00-6b5f-41ae-8ab5-218dcbe37833
keywords:
- 印刷スプーラーは印刷プロバイダー、WDK をカスタマイズします。
- スプーラが印刷、印刷のプロバイダーを WDK のカスタマイズ
- 印刷スプーラー コンポーネント WDK、印刷プロバイダーのカスタマイズ
- 印刷プロバイダー WDK、書き込み
- ネットワーク印刷プロバイダー WDK
- 印刷のプロバイダーの作成
- WDK のプロバイダーの印刷、ネットワークの詳細については、プリント プロバイダー
- ネットワークに関するネットワーク印刷プロバイダー WDK、印刷プロバイダー
- WDK のプロバイダーを印刷します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9de1dbf8ea7d63765c4e6e25db5d4edefa03c05
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531270"
---
# <a name="writing-a-network-print-provider"></a>ネットワーク印刷プロバイダーの作成





場合によっては、仕入先がありますを指定する、[印刷プロバイダー](print-providers.md)新しいネットワーク アーキテクチャをサポートします。 新しい印刷プロバイダーの機能を提供する方法の 1 つが置換するまったく新しい印刷プロバイダーを作成するには、[ローカル印刷プロバイダー](local-print-provider.md)します。 実際には、ただし、これは、困難でおそらく不要なタスクです。 別の方法では、ローカルの印刷プロバイダーと組み合わせて動作する部分的な印刷のプロバイダーを作成します。

このセクションでは、次のトピックでは。

[部分的な印刷プロバイダーの概要](overview-of-partial-print-providers.md)

[プリンターの変更通知のサポート](supporting-printer-change-notifications.md)

[ネットワーク印刷プロバイダーのインストール](installing-a-network-print-provider.md)

 

 




