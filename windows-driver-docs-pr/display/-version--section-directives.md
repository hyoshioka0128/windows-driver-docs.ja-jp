---
title: '[バージョン] セクション ディレクティブ'
description: このトピックでは、[バージョン]、INF セクション ディレクティブについて説明します。
ms.assetid: 76AC10DC-AECC-4C35-8BEE-4B2E8B06FEE0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e472b66ca51893a81e181c97fde57322f4960594
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391286"
---
# <a name="version-section-directives"></a>\[バージョン\]セクション ディレクティブ


このトピックで説明 *\[バージョン\]* INF でディレクティブをセクションします。

受信トレイのすべてのドライバーでは、Layout.inf ファイルを参照する必要があります。

受信トレイのすべてのドライバーは、すべてのカタログ ファイルを参照しないでください。

次に、例を示します。

``` syntax
[Version]
Signature="$Windows NT$"
Provider=%MSFT%
ClassGUID={4D36E968-E325-11CE-BFC1-08002BE10318}
Class=Display
DriverVer=11/22/2004, 6.14.10.7000

Note: 
no line item for LayoutFile=layout.inf
no line item for CatalogFile=delta.cat
```

WHQL ディスプレイ ドライバーは、Layout.inf ファイルを参照する必要があります。

次に、例を示します。

``` syntax
[Version]
Signature="$Windows NT$"
Provider=%IHV%
ClassGUID={4D36E968-E325-11CE-BFC1-08002BE10318}
Class=Display
DriverVer=11/22/2004, 6.14.10.7000

Note: 
no line item for LayoutFile=layout.inf
```

 

 





