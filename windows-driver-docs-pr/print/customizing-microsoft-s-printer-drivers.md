---
title: Microsoft のプリンター ドライバーをカスタマイズします。
description: Microsoft のプリンター ドライバーをカスタマイズします。
ms.assetid: b7761209-1f6f-4288-af47-4ed855c2e629
keywords:
- プリンター ドライバーの WDK のカスタマイズ
- プリンター ドライバー WDK のカスタマイズ
- プリンター ドライバーのプリンター ドライバーをカスタマイズする方法、WDK をカスタマイズします。
- プリンター ドライバーをカスタマイズする方法、WDK のプリンター ドライバーをカスタマイズします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 361235638ddee507431f86d8d9f46f7dea86c9cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571007"
---
# <a name="customizing-microsoft-printer-drivers"></a>Microsoft のプリンター ドライバーをカスタマイズします。


デザイン、 [Microsoft ユニバーサル プリンター ドライバー](microsoft-universal-printer-driver.md) (Unidrv) と[Microsoft PostScript プリンター ドライバー](microsoft-postscript-printer-driver.md) (Pscript) は、NT ベースのオペレーティング システムに基づいて[プリンター ドライバーアーキテクチャ](printer-driver-architecture.md)します。 2 つのコンポーネントの構成がそれぞれそのため、[プリンター インターフェイス DLL](printer-interface-dll.md)と[プリンター グラフィックス DLL](printer-graphics-dll.md)します。 このセクションでは、これらのコンポーネントをカスタマイズする方法について説明します。

Unidrv または Pscript の DLL が提供されるプリンターのインターフェイスをカスタマイズするには、1 つまたは複数を指定する必要があります[ユーザー インターフェイスのプラグイン](user-interface-plug-ins.md)します。ドライバーのユーザー インターフェイスを変更して、プリンターのイベントを処理して特定の追加を提供するなプラグインを使用できます。 Unidrv から Windows Vista を使用している場合は、ユーザー インターフェイスを完全に置き換えることができます。

Unidrv または Pscript の DLL が提供されるプリンターのグラフィックスをカスタマイズするには、1 つまたは複数を指定する必要があります[レンダリング プラグイン](rendering-plug-ins.md)します。印刷ジョブのデータ ストリーム内の印刷スプーラーに送信されるデータを変更するのになプラグインを使用できます。

ここでは、次のトピックについて説明します。

[ユーザー インターフェイスのプラグイン](user-interface-plug-ins.md)

[プラグインの表示](rendering-plug-ins.md)

[プリンター ドライバーの COM インターフェイスを実装します。](implementing-printer-driver-com-interfaces.md)

[カスタマイズされたドライバー コンポーネントをインストールします。](installing-customized-driver-components.md)

[プロパティ シートの一般的なユーザー インターフェイス](common-property-sheet-user-interface.md)

[プリンターの色の管理](color-management-for-printers.md)

[印刷ドライバーに対して印刷チケットのサポートを追加します。](adding-print-ticket-support-to-print-drivers.md)

[ドキュメントのデバイスを device Stage](device-stage-for-document-devices.md)

 

 




