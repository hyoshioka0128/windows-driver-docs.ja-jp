---
title: Windows Me および Windows XP の WIA スキャナー項目ツリー レイアウト
description: Windows Me および Windows XP の WIA スキャナー項目ツリー レイアウト
ms.assetid: e4824d3a-6439-4ebb-903e-2b592108ddbe
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20a8304abdd39e939dd001c0ad8528d37e828f64
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840670"
---
# <a name="wia-scanner-item-tree-layout-for-windows-xp"></a>Windows XP 用 WIA スキャナー項目ツリーのレイアウト


Windows XP の WIA スキャナー項目ツリーは、ルート項目と1つの子項目で構成されています。 次の図は、WIA スキャナーの項目ツリーを示しています。

![wia スキャナーの項目ツリーを示す図](images/scanner-tree.png)

項目ツリーを作成する方法の例については、「[アプリケーションで WIA デバイスを作成する方法](how-the-application-creates-the-wia-device.md)」を参照してください。 詳細については、「wia[ミニドライバーの初期化](initializing-the-wia-minidriver.md)」、「 [wia ドライバーサービスライブラリ](wia-driver-services-library.md)での**項目ツリーの構築と保守**」、および「 [**IWiaMiniDrv::d rvinitializewia**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)」を参照してください。 スキャナー項目ツリーのルート項目には、すべての WIA ミニドライバーに存在する情報と、スキャナー固有のプロパティが含まれています。 スキャナー固有のプロパティには、デバイスの光学情報とドキュメントフィーダーのサポートが含まれます。

子項目は、デバイスのデータ収集機能を表し、データの転送に使用されます。 スキャナーの子項目には、実行できる操作を反映する名前を付ける必要があります。

Microsoft では、Windows XP に次の名前が必要です。

**ルート**  
WIA 項目ツリー内の最初の要素を表す項目。

**ベッド**  
ドキュメントフィーダーの有無にかかわらず、フラットベッドスキャナーを表す項目。

**フィーダー**  
ドキュメントフィーダーのみを備えたスキャナーを表す項目。

Windows Me と Windows XP の場合、アプリケーションは、ルート項目と最初の子項目の WIA プロパティを読み取って、スキャナーデバイスの機能を判別できるようにする必要があります。

アプリケーションでは、次の操作を実行するために、WIA サービスを使用できます。

-   クエリスキャナー機能。

-   スキャナーデバイスのプロパティを設定します。

-   データ転送を要求します。

通常、アプリケーションは、ルート項目と単一の子項目の2つの項目によって表される、自動ドキュメントフィーダー (ADFs) を含むフラットベッドスキャナーを想定しています。 すべてのデータ転送は、子項目から実行されます。
