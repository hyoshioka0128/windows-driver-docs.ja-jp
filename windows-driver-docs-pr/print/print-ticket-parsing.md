---
title: 印刷チケット解析
description: 印刷チケット解析
ms.assetid: 8328110a-abb4-47aa-ab1d-730e4a2ce7bd
keywords:
- XPSDrv プリンター ドライバー WDK、モジュールを表示します。
- モジュール WDK XPSDrv、印刷チケットを表示します。
- 印刷チケット WDK、XPSDrv プリンター ドライバー
- 解析の印刷チケット オブジェクト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5144289f05eba100bc3161a328f028386ddace13
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363981"
---
# <a name="print-ticket-parsing"></a>印刷チケット解析


印刷チケットは、現在の文書パーツのマージされたが後、印刷ドライバーのフィルターはフィルターに適用される設定を検索する内容を解析する必要があります。 メソッド、 [IPrintCoreHelper インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nn-prcomoem-iprintcorehelper)印刷チケットの要素を解析するために、印刷ドライバーのフィルター モジュールで使用できます。 印刷チケットから印刷チケットの要素を展開した後は、フィルター モジュールの関数に統合することができます。 フィルター モジュールが記載されて、 [XPS フィルター パイプライン](xpsdrv-printer-driver.md)セクション。

 

 




