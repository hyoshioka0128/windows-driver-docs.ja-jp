---
title: KS のクロック
description: KS のクロック
ms.assetid: e3ffc7ca-f3cd-4989-af40-78b6a2438f95
keywords:
- カーネルの WDK、クロックのストリーミング
- KS WDK、クロック
- ストリーミングのクロックの WDK カーネル
- ストリーミング時間 WDK カーネル
- ストリーミング時間スタンプの WDK カーネル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c61cd0ef2dc26fa00d296c3c6b7fdd85c447c349
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362250"
---
# <a name="ks-clocks"></a>KS のクロック





AVStream、ミニドライバーを作成する場合を参照してください[AVStream クロック](avstream-clocks.md)します。

セット内のプロパティのコールバックを提供することでクロックの操作をサポートしてカーネル ストリーミング ミニドライバー [KSPROPSETID\_クロック](https://msdn.microsoft.com/library/windows/hardware/ff566564)します。 これを行う方法についてを参照してください。 [KS プロパティ](ks-properties.md)します。

クロックが特定のタイムスタンプに達したときに通知するか、クロックに一定の時間が経過する定期的な通知を受信する、ユーザー モードのクライアントを要求できます。 これを行うには、クライアントが登録[ **KSEVENT\_クロック\_位置\_マーク**](https://msdn.microsoft.com/library/windows/hardware/ff561811)と[ **KSEVENT\_クロック\_間隔\_マーク**](https://msdn.microsoft.com/library/windows/hardware/ff561805)します。

このセクションには、次のトピックについての情報が含まれています。

[マスターのクロック](master-clocks.md)

[既定のクロック](default-clocks.md)

 

 




