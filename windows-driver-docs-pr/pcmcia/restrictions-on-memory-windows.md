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
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580438"
---
# <a name="restrictions-on-memory-windows"></a>メモリ ウィンドウに関する制限事項





このセクションでは、Windows 2000 および PCMCIA メモリ カードのメモリ ウィンドウで、以降のオペレーティング システムによって課される制限について説明します。

PCMCIA のメモリ カードのリソース要件は、プラグ アンド プレイのマネージャーの要求でデバイスを列挙したときに通常、バス ドライバーによって指定されます。 Windows の特定のメモリを指定することも、 [ **INF DDInstall.LogConfigOverride セクション**](https://msdn.microsoft.com/library/windows/hardware/ff547339)デバイス ドライバーの INF ファイル。 PCMCIA のメモリ カードの 2 つのメモリ ウィンドウの最大値を要求できます。

 

 





