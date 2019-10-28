---
title: フレームワーク ロックの使用
description: フレームワーク ロックの使用
ms.assetid: d036a2d5-a9e9-4375-84b0-fbd797ee6f13
keywords:
- WDK KMDF の同期
- 同期ロック WDK KMDF
- WDK KMDF のロック
- コールバック同期による WDK KMDF のロック
- スピンロック WDK KMDF
- wait locks WDK KMDF
- 中断ロック WDK KMDF
- フレームワークの割り込みロック WDK KMDF
- framework wait locks WDK KMDF
- フレームワークスピンロック WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 106603e3ad46679553896d7b3a9b6c8a65c3985c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843085"
---
# <a name="using-framework-locks"></a>フレームワーク ロックの使用


場合によっては、フレームワークによって提供される同期の代わりに、またはの代替として、i/o 要求に関連するコールバック関数のドライバー固有の同期をドライバーが提供する必要があります。 ドライバーは、コールバック同期ロック、スピンロック、待機ロック、および割り込みロックを使用してドライバーコードを同期できます。

### <a name="callback-synchronization-locks"></a>コールバック同期ロック

フレームワークの[自動同期](using-automatic-synchronization.md)機能を使用するようにドライバーを設定した場合、フレームワークは、ドライバーの i/o 要求に関連するイベントコールバック関数を呼び出す前に、同期ロックを取得します。

これらの*コールバック同期ロック*は、フレームワークのデバイスオブジェクトとキューオブジェクトに関連付けられており、ドライバーで取得することもできます。 同期ロックを取得するために、ドライバーは[**WdfObjectAcquireLock**](https://msdn.microsoft.com/library/windows/hardware/ff548721)を呼び出します。 ロックを解除するには、ドライバーは[**Wdfobjectreleaselock**](https://msdn.microsoft.com/library/windows/hardware/ff548765)を呼び出します。

ドライバーが、i/o 要求関連のコールバック関数のフレームワークのデバイスレベルまたはキューレベルの同期を使用するが、IRQL =\_PASSIVE で実行される一部のコードを同期する必要がある場合は、ドライバーでコールバック同期ロックを使用することができます。IRQL = ディスパッチ\_レベルで実行されるコールバック関数を使用したレベル。 これは、ドライバーが自動同期を使用できるのは、同じ IRQL で実行されるコールバック関数に対してのみであるためです。

たとえば、作業項目オブジェクトの親の実行レベルが**Wdfexecutionlevelpassive** (作業項目のコールバック関数が常に IRQL =\_PASSIVE で実行されるため) である場合にのみ、ドライバーは作業項目オブジェクトに対して自動同期を使用できます。レベル)。 このため、ドライバーがデバイスオブジェクトの[**WDF\_オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)構造の**executionlevel**メンバーで**wdfexecutionleveldispatch**を指定した場合、ドライバーは自動**シリアル化**を設定できません。子作業項目オブジェクトの構成構造のメンバー。 代わりに、ドライバーは、 [*Evtworkitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfworkitem/nc-wdfworkitem-evt_wdf_workitem)コールバック関数と親デバイスオブジェクトのコールバック関数を同期するコールバック同期ロックを取得する必要があります。

### <a name="framework-wait-locks"></a>フレームワークの待機ロック

IRQL = パッシブ\_レベルで実行されるコードからドライバーデータへのアクセスを同期するには、フレームワークの待機ロックを使用します。 ドライバーは、フレームワークの待機ロックを使用できるようにするために、 [**Wdfwaitlockcreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockcreate)を呼び出して、待機ロックオブジェクトを作成する必要があります。 次に、ドライバーは[**Wdfwaitlockacquire**](https://msdn.microsoft.com/library/windows/hardware/ff551168)を呼び出して、ロックと[**wdfwaitlockacquire**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockrelease)を取得して解放します。

### <a href="" id="framework-spin-locks"></a>フレームワークのスピンロック

.Net framework スピンロックを使用して、IRQL &lt;= ディスパッチ\_レベルで実行されるコードからドライバーデータへのアクセスを同期します。 ドライバースレッドがスピンロックを取得すると、システムはスレッドの IRQL をディスパッチ\_レベルに設定します。 スレッドがロックを解放すると、システムはスレッドの IRQL を前のレベルに復元します。

自動フレームワーク同期を使用しないドライバーでは、コンテキスト空間が書き込み可能で、ドライバーのイベントコールバック関数の1つ以上が領域にアクセスする場合、スピンロックを使用してデバイスオブジェクトのコンテキスト空間へのアクセスを同期することがあります。

ドライバーがフレームワークのスピンロックを使用できるようにするには、まず[**WdfSpinLockCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfspinlockcreate)を呼び出して、スピンロックオブジェクトを作成する必要があります。 次に、ドライバーは[**WdfSpinLockAcquire**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))を呼び出してロックを取得し、 [**WdfSpinLockRelease**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550044(v=vs.85))を解放します。

スピンロックの使用例については、「[送信された要求のキャンセルの同期](synchronizing-cancellation-of-sent-requests.md)」を参照してください。

### <a name="framework-interrupt-locks"></a>フレームワークの割り込みロック

DIRQL 割り込み処理をサポートする interrupt オブジェクトの場合、フレームワークの割り込みロックはスピンロックです。 ドライバーは、割り込みスピンロックを取得した後、デバイスの DIRQL でロックを解除するまで実行します。 割り込みロックの使用の詳細については、「[割り込みコードの同期](synchronizing-interrupt-code.md)」を参照してください。

パッシブレベルの処理をサポートする interrupt オブジェクトの場合、フレームワークの割り込みロックは待機ロックです。 ドライバーは、割り込み待機ロックを取得した後、ロックを解放するまで、IRQL = パッシブ\_レベルで実行されます。 パッシブレベルの処理の詳細については、「[パッシブレベルの割り込みのサポート](supporting-passive-level-interrupts.md)」を参照してください。

 

 





