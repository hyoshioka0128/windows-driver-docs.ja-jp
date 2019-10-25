---
title: 印刷チケット解析
description: 印刷チケット解析
ms.assetid: 8328110a-abb4-47aa-ab1d-730e4a2ce7bd
keywords:
- XPSDrv プリンタードライバー WDK、render モジュール
- レンダーモジュール WDK XPSDrv、印刷チケット
- 印刷チケット WDK、XPSDrv プリンタードライバー
- 印刷チケットオブジェクトの解析
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5071e3cd20b2ee6585297ae7e68f2cd2d894401b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842338"
---
# <a name="print-ticket-parsing"></a>印刷チケット解析


現在のドキュメントパーツに対して印刷チケットをマージした後、印刷ドライバーフィルターは、そのコンテンツを解析して、フィルターに適用される設定を見つける必要があります。 印刷ドライバーフィルターモジュールでは、 [Iprintcorehelper インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelper)のメソッドを使用して、印刷チケット要素を解析できます。 印刷チケット要素は、印刷チケットから抽出された後、フィルターモジュール関数に統合できます。 フィルターモジュールについては、「 [XPS フィルターパイプライン](xpsdrv-printer-driver.md)」セクションを参照してください。

 

 




