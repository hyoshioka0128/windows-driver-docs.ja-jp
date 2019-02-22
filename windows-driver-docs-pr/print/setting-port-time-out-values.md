---
title: ポート設定のタイムアウト値
description: ポート設定のタイムアウト値
ms.assetid: bf39670b-440d-46f9-9110-790d36eb3b49
keywords:
- ポート管理 WDK 印刷、タイムアウト値
- タイムアウト WDK の印刷
- OpenPort
- SetPortTimeOuts
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22c4dfcd6fd4ad424b61c57f2f92b9c42f339c45
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560028"
---
# <a name="setting-port-time-out-values"></a>ポート設定のタイムアウト値





モニターの内からタイムアウト値を初期化する必要がありますを変更可能なタイムアウト値を持つポートのポート モニターを作成する場合[ **OpenPort** ](https://msdn.microsoft.com/library/windows/hardware/ff559593)関数。 たとえば、 **OpenPort** Localmon.dll、関数、[サンプル ポート モニター](sample-port-monitor.md)、呼び出し、 **SetCommTimeouts** Microsoft Windows SDK で説明されている関数この目的の場合は、ドキュメントです。

さらに、ポート モニタを提供できます必要に応じて、 [ **SetPortTimeOuts** ](https://msdn.microsoft.com/library/windows/hardware/ff562630)関数で、言語モニターによって呼び出すことができます。 Pjlmon.dll、によって、関数が呼び出されます、[サンプル言語モニター](sample-language-monitor.md)します。 印刷スプーラを呼び出しません**SetPortTimeOuts**します。

 

 




