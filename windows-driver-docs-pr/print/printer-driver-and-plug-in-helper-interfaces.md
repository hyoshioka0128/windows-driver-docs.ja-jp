---
title: プリンタードライバーとプラグインヘルパーインターフェイス
description: プリンタードライバーとプラグインヘルパーインターフェイス
ms.assetid: 21e5ae44-01e8-4f80-8d67-18e4d9c190c5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1861667a91c5bfa1c15daf0c500c2d53b3b96a54
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840436"
---
# <a name="printer-driver-and-plug-in-helper-interfaces"></a>プリンタードライバーとプラグインヘルパーインターフェイス


Windows Vista 以降で使用可能な[Iprintcorehelper](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelper)インターフェイスは、4つのコアドライバーモジュールすべて (unidrv レンダリング、unidrv ユーザーインターフェイス (UI)、Pscript5 レンダリング、Pscript5 UI) で利用できる基本的な機能を提供します。 次の理由により、4つのモジュールすべてに1つのインターフェイスが用意されています。

-   インターフェイスは、基になるアーキテクチャを反映しています。

-   インターフェイスは、プラグインの共通コードモジュールを記述して、制約の解決などの特定の動作を実行する機能を提供します。

**Iprintcorehelper**インターフェイスを使用して、Unidrv ベースおよび Pscript5 ベースのドライバー用に1つの UI 置換プラグインを記述できます。

Pscript5 と Unidrv driver インフラストラクチャの違いにより、iprintcore [Peruni](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni)と[Iprintcoreare perps](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps)という2つのインターフェイスがあります。これは**iprintcorehelper**インターフェイスから継承し、個々のドライバーに基づいて拡張サービスを提供します。 これらのインターフェイスは、それぞれのモジュールでのみ使用できます。 Pscript5 helper インターフェイス**Iprintcore Perps**は、特定の PostScript プリンターの説明 (PPD) データへのアクセスを提供します。一方、Unidrv ヘルパーインターフェイス**Iprintcore/peruni**は、汎用プリンターにアクセスする機能を提供します。GDL パーサーを使用した構成 (GPD) ファイル。これは、Windows Vista に新しく追加されたものです。

ここでは、次のトピックについて説明します。

[プラグイン用の Unidrv および Pscript5 ヘルパーインターフェイス](unidrv-and-pscript5-helper-interfaces-for-plug-ins.md)

[インターフェイスを公開する](publishing-the-interfaces.md)

[IPrintCoreHelper インターフェイスの詳細](details-of-the-iprintcorehelper-interface.md)

 

 




