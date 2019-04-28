---
title: メモリ ウィンドウに関する制限事項
description: メモリ ウィンドウに関する制限事項
ms.assetid: 664320e6-b155-470b-9b86-8b463663961f
keywords:
- PCMCIA WDK バス、[メモリ] ウィンドウ
- メモリ ウィンドウ WDK PCMCIA バス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 59fb0c3ccab6445493a43bb15c9c39fac2b346ee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378254"
---
# <a name="restrictions-on-memory-windows"></a>メモリ ウィンドウに関する制限事項





このセクションでは、Windows 2000 および PCMCIA メモリ カードのメモリ ウィンドウで、以降のオペレーティング システムによって課される制限について説明します。

PCMCIA のメモリ カードのリソース要件は、プラグ アンド プレイのマネージャーの要求でデバイスを列挙したときに通常、バス ドライバーによって指定されます。 Windows の特定のメモリを指定することも、 [ **INF DDInstall.LogConfigOverride セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547339)デバイス ドライバーの INF ファイル。 PCMCIA のメモリ カードの 2 つのメモリ ウィンドウの最大値を要求できます。

 

 





