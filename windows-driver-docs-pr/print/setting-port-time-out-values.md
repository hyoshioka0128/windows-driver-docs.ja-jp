---
title: ポートのタイムアウト値の設定
description: ポートのタイムアウト値の設定
ms.assetid: bf39670b-440d-46f9-9110-790d36eb3b49
keywords:
- ポート管理 WDK 印刷、タイムアウト値
- タイムアウト WDK 印刷
- OpenPort
- SetPortTimeOuts
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5479f5418904d41c102d3c5bf73fd9c1c756bd2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840410"
---
# <a name="setting-port-time-out-values"></a>ポートのタイムアウト値の設定





変更可能なタイムアウト値が設定されているポートのポートモニターを作成する場合、タイムアウト値は、モニターの[**Openport**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winsplp/nf-winsplp-openport)関数内から初期化する必要があります。 たとえば、[サンプルのポートモニター](sample-port-monitor.md)である Localmon の**openport**関数は、この目的のために Microsoft Windows SDK のドキュメントで説明されている**setcommtimeouts**関数を呼び出します。

また、ポートモニターでは、必要に応じて[**Setporttimeouts**](https://docs.microsoft.com/previous-versions/ff562630(v=vs.85))関数を指定することもできます。これは、言語モニターから呼び出すことができます。 関数は、[サンプル言語モニター](sample-language-monitor.md)である Pjlmon .dll によって呼び出されます。 印刷スプーラは**Setporttimeouts**を呼び出しません。

 

 




