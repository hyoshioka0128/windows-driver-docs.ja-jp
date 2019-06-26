---
title: フレームワーク ロックの使用
description: フレームワーク ロックの使用
ms.assetid: d036a2d5-a9e9-4375-84b0-fbd797ee6f13
keywords:
- WDK KMDF の同期
- 同期ロック WDK KMDF
- ロックの WDK KMDF
- コールバックの同期ロック WDK KMDF
- スピン ロック WDK KMDF
- WDK KMDF のロックを待機します。
- 割り込みは、WDK KMDF をロックします。
- framework 割り込み WDK KMDF をロックします。
- framework 待機ロック WDK KMDF
- framework スピン ロック WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa124274bb6d6e7f39d1ff7d5754e78577b160e6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372261"
---
# <a name="using-framework-locks"></a>フレームワーク ロックの使用


場合がありますドライバーに加え、またはフレームワークが指定した同期の代わりとして、I/O 要求に関連するコールバック関数のドライバー固有の同期を提供する必要があります。 ドライバーがコールバックの同期ロックを使用して、スピンロック、ロックを待機し、ドライバーのコードを同期するロックを中断します。

### <a name="callback-synchronization-locks"></a>コールバックの同期ロック

フレームワークを使用するには、ドライバーを設定するかどうかは[自動同期](using-automatic-synchronization.md)ドライバーの I/O 要求に関連するイベントのコールバック関数を呼び出す前に、機能フレームワークの取得同期ロックします。

これら*コールバック同期ロック*、framework デバイス オブジェクトと、キュー オブジェクトに関連付けられている取得することもドライバー。 ドライバーの呼び出しで同期ロックを取得するのには[ **WdfObjectAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff548721)します。 ドライバーの呼び出し、ロックを解放する[ **WdfObjectReleaseLock**](https://msdn.microsoft.com/library/windows/hardware/ff548765)します。

ドライバーが I/O 要求に関連するコールバック関数のフレームワークのデバイス レベルまたはキュー レベルの同期を使用して、IRQL でを実行するコードを同期する必要がある場合は、コールバックの同期ロックを使用するには、ドライバーが必要な場合があります = パッシブ\_IRQL で実行するコールバック関数とレベル = ディスパッチ\_レベル。 これは、ため、ドライバーは、自動同期を使用して、同じ IRQL で実行されるコールバック関数に対してのみです。

たとえば、ドライバーの自動同期作業項目オブジェクトの場合のみ使用できます、作業項目オブジェクトの親の実行レベルは**WdfExecutionLevelPassive** (ために、作業項目のコールバック関数が常に実行されますIRQL = パッシブ\_レベル)。 そのため、ドライバーが指定されている場合**WdfExecutionLevelDispatch**で、 **ExecutionLevel**デバイス オブジェクトのメンバー [ **WDF\_オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfobject/ns-wdfobject-_wdf_object_attributes)構造、ドライバーを設定できません、 **AutomaticSerialization**子作業項目オブジェクトの構成構造体のメンバー。 代わりに、ドライバーが同期するコールバック同期ロックを取得する必要があります、 [ *EvtWorkItem* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)親デバイス オブジェクトのコールバック関数のコールバック関数。

### <a name="framework-wait-locks"></a>Framework 待機ロック

Framework 待機のロックを使用して、アクセスを同期する IRQL で実行されるコードからドライバーのデータを = パッシブ\_レベル。 ドライバーが framework 待機のロックを使用する前に呼び出す必要があります[ **WdfWaitLockCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfsync/nf-wdfsync-wdfwaitlockcreate)待機ロック オブジェクトを作成します。 ドライバーを呼び出すことが[ **WdfWaitLockAcquire** ](https://msdn.microsoft.com/library/windows/hardware/ff551168)ロックを取得および[ **WdfWaitLockRelease** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfsync/nf-wdfsync-wdfwaitlockrelease)を解放します。

### <a href="" id="framework-spin-locks"></a> Framework スピン ロック

Framework スピン ロックを使用して、IRQL で実行されるコードからドライバーのデータにアクセスを同期する&lt;= ディスパッチ\_レベル。 システムは、スレッドの IRQL をディスパッチに設定してドライバー スレッドは、スピン ロックを取得するときに\_レベル。 スレッドがロックを解放する場合、システムは、前のレベルに、スレッドの IRQL を復元します。

自動 framework の同期を使用していないドライバーは、スピン ロックを使用して、コンテキストの領域が書き込み可能で、スペースにアクセス数より多い場合、ドライバーのイベントのコールバック関数のいずれかの場合は、デバイス オブジェクトのコンテキストの領域へのアクセスを同期する可能性があります。

ドライバーが、framework スピン ロックを呼び出す必要がありますを使用する前に[ **WdfSpinLockCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfsync/nf-wdfsync-wdfspinlockcreate)スピン ロック オブジェクトを作成します。 ドライバーを呼び出すことが[ **WdfSpinLockAcquire** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))ロックを取得および[ **WdfSpinLockRelease** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550044(v=vs.85))を解放します。

スピン ロックの使用例については、次を参照してください。[送信要求のキャンセルの同期](synchronizing-cancellation-of-sent-requests.md)します。

### <a name="framework-interrupt-locks"></a>フレームワークの割り込みのロック

DIRQL をサポートする割り込みオブジェクトの割り込み処理、framework 割り込みロックはスピン ロックです。 ドライバーは、割り込みスピン ロックを取得、後に、ロックを解放するまで、デバイスの DIRQL でドライバーを実行します。 詳細については、割り込みのロックを使用して、次を参照してください。[同期割り込みコード](synchronizing-interrupt-code.md)します。

パッシブ レベルの処理をサポートする割り込みオブジェクト、framework 割り込みロックはロックを待機します。 ドライバーは IRQL で、実行後に、ドライバーは、割り込み待機ロックを取得、パッシブ =\_レベルのロックを解放するまでです。 パッシブ レベルの処理の詳細については、次を参照してください。[パッシブ レベルをサポートしている中断](supporting-passive-level-interrupts.md)します。

 

 





