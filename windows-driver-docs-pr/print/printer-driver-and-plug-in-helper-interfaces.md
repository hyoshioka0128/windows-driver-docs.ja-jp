---
title: プリンター ドライバーとプラグイン ヘルパーのインターフェイス
description: プリンター ドライバーとプラグイン ヘルパーのインターフェイス
ms.assetid: 21e5ae44-01e8-4f80-8d67-18e4d9c190c5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dd9cd4f296b2e9765519d15302cd759736a7b26
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340892"
---
# <a name="printer-driver-and-plug-in-helper-interfaces"></a>プリンター ドライバーとプラグイン ヘルパーのインターフェイス


[IPrintCoreHelper](https://msdn.microsoft.com/library/windows/hardware/ff552960) - 4 コアのすべてのドライバー モジュールで使用できる基本的な機能を提供するインターフェイスで、以降 Windows Vista で利用できますが、Unidrv レンダリング、Unidrv ユーザー インターフェイス (UI) Pscript5 レンダリングでは、Pscript5 UI。 に、4 つすべてのモジュールを 1 つのインターフェイスが用意されています。

-   インターフェイスには、基になるアーキテクチャが反映されます。

-   インターフェイスは、制約の解像度などの特定の動作を実行するには、プラグインの一般的なコード モジュールを記述する機能を提供します。

使用することができます、 **IPrintCoreHelper** Unidrv および Pscript5 ベースのドライバーの 1 つの UI 置換プラグインを記述するインターフェイス。

追加の 2 つのインターフェイスがあるため Pscript5 Unidrv ドライバー インフラストラクチャ間の相違点、 [IPrintCoreHelperUni](https://msdn.microsoft.com/library/windows/hardware/ff552940)と[IPrintCoreHelperPS](https://msdn.microsoft.com/library/windows/hardware/ff552906)、から継承します。**IPrintCoreHelper**インターフェイスを個々 のドライバーに基づく拡張サービスを提供します。 これらのインターフェイスは、それぞれのモジュールでのみ使用できます。 Pscript5 のヘルパー インターフェイス**IPrintCoreHelperPS**、Unidrv のヘルパー インターフェイスの中に特定 PostScript のプリンターの説明 (PPD) データへのアクセスを提供します**IPrintCoreHelperUni**、提供、Windows Vista の新機能である、GDL パーサーを使用して一般的なプリンターの構成 (GPD) ファイルにアクセスする権限です。

このセクションでは、次のトピックでは。

[Unidrv とプラグインの Pscript5 ヘルパー インターフェイス](unidrv-and-pscript5-helper-interfaces-for-plug-ins.md)

[インターフェイスを公開](publishing-the-interfaces.md)

[IPrintCoreHelper インターフェイスの詳細](details-of-the-iprintcorehelper-interface.md)

 

 




