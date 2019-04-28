---
title: ハング検出と回復
description: IHV コンポーネントに、このコマンドを実行した後、ホストは、タイマーを開始します。
ms.assetid: 89133252-C08C-4ADC-A5EE-E46A91909337
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbce550fe7744e921d732085f37a0a7abe5fcaa7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367526"
---
# <a name="hang-detection-and-recovery"></a>ハング検出と回復


IHV コンポーネントに、このコマンドを実行した後、ホストは、タイマーを開始します。 IHV コンポーネントが完了する前に、タイマーが切れた場合 (手順 3 メッセージ図形内で[通信モデル、同期、および中止](wdi-communication-model.md))、ドライバーで IHV コンポーネントが停止している、IHV コンポーネントをリセットし、場合が回復されます前提条件です。

前提条件は、システムがバスまたはデバイス レベルでは、デバイスをリセットする ACPI メソッドを提供することです。

M1、M3 のハングのタイムアウトは、10 秒です。

M3 M4 タスクがハングのタイムアウトは 30 秒、またはタスクに基づいて構成できます。

> [!NOTE]
> いくつかのタスクを予想して、(たとえば、特定のシナリオで選択したレジストラー ビットの場合、Wi-Fi Direct の検出など) の完了まで 30 秒より長い時間がかかる場合があります。 このような場合は、タスクのホスト側開始のタイムアウトは 30 秒、タスクの最大の予想される実行時間よりも長いために適宜調整されます。 

これらは、コマンドの最大上限を設定し、この時間は、エラーと見なされるよりも長くかかる処理します。 操作 (CPU stress なし) の通常モードの場合、ほとんどのタスクとプロパティ終了が大幅に上記で指定したタイムアウトよりも早くと想定されます。 これらの値は、各タスクまたはプロパティで指定されます。 アダプターでは、これらの実行時間を超える原因となる待機がないことを確認してください。

## <a name="in-this-section"></a>このセクションの内容

[UE ハングアップ検出と復旧フロー](wdi-ue-hang-detection-and-recovery-flow.md)
[UE ハング検出: 手順 1 ~ 14](wdi-ue-hang-detection--step-1-to-step-14.md)
[(突然の削除) のリセット: 15 ~ 20 のステップ](wdi-reset--surprise-remove---steps-15-20.md)
 [診断の呼び出しのタイミング](wdi-timings-for-diagnose-call.md)
[LE ハング検出](wdi-le-hang-detection.md)
[PLDR](wdi-pldr-and-fldr.md)
 

 





