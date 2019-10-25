---
title: 高分解能タイマー
description: Windows 8.1 以降では、ドライバーは Exxxx タイマールーチンを使用して、高解像度のタイマーを管理できます。
ms.assetid: B8F2B28C-A02B-4015-B392-3D30BC0229B8
keywords:
- 高解像度タイマー
- タイマー精度
- タイマー精度
- システムクロックの粒度
- EX_TIMER_HIGH_RESOLUTION
- Exxxx タイマールーチン
- ExQueryTimerResolution
- ExSetTimerResolution
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: fbb3ddbfcef4ae646420e6a2967abac5a2687486
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838648"
---
# <a name="high-resolution-timers"></a>高分解能タイマー


Windows 8.1 以降では、ドライバーで[**Ex*Xxx*タイマー**](exxxxtimer-routines-and-ex-timer-objects.md)ルーチンを使用して、高解像度のタイマーを管理できます。 高解像度タイマーの精度は、システムクロックのサポートされている最大解像度によってのみ制限されます。 これに対し、既定のシステムクロック解像度に限定されたタイマーは、大幅に精度が低下します。

ただし、高解像度のタイマーでは、システムクロック割り込み (少なくとも一時的に) が高い速度で実行されるため、電力消費量が増加する傾向があります。 そのため、ドライバーは、タイマー精度が不可欠な場合にのみ、高解像度タイマーを使用し、その他のすべての場合に既定の解決タイマーを使用する必要があります。

高解像度タイマーを作成するには、WDM ドライバーが[**Exallocatetimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatetimer)ルーチンを呼び出し、 *Attributes*パラメーターに\_TIMER\_high\_resolution フラグを設定します。 ドライバーが[**ExSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exsettimer)ルーチンを呼び出して高解像度タイマーを設定すると、オペレーティングシステムは必要に応じてシステムクロックの解決を増やします。これにより、タイマーが有効期限切れになるまでの時間がより正確になります。*DueTime*および*Period*パラメーターに指定された有効期限。

カーネルモードドライバーフレームワーク (KMDF) ドライバーは、 [**Wdftimercreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/nf-wdftimer-wdftimercreate)メソッドを呼び出して、高解像度のタイマーを作成できます。 この呼び出しでは、ドライバーは[**WDF\_TIMER\_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdftimer/ns-wdftimer-_wdf_timer_config)構造体へのポインターをパラメーターとして渡します。 高解像度タイマーを作成するために、ドライバーはこの構造体の**Usehighresolution タイマー**メンバーを**TRUE**に設定します。 このメンバーは、Windows 8.1 と KMDF バージョン1.13 以降の構造体の一部です。

## <a name="controlling-timer-accuracy"></a>タイマー精度の制御


たとえば、x86 プロセッサで実行されている Windows の場合、システムクロックティック間の既定の間隔は通常約15ミリ秒で、システムクロックティックの最小間隔は約1ミリ秒です。 このため、既定の解決タイマーの有効期限 (例\_タイマー\_高\_解像度フラグが設定されていない場合) は、約15ミリ秒以内でのみ制御**できますが**、有効期限は、高解像度のタイマーは、ミリ秒以内に制御できます。

ドライバーが既定の解決タイマーの相対有効期限を指定した場合、タイマーは指定された有効期限よりも最大15ミリ秒前に期限切れになることがあります。 ドライバーが高解像度タイマーの相対有効期限を指定した場合、タイマーは、指定された有効期限からのミリ秒ほど遅れますが、早期に期限切れになることはありません。 システムクロックの解像度とタイマー精度の関係の詳細については、「[タイマー精度](timer-accuracy.md)」を参照してください。

高解像度のタイマーが設定されていない場合、オペレーティングシステムは通常、システムクロックを既定の速度で実行します。 ただし、1つまたは複数の高解像度タイマーが設定されている場合、オペレーティングシステムは、これらのタイマーの有効期限が切れる前に、少なくともその時間の最大速度でシステムクロックを実行する必要があります。

不要な電力消費を避けるために、オペレーティングシステムは、高解像度タイマーのタイミング要件を満たすために必要な場合に限り、システムクロックを最大速度で実行します。 たとえば、高解像度のタイマーが周期的で、その期間が複数の既定のシステムクロックティックにまたがっている場合、オペレーティングシステムは、各有効期限の直前にあるタイマー期間の部分でのみ、最大速度でシステムクロックを実行する可能性があります。 残りのタイマー期間については、システムクロックが既定の速度で実行されます。

電力消費が過剰にならないようにするには、実行時間の長い高解像度タイマーの期間を、システムクロックティック間の既定の間隔よりも短い値に設定することを避ける必要があります。 そうしないと、オペレーティングシステムは、システムクロックを常に最大速度で継続的に実行することになります。

Windows 8 以降では、ドライバーは[**Exquerytimerresolution**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exquerytimerresolution)ルーチンを呼び出して、システムクロックでサポートされているタイマー解像度の範囲を取得できます。

## <a name="comparison-to-exsettimerresolution"></a>ExSetTimerResolution との比較


Windows 2000 以降では、ドライバーは[**Exsettimerresolution**](calling-exsettimerresolution-while-processing-a-power-irp.md)ルーチンを呼び出して、連続するシステムクロック割り込み間の時間間隔を変更できます。 たとえば、ドライバーはこのルーチンを呼び出して、システムクロックを既定の速度から最大速度に変更し、タイマーの精度を向上させることができます。 ただし、 **Exsettimerresolution**を使用すると、 **Exsettimerresolution**によって作成された高解像度タイマーを使用する場合と比較して、いくつかの欠点があります。

まず、 **Exsettimerresolution**を呼び出してシステムクロックレートを一時的に増やした後、ドライバーは、システムクロックを既定の速度に復元するために、2回目に**exsettimerresolution**を呼び出す必要があります。 それ以外の場合は、システムクロックタイマーによって割り込みが最大速度で継続的に生成されるため、電力消費が過剰になる可能性があります。

2つ目の方法として、 **Exsettimerresolution**ルーチンを使用するドライバーは、オペレーティングシステムが高解像度タイマーに対して行うのと同じように、システムクロックレートの高い一時的な使用を最適化することはできません。 したがって、システムクロックは、厳密には必要ではなく、最大速度での実行に時間がかかることになります。

3つ目の方法として、複数のドライバーが同時に**Exsettimerresolution**を使用してタイマー精度を向上させる場合、システムクロックが長い間、最大速度で実行される可能性があります。 これに対し、オペレーティングシステムでは、複数の高解像度タイマーの動作がグローバルに調整されるので、システムクロックは、これらのタイマーのタイミング要件を満たすために必要な場合に限り、最大速度で実行されます。

最後に、 **Exsettimerresolution**を使用することは、高解像度タイマーを使用するよりも本質的に精度が低くなります。 ドライバーが**Exsettimerresolution**を呼び出してシステムクロックを最大速度に上げると (通常はミリ秒あたりのティック)、ドライバーは[**Kesettimerex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kesettimerex)などのルーチンを呼び出してタイマーを設定する可能性があります。 この呼び出しで、ドライバーが相対的な有効期限を指定した場合、タイマーの有効期限は、指定した有効期限よりも前のミリ秒になります。 ただし、高解像度タイマーに対して相対的な有効期限が指定されている場合、タイマーは、指定された有効期限よりも長い間、期限切れになることがありますが、早期に期限切れになることはありません。

 

 




