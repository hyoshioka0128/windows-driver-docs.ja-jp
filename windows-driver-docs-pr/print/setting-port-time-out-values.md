---
title: ポート タイムアウト値の設定
description: ポート タイムアウト値の設定
ms.assetid: bf39670b-440d-46f9-9110-790d36eb3b49
keywords:
- ポート管理 WDK 印刷、タイムアウト値
- タイムアウト WDK の印刷
- OpenPort
- SetPortTimeOuts
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 02b507030b09bbf26a531b439dcae6d1a277ad7a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384167"
---
# <a name="setting-port-time-out-values"></a>ポート タイムアウト値の設定





モニターの内からタイムアウト値を初期化する必要がありますを変更可能なタイムアウト値を持つポートのポート モニターを作成する場合[ **OpenPort** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winsplp/nf-winsplp-openport)関数。 たとえば、 **OpenPort** Localmon.dll、関数、[サンプル ポート モニター](sample-port-monitor.md)、呼び出し、 **SetCommTimeouts** Microsoft Windows SDK で説明されている関数この目的の場合は、ドキュメントです。

さらに、ポート モニタを提供できます必要に応じて、 [ **SetPortTimeOuts** ](https://docs.microsoft.com/previous-versions/ff562630(v=vs.85))関数で、言語モニターによって呼び出すことができます。 Pjlmon.dll、によって、関数が呼び出されます、[サンプル言語モニター](sample-language-monitor.md)します。 印刷スプーラを呼び出しません**SetPortTimeOuts**します。

 

 




