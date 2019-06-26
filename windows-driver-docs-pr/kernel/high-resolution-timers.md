---
title: 高分解能タイマー
description: Windows 8.1 以降、ドライバーは高解像度のタイマーを管理するのに ExXxxTimer ルーチンを使用できます。
ms.assetid: B8F2B28C-A02B-4015-B392-3D30BC0229B8
keywords:
- 高分解能タイマー
- タイマー精度
- タイマー精度
- システム クロックの粒度
- EX_TIMER_HIGH_RESOLUTION
- ExXxxTimer ルーチン
- ExQueryTimerResolution
- ExSetTimerResolution
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 186a6899369a48d218f27854ebe2d4284bf717bd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371886"
---
# <a name="high-resolution-timers"></a>高分解能タイマー


Windows 8.1 以降、ドライバーを使用できる、 [ **Ex*Xxx*タイマー** ](exxxxtimer-routines-and-ex-timer-objects.md)高分解能タイマーを管理するルーチン。 高分解能タイマーの精度は、システム クロックの最大のサポートされている解像度によってのみ制限されます。 これに対し、既定のシステム時計の解像度に制限されているタイマーは、正確性が大幅に低下します。

ただし、高解像度のタイマーには、システム クロック割り込みを必要があります。: 少なくとも、一時的に — 電力消費量が増加する傾向にある、より高い割合で発生します。 そのため、ドライバーは高分解能タイマーを使用して、タイマー精度が、重要な場合にのみとそれ以外の場合、既定の解像度タイマーを使用する必要があります。

WDM ドライバーが呼び出し高分解能タイマを作成するのには、 [ **ExAllocateTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatetimer)ルーチンとセット EX\_タイマー\_高\_解像度、フラグ*属性*パラメーター。 ドライバーを呼び出すと、 [ **ExSetTimer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exsettimer)高分解能タイマを設定する日常的なオペレーティング システムが、必要に応じて、システム時計の解像度ように位置回タイマー有効期限が切れるで指定した有効期限が切れた時刻に正確に対応の詳細は、 *DueTime*と*期間*パラメーター。

カーネル モード ドライバー フレームワーク (KMDF) ドライバーを呼び出すことができます、 [ **WdfTimerCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/nf-wdftimer-wdftimercreate)高分解能タイマを作成します。 この呼び出しでは、ドライバーはへのポインターを渡します。 を[ **WDF\_タイマー\_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdftimer/ns-wdftimer-_wdf_timer_config)をパラメーターとして構造体。 高分解能タイマをドライバーのセットを作成する、 **UseHighResolutionTimer**をこの構造体のメンバー **TRUE**します。 このメンバーは、Windows 8.1 および KMDF バージョン 1.13 以降では、構造体の一部です。

## <a name="controlling-timer-accuracy"></a>タイマー精度を制御します。


たとえば、x86 で実行されている Windows のプロセッサ、システム クロックのティック間の既定の間隔は使用可能では、通常 15 ミリ秒、およびシステム クロックのティック間の最小間隔は約 1 ミリ秒。 したがって、既定の解像度タイマーの有効期限 (が**ExAllocateTimer**場合作成 EX\_タイマー\_高\_解像度フラグが設定されていない) 約 15 内にのみ制御できます(ミリ秒単位) が高分解能タイマの有効期限は、1 ミリ秒内に制御できます。

ドライバーは、既定の解像度タイマーの相対的な有効期限の時間を指定する場合は、指定した有効期限より前または後最大で約 15 ミリ秒、タイマーが切れることができます。 ドライバーは、高分解能タイマーの相対的な有効期限の時間を指定する場合遅延指定の有効期限の後のミリ秒の時間が無期限に早い段階として、タイマーの期限が切れできます。 システム クロックの解像度とタイマー精度の間のリレーションシップの詳細については、次を参照してください。[タイマー精度](timer-accuracy.md)します。

