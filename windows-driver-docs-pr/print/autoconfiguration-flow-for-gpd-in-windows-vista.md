---
title: Windows Vista の GPD の自動構成フロー
description: Windows Vista の GPD の自動構成フロー
ms.assetid: 41468218-fa05-4431-a57d-3056449f2e2e
keywords:
- GPD ファイル WDK GDL 拡張機能、自動構成のフロー
- ボックスの自動構成サポートの WDK プリンター、一連の手順
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc54fd9a9b856405abd1775f54c50f00f8aa355e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370474"
---
# <a name="autoconfiguration-flow-for-gpd-in-windows-vista"></a>Windows Vista の GPD の自動構成フロー


自動構成は、次のシーケンスを次に示します。

1.  ポート モニターは、スプーラーに以前ではなく、キャッシュまたは変更されたすべての値を含む通知を送信します。

2.  スプーラーは通知に応答のポート モニターから呼び出すことによって[ **DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvprinterevent)します。

3.  プリンター\_イベント\_構成がすべての新しい値を含むドライバーに渡されます。 属性の値が変更されたことと、レジストリを更新しても、ドライバーに通知されます。

4.  通知メッセージが大きすぎる場合は、スキーマ イベントの制限が呼び出されます。

5.  PPD ファイルを解析すると、すべての GDL ファイルの拡張機能と、PPD. 内 GDL コンテンツを含む いずれかの GDL ファイル拡張機能または PPD ファイル全体ですべての GDL コンテンツで囲む必要があります **\*Ifdef**:GDL\_有効になっていると **\*Endif**:GDL\_を有効にします。

6.  プラグインはの値を取得 **\*MSBidiValue**の現在の文字列値に基づいてこのは **\*QueryString**します。 たとえば、  **\*QueryString**の値"\\Printer.Configuration.DuplexUnit:Installed"を表す、  **\*BidiValue** BOOL(TRUE) の値。

7.  プラグインは最新の構成に従って更新のドライバーの UI。

 

 




