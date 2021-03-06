---
title: タイマー精度
description: システム タイマーのルーチンには、通常、タイマーの絶対パスまたは相対的な有効期限の時間のいずれかを指定する呼び出し元ことができます。
ms.assetid: CA29DC02-1AEA-4A13-B2D6-8C8052E21EDB
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 10ee2a2218d97986f86a70cc0551b5bdabf061dd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382960"
---
# <a name="timer-accuracy"></a>タイマー精度


システム タイマーのルーチンには、通常、タイマーの絶対パスまたは相対的な有効期限の時間のいずれかを指定する呼び出し元ことができます。 たとえばを参照してください[ **kewaitforsingleobject の 1**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)、 [ **KeSetTimer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kesettimer)、または[ **KeDelayExecutionThread**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kedelayexecutionthread)します。 オペレーティング システムを有効期限の時間を測定できます精度は、システム クロックの粒度によって制限されます。

システム時刻は、システム クロックを刻むごとに更新されの最新のティック精度です。 呼び出し元は、絶対有効期限を指定する場合は、指定した時間後に発生する最初のシステム クロック ティックの処理中に、タイマーの有効期限が検出されました。 したがって、タイマーは、1 つとしてシステム クロック期間を指定した絶対有効期限より後を有効期限が切れることができます。 有効期限が、期間まで発生する可能性がタイマーの間隔、または相対的な有効期限の時間が代わりに指定されて場合よりも前またはシステム クロックのティック間この間隔の開始および終了時刻だけを分類する場所に応じて、指定された期間より後の期間。 絶対パスまたは相対時刻が指定するかどうかに関係なくタイマーの期限可能性がありますまで検出されませんも後で割り込みが他のデバイスの処理で割り込みシステム クロックの処理が遅延される場合。

呼び出し元は、相対的な有効期限の時間を指定する場合、タイマー ルーチンは、タイマーを使用する絶対有効期限の時間を計算する相対的な有効期限を指定した時間に現在のシステム クロックの時刻を追加します。 システム時刻は、システム クロックの最新の目盛りにのみ正確であるために、システム クロックの期間、呼び出し元で想定されている有効期限の時刻より前まで、計算される有効期間を引き起こすことができます。 指定した相対的な有効期限に近いか、システム クロックの期間よりも小さい場合は、タイマーが期限切れ直後に、遅延なしで。

正確に短い有効期限をサポートするために可能な方法は、システム クロックのティック間の時間を短縮するが、電力消費量が増加する可能性があります。 さらに、システム クロックの期間を減らすこと可能性があります確実に実現できないシステム クロック粒度の細かいしない限り、システム クロック割り込みの処理に遅延が割り込み、他のデバイス プラットフォームでの処理を保証できます。

Windows 8 では、以降では[ **KeDelayExecutionThread** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kedelayexecutionthread)より正確な手法を使用して、相対的な有効期限の呼び出し元が指定した時間から絶対有効期限の時間を計算します。 最初に、現在のシステム時刻のより正確な推定値を取得する日常的な使用時間を測定するシステムのパフォーマンス カウンターが最後のシステムから経過したクロック ティック。 次に、ルーチンでは、絶対有効期限の時間を計算する相対的な有効期限の時間に、システム時刻のこのより正確な見積もりを追加します。 この手法によって計算された絶対有効期限の時間はマイクロ秒内に正確です。 その結果、タイマーは期限切れ、指定した相対的な有効期限が経過する前にします。 タイマーは、システム クロックの期間、指定された期間よりも後まで期限を切ることもと有効期限が後でも割り込みの他のデバイスの処理でシステム クロック割り込みの処理が遅延される場合。

タイマーの有効期限が切れる前に、システム時刻が変更された場合は、相対タイマーが影響を受けませんが、システムを調整します。 各絶対タイマー。 相対的なタイマーは、絶対のシステム時刻に関係なく、指定された時間単位数が経過した後に常に有効期限です。 タイマーを絶対有効期限が切れる、特定のシステムでので絶対のタイマーの待機時間、システム時刻の変更で変更します。

 

 




