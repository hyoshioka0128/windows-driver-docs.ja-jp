---
title: モニター フィルター ドライバー
description: モニター フィルター ドライバー
ms.assetid: cf2bd4c5-d586-4202-ad79-4e7ff9ad6061
keywords:
- フィルター ドライバー WDK モニター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90fa623cda5ab86e461cc7b771073e1213e6c51d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56582364"
---
# <a name="monitor-filter-drivers"></a>モニター フィルター ドライバー


## <span id="ddk_monitor_filter_drivers_gg"></span><span id="DDK_MONITOR_FILTER_DRIVERS_GG"></span>


Microsoft は、汎用的なモニター クラス関数ドライバー、Monitor.sys、ほとんどのモニターに関連するタスクを処理します。 仕入先がモニター クラスの関数のドライバーによって提供されるもの以外のサービスを提供したい場合を除き、モニターのベンダーから提供されたドライバーの必要はありません。

モニター ベンダーがフィルター ドライバーを提供することを選択する場合、そのドライバーは、モニターのデバイス スタックの機能のデバイス オブジェクトの上に位置するフィルター デバイス オブジェクトによって表されます。 フィルター ドライバーは、モニターのベンダーによって提供されることも、ユーザー モード アプリケーションからの要求を処理します。 フィルター ドライバーとユーザー モード アプリケーション間のインターフェイスは、プライベートおよびモニターの仕入先のみで認識します。

モニターのベンダーには、目的のためのフィルター ドライバーは記述しないでください、表示データ チャネル コマンド インターフェイス (CI/DDC) 経由のモニターのプログラムによる制御が、監視デバイス スタックで処理されないことに注意してください。

モニターのデバイス スタックの形式では、次を参照してください。[モニター クラス関数ドライバー](monitor-class-function-driver.md)します。

 

 





