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
ms.openlocfilehash: 22c4dfcd6fd4ad424b61c57f2f92b9c42f339c45
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372064"
---
# <a name="setting-port-time-out-values"></a>ポート タイムアウト値の設定





モニターの内からタイムアウト値を初期化する必要がありますを変更可能なタイムアウト値を持つポートのポート モニターを作成する場合[ **OpenPort** ](https://msdn.microsoft.com/library/windows/hardware/ff559593)関数。 たとえば、 **OpenPort** Localmon.dll、関数、[サンプル ポート モニター](sample-port-monitor.md)、呼び出し、 **SetCommTimeouts** Microsoft Windows SDK で説明されている関数この目的の場合は、ドキュメントです。

さらに、ポート モニタを提供できます必要に応じて、 [ **SetPortTimeOuts** ](https://msdn.microsoft.com/library/windows/hardware/ff562630)関数で、言語モニターによって呼び出すことができます。 Pjlmon.dll、によって、関数が呼び出されます、[サンプル言語モニター](sample-language-monitor.md)します。 印刷スプーラを呼び出しません**SetPortTimeOuts**します。

 

 




