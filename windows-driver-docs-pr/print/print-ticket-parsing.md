---
title: 印刷チケットの解析
description: 印刷チケットの解析
ms.assetid: 8328110a-abb4-47aa-ab1d-730e4a2ce7bd
keywords:
- XPSDrv プリンター ドライバー WDK、モジュールを表示します。
- モジュール WDK XPSDrv、印刷チケットを表示します。
- 印刷チケット WDK、XPSDrv プリンター ドライバー
- 解析の印刷チケット オブジェクト
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce0d061497ef14d0589dc76db55bfd98f887995b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558317"
---
# <a name="print-ticket-parsing"></a>印刷チケットの解析


印刷チケットは、現在の文書パーツのマージされたが後、印刷ドライバーのフィルターはフィルターに適用される設定を検索する内容を解析する必要があります。 メソッド、 [IPrintCoreHelper インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff552960)印刷チケットの要素を解析するために、印刷ドライバーのフィルター モジュールで使用できます。 印刷チケットから印刷チケットの要素を展開した後は、フィルター モジュールの関数に統合することができます。 フィルター モジュールが記載されて、 [XPS フィルター パイプライン](xpsdrv-printer-driver.md)セクション。

 

 




