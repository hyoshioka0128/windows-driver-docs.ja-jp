---
title: 自動構成の詳細
description: 自動構成の詳細
ms.assetid: ba596ce3-724d-45c4-85ee-2486a31a0c01
keywords:
- 自動構成の WDK プリンター、プリンターの自動構成について
- プリンターの自動構成 WDK プリンター、プリンターの自動構成について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70c4a6cd3d6756bbdf429389e273b98a9f6d98ae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370490"
---
# <a name="autoconfiguration-details"></a>自動構成の詳細


自動構成は、印刷サブシステムとプリンターの間の双方向プリンター通信 (双方向の通信とも呼ばれます) によって動作します。 作業を自動構成は、プリンターができる必要があります。

-   ポート モニターによって送信されるクエリを理解します。

-   クエリに適切な応答を生成します。

自動構成をサポートするために、プリンター ドライバーと、ポート モニターの両方を変更する必要があります。

プリンター ドライバーが必要です。

-   双方向の通知スキーマを把握します。

-   双方向の通知スキーマを使用してデバイス構成の変更に関する通知を受信できるようにします。

-   使用してプリンターから構成データを集めることができる、[双方向の通信インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_print/index)、および IBidiSpl2 COM インターフェイスでは具体的には。

ポート モニターにする必要があります。

-   プリンターの構成のクエリを実行できるデバイス プロトコルをサポートします。

-   プリンターから要請されていない状態のメッセージを受信できるようにします。

-   要請されていないステータス メッセージを適切なドライバーの通知に変換します。

-   すべてのデバイスの状態と構成データをポーリングやアラートを使用して最新に保つには。

-   ドライバーまたはデバイスの構成の変更のアプリケーションに通知します。

自動構成は、Windows Vista でサポートされます。 ただし、ポイント アンド プリントを使って構成で、サーバー上のポート モニターと、クライアント上のドライバーもなりません双方向通信が可能。

このセクションでは、次のトピックについて説明します。

[デバイスのインストール中に自動構成](autoconfiguration-during-device-installation.md)

[構成の変更中に自動構成](autoconfiguration-during-configuration-change.md)

 

 