高解像度のタイマーが設定されていない場合、オペレーティング システムは通常、システム クロックをその既定のレートで実行されます。 ただし、1 つまたは複数の高解像度タイマーが設定されている場合は、オペレーティング システムがその最大レートでこれらのタイマーの有効期限が切れるまでの時間の少なくとも一部のシステム クロックを実行する必要があります。

不必要な電力消費量を増やすことを避けるためには、オペレーティング システムには、その最大転送率の高解像度のタイマーのタイミングの要件を満たすために必要な場合にのみでシステム クロックが実行されます。 たとえば、高分解能タイマーは、その期間にわたるいくつかの既定システム クロックのティック場合は、オペレーティング システム可能性がありますシステム クロック最大速度でのみ実行ごとの有効期限の直前にあるタイマー期間の一部。 タイマーの期間の残りの部分、システム クロックがその既定のレートでが実行されます。

電力の過剰消費を防ぐためには、ドライバーが、実行時間の長い高分解能タイマーの期間のシステム クロックのティック間の既定の間隔よりも小さい値に設定を避ける必要があります。 それ以外の場合、最大速度でシステム クロックを継続的に実行するオペレーティング システムが強制されます。

Windows 8 以降、ドライバーが呼び出すことができます、 [ **ExQueryTimerResolution** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exquerytimerresolution)ルーチンをシステム クロックでサポートされているタイマーの解像度の範囲を取得します。

## <a name="comparison-to-exsettimerresolution"></a>ExSetTimerResolution との比較


Windows 2000 以降、ドライバーが呼び出すことができます、 [ **ExSetTimerResolution** ](calling-exsettimerresolution-while-processing-a-power-irp.md)ルーチンを一連のシステム クロック割り込み間の時間間隔を変更します。 たとえば、ドライバーでは、その既定のレートからタイマー精度を向上させるために最大速度に、システム クロックを変更するには、このルーチンを呼び出すことができます。 ただしを使用して**ExSetTimerResolution**によって作成された高解像度のタイマーを使用する場合に比べていくつかの欠点が**ExAllocateTimer**します。

最初に呼び出した後**ExSetTimerResolution**をシステム クロックの速度を一時的に増やします、ドライバーを呼び出す必要があります**ExSetTimerResolution**をもう一度その既定のレートに、システム クロックを復元します。 それ以外の場合、システム時計のタイマーは、継続的に電力の過剰消費を原因と考えられる最大転送率の割り込みを生成します。

次に、ドライバーを使用する、 **ExSetTimerResolution**ルーチンが、オペレーティング システムが高解像度のタイマーは効果的に高いシステム クロックの速度、一時的に使用を最適化することはできません。 したがって、システム クロックより厳密に必要な最大レートで実行されている多くの時間を費やしています。

同時に複数のドライバーを使用する場合、サードパーティ**ExSetTimerResolution**タイマー精度を高めるためには、システム クロックを長期間実行の最大レートで可能性があります。 これに対し、オペレーティング システムではグローバルに複数の高解像度タイマーの操作を調整して、システム クロックがこれらのタイマーのタイミングの要件を満たすために必要な場合にのみの最大レートでが実行されるようにします。

最後を使用して**ExSetTimerResolution**は本質的に高分解能タイマを使用するよりも精度が低下します。 ドライバーを呼び出してから**ExSetTimerResolution** 、ミリ秒あたりのティックの詳細については、最大速度に、システム クロックを向上させるドライバー呼び出すことができます、ルーチンなど[ **KeSetTimerEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesettimerex)タイマーを設定します。 タイマーできる最大有効期限が切れる、この呼び出しでは、ドライバーは、相対的な有効期限の時間を指定する場合は、約 1 ミリ秒より前か、指定した有効期限よりも後。 ただし、高分解能タイマーの相対的な有効期限の時間が指定されている場合は、タイマーできます有効期限が切れるまで約 1 ミリ秒、指定した有効期限より後が決して早期失効します。

 

 




