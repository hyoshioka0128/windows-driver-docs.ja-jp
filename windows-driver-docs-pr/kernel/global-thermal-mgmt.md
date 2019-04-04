---
title: グローバルの温度管理
description: IRP_MN_SURPRISE_REMOVAL 要求の処理
ms.assetid: 3CBF44B2-891A-4B68-97F6-3563EC0D5122
keywords:
- グローバルの温度管理
- 温度
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3177ded380484b2f4661582cc643680672eaa4bd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538758"
---
# <a name="global-thermal-management"></a>グローバルの温度管理 

GUID_THERMAL_COOLING_INTERFACE のドライバー インターフェイスでは、さまざまなハードウェア プラットフォームでデバイスの温度のグローバルな管理に参加するデバイス ドライバーを使用します。 温度管理機能を備えたデバイス用のドライバーでは、このインターフェイスに、コールバック ルーチンを実装します。 オペレーティング システムでは、ユーザー アクティビティと環境の状態の変更に応答し、プラットフォームに温度のレベルを動的に管理するためにこれらのルーチンを呼び出します。

過熱を防ぐことでは、Windows 温度管理は、確実に動作するデバイスを保持し、ユーザーがアクセスできるサーフェスがホット多くなることを防ぎます。 Windows は、プラットフォームは、バッテリの充電で操作できる時間を延長とでは常に、常に接続されているコンピューターの外観を維持するために、プラットフォームのデバイスの温度レベル要件をインテリジェントに分散します。

詳細については、[デバイス レベルの温度管理](device-level-thermal-management.md)を参照してください。

