---
title: Windows Vista の GPD の自動構成フロー
description: Windows Vista の GPD の自動構成フロー
ms.assetid: 41468218-fa05-4431-a57d-3056449f2e2e
keywords:
- GPD ファイル WDK GDL 拡張機能、自動構成フロー
- 組み込みの自動構成サポート WDK プリンター、一連の手順
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a8a92eff84165592aa9541c0374830a3f00c52b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842838"
---
# <a name="autoconfiguration-flow-for-gpd-in-windows-vista"></a>Windows Vista の GPD の自動構成フロー


自動構成は次の順序に従います。

1.  ポートモニターは、以前にキャッシュに存在しなかった値または変更された値を含む通知をスプーラに送信します。

2.  スプーラは、 [**DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent)を呼び出すことによって、ポートモニターからの通知に応答します。

3.  プリンタ\_イベント\_構成は、すべての新しい値を含むドライバに渡されます。 ドライバーには、属性の値が変更されたことが通知され、レジストリも更新されます。

4.  通知が大きすぎる場合は、スキーマイベントの削減が呼び出されます。

5.  Ppd 内のすべての GDL ファイル拡張子と GDL コンテンツを含む、PPD ファイルが解析されます。 GDL ファイルの拡張子または PPD ファイル全体のすべての GDL コンテンツは、 **\*Ifdef**: gdl\_有効で、 **\*Endif**: gdl\_有効になっている必要があります。

6.  プラグインによって **\*MSBidiValue**の値が取得されます。この値は **\*QueryString**の現在の文字列値に基づいています。 たとえば、"\\DuplexUnit: Installed" という **\*QueryString**値は、ブール値 (TRUE) の **\*bidivalue**値を表します。

7.  プラグインによって、最新の構成に従ってドライバーの UI が更新されます。

 

 




