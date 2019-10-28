---
title: 自動構成の詳細
description: 自動構成の詳細
ms.assetid: ba596ce3-724d-45c4-85ee-2486a31a0c01
keywords:
- 自動構成 WDK プリンター、プリンターの自動構成について
- プリンター自動構成 WDK プリンター、プリンターの自動構成について
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78bd1b12e397d89d7a8a2b43cf6216a27b02e365
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842760"
---
# <a name="autoconfiguration-details"></a>自動構成の詳細


自動構成は、印刷サブシステムとプリンター間で双方向のプリンター通信 (bidi 通信とも呼ばれます) を使用して機能します。 自動構成を機能させるには、プリンターが次の操作を実行できる必要があります。

-   ポートモニターによって送信されたクエリについて理解します。

-   クエリに対する適切な応答を生成します。

自動構成をサポートするには、プリンタドライバとポートモニタの両方を変更する必要があります。

プリンタドライバには次のものが必要です。

-   Bidi 通知スキーマに注意してください。

-   Bidi 通知スキーマを使用して、デバイス構成の変更に関する通知を受信できるようにします。

-   [Bidi 通信インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_print/index)、特に IBidiSpl2 COM インターフェイスを使用して、プリンターから構成データを送信することができます。

ポートモニターは次のことを行う必要があります。

-   プリンターの構成に対してクエリを実行できるデバイスプロトコルをサポートします。

-   プリンターから、要請されていないステータスメッセージを受信できるようにします。

-   要求されていないステータスメッセージを適切なドライバー通知に変換します。

-   ポーリングまたはアラートによって、デバイスの状態と構成データをすべて最新の状態に保ちます。

-   デバイスの構成変更をドライバーまたはアプリケーションに通知します。

自動構成は Windows Vista でサポートされています。 ただし、ポイントアンドプリントを使用する構成では、サーバー上のポートモニターとクライアント上のドライバーは、両方とも bidi 通信に対応している必要があります。

このセクションでは、次のトピックについて説明します。

[デバイスのインストール中の自動構成](autoconfiguration-during-device-installation.md)

[構成の変更時の自動構成](autoconfiguration-during-configuration-change.md)

 

 




