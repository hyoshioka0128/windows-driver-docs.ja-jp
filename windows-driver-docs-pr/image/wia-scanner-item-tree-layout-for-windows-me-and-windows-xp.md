---
title: Windows Me および Windows XP の WIA スキャナー項目ツリー レイアウト
description: Windows Me および Windows XP の WIA スキャナー項目ツリー レイアウト
ms.assetid: e4824d3a-6439-4ebb-903e-2b592108ddbe
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e26a9dc2bf6b51b0b418cca831cfe284244e86cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352667"
---
# <a name="wia-scanner-item-tree-layout-for-windows-xp"></a>Windows XP の WIA スキャナー項目ツリーのレイアウト


Windows xp で WIA スキャナーの項目のツリーは、ルート項目と 1 つの子項目で構成されます。 次の図は、WIA スキャナーの項目のツリーを示しています。

![wia スキャナーの項目のツリーを示す図](images/scanner-tree.png)

参照してください[アプリケーションは、WIA デバイスを作成する方法](how-the-application-creates-the-wia-device.md)項目ツリーを作成する方法の例についてはします。 詳細については、次を参照してください[WIA ミニドライバーの初期化](initializing-the-wia-minidriver.md)、**を構築して、項目のツリーを維持**で[WIA ドライバー サービス ライブラリ](wia-driver-services-library.md)、および[。**IWiaMiniDrv::drvInitializeWia**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvinitializewia)します。 スキャナーの項目のツリーで、ルート項目には、すべての WIA のミニドライバーとスキャナーに固有のプロパティに表示される情報が含まれています。 スキャナーに固有のプロパティには、デバイスの光の情報とドキュメント フィーダーのサポートが含まれます。

子項目は、デバイスのデータ収集機能を表し、データを転送するために使用されます。 スキャナーの子項目を実行できる操作を反映するように名前必要があります。

Microsoft では、Windows XP には、次の名前が必要です。

**Root**  
この項目は、WIA 項目のツリー内の最初の要素を表します。

**フラット ベッド**  
フラット ベッド スキャナーでドキュメント フィーダー付きの有無を表す項目です。

**フィーダー**  
ドキュメント フィーダー付きのみ使用しているスキャナーを表す項目です。

Windows Me と Windows XP は、アプリケーションする必要がありますプロパティの読み取り WIA ルート項目の最初の子項目をスキャナー デバイスの機能を確認できるようにします。

アプリケーションは、WIA サービスを使用して、次の操作を実行することができます。

-   スキャナーの機能のクエリを実行します。

-   スキャナーのデバイス プロパティを設定します。

-   データ転送を要求します。

アプリケーションは、通常は、次の 2 つの項目で表される自動ドキュメント フィーダー (ADFs) を含むフラット ベッド スキャナーを想定: ルート項目と 1 つの子項目。 すべてのデータ転送は、子項目から実行されます。
