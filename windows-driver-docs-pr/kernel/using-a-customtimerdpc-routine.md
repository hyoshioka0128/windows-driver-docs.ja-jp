---
title: CustomTimerDpc ルーチンの使用
description: CustomTimerDpc ルーチンの使用
ms.assetid: e95d01a2-4d13-40d2-aeb0-44c45e4a49f5
keywords:
- タイマー オブジェクトの WDK カーネル、CustomTimerDpc ルーチン
- CustomTimerDpc
- タイマー オブジェクトを無効にします。
- タイマー オブジェクトの WDK カーネルを無効にします。
- 定期的なタイマー WDK カーネル
- キューのタイマー オブジェクト
- タイマー オブジェクトの WDK カーネル、有効期限の設定
- タイマーの有効期限の WDK カーネル
- 有効期限が切れたタイマー WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a93e78f91adcb769b83b8d75197c982e815b9723
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355268"
---
# <a name="using-a-customtimerdpc-routine"></a>CustomTimerDpc ルーチンの使用





以前に設定を無効にするタイマー オブジェクトをドライバーは呼び出し[ **KeCancelTimer**](https://msdn.microsoft.com/library/windows/hardware/ff551970)します。 このルーチンは、システムのタイマー キューからタイマー オブジェクトを削除します。 一般に、タイマー オブジェクトは、シグナル状態に設定されていないと、 *CustomTimerDpc*ルーチンが実行をキューに登録されません。 ただし、タイマーの期限切れが近い場合と**KeCancelTimer**が呼び出されると、有効期限が発生する可能性が前に**KeCancelTimer**後者シグナルと DPC キューは、キューの時間にアクセスする機会を持つ発生します。

リコール[ **KeSetTimer** ](https://msdn.microsoft.com/library/windows/hardware/ff553286)または[ **KeSetTimerEx**](https://msdn.microsoft.com/library/windows/hardware/ff553292)、以前指定*タイマー*と*Dpc*ポインター、以前に指定した期間が経過する前に次のような影響があります。

-   カーネル オブジェクトをシグナル状態に設定するか、またはキューなし、タイマー キューからタイマー オブジェクトを削除します、 *CustomTimerDpc*ルーチン。

-   カーネルが新しいを使用して、タイマー キュー内のタイマー オブジェクトを reinserts *DueTime*値。

さまざまな目的で同じタイマー オブジェクトを使用すると、競合状態または重大なドライバー エラーが発生できます。 たとえば、ドライバーは、オブジェクトの両方への呼び出しを設定する 1 つのタイマーを指定します、 *CustomTimerDpc*ルーチンとドライバー専用のスレッド内の待機時間を設定します。 ドライバー専用のスレッドを呼び出すたびに**KeSetTimer**、 **KeSetTimerEx**、または**KeCancelTimer**共通のタイマー オブジェクトのスレッドが、への呼び出しをキャンセルは*CustomTimerDpc*のタイマー オブジェクトが既にキューに登録する場合は、ルーチン、 *CustomTimerDpc*呼び出します。

ドライバーがある場合*CustomTimerDpc*ルーチンもタイマーで発生する待機オブジェクトおよび nonarbitrary スレッドのコンテキストでその必要があります。

-   決して nonarbitrary スレッド コンテキスト、またはその逆に、状況依存のスレッド タイマーがオブジェクトを使用します。

-   ごとに別々 のタイマー オブジェクトを割り当てる*CustomTimerDpc*ルーチン。 ドライバーのスレッドまたは nonarbitrary スレッド コンテキストで呼び出されるドライバー ルーチンの各セットは、独自のタイマーを「待機可能な」オブジェクトのセットが必要です。

使用する場合、 *CustomTimerDpc*ルーチン、ドライバーの間隔が経過する呼び出しでは慎重に選択**KeSetTimer**または**KeSetTimerEx**します。 さらに、すべての呼び出しの影響を考慮**KeCancelTimer** SMP プラットフォームでは特に、この呼び出しは、任意のドライバー ルーチンから同じタイマー オブジェクトを使用します。

に関する次の点に注意してください保持*CustomTimerDpc*ルーチン。

DPC を特定の DPC ルーチンを表すオブジェクトの 1 つだけインスタンス化は、特定の時点での実行のキューに登録できます。

2 番目のドライバーのルーチンを呼び出す場合**KeSetTimer**または**KeSetTimerEx**を実行する同じ*CustomTimerDpc*ルーチンの最初の呼び出し元によって指定された期間が経過する前に、*CustomTimerDpc*ルーチンは、2 つ目の呼び出し元によって指定された期間の期限が切れた後にのみを実行します。 このような場合、 *CustomTimerDpc*は最初のルーチンを呼び出す対象の作業は不要**KeSetTimer**または**KeSetTimerEx**します。

ドライバーを持つ*CustomTimerDpc*ルーチンと定期的なタイマーを使用します。

ドライバーは、DPC ルーチンからの定期的なタイマーを解放できません。 ドライバーのみ非連続タイマー DPC ルーチンから割り当てを解除できます。

次を検討してください。 両方があるドライバーのデザイン ガイドライン*CustomDpc*と*CustomTimerDpc*ルーチン。

競合状態を防ぐためには、渡すことはありません、同じ*Dpc*へのポインター **KeSetTimer**または**KeSetTimerEx**と[ **KeInsertQueueDpc**](https://msdn.microsoft.com/library/windows/hardware/ff552185).

つまり、たとえば、ドライバーの*StartIo*ルーチンの呼び出し**KeSetTimer**または**KeSetTimerEx**キューに、 *CustomTimerDpc*ルーチンドライバーの ISR 呼び出して**KeInsertQueueDpc**同時に同じで別のプロセッサから*Dpc*ポインター。 プロセッサの IRQL を下回るディスパッチと DPC ルーチンが実行されること\_レベルまたはタイマー間隔経過すると、先に達した。 どちらがものでは最初に、いくつかの重要な作業を*StartIo*または ISR が DPC ルーチンによって削除されます。 だけです。

独立したよりもパフォーマンス特性が低下する非常にさまざまな機能を備えた 2 つの標準のドライバーのルーチンで使用される DPC がさらに、しなければ*CustomTimerDpc*と*CustomDpc*ルーチン。 DPC が原因となった条件に応じて、実行するために、どの操作を決定する必要があります、 *StartIo*ルーチンまたは ISR、キューに登録します。 DPC でこれらの条件のテストの追加 CPU サイクルを使用します。

 

 




