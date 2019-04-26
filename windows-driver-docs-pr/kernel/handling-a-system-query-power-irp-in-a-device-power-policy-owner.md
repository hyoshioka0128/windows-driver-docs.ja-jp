---
title: デバイス電源ポリシー オーナーでのシステム電源クエリ IRP の処理
description: デバイス電源ポリシー オーナーでのシステム電源クエリ IRP の処理
ms.assetid: 680e3be2-63d9-4d79-a7c0-422e852e9347
keywords:
- クエリ power Irp WDK の電源管理
- デバイスの電源ポリシー所有者 WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39f3e36ce6f240d400449f9f160a1c81527f9ef6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359822"
---
# <a name="handling-a-system-query-power-irp-in-a-device-power-policy-owner"></a>デバイス電源ポリシー オーナーでのシステム電源クエリ IRP の処理





デバイスの電源ポリシー所有者が受信すると、 [ **IRP\_MN\_クエリ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff551699)のシステム電源の状態をクエリの速度と、を渡すことによって応答[*IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)日常的な送信、 **IRP\_MN\_クエリ\_POWER**デバイスの電源状態にします。 スタック内のすべてのドライバーには、デバイス クエリが完了したら、デバイスの電源ポリシー所有者は、システムのクエリを完了します。

デバイスの電源ポリシー所有者、次の手順を実行する必要があります、 [DispatchPower ルーチン](dispatchpower-routines.md)システム クエリに応答します。

1.  呼び出す[ **IoAcquireRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff548204)、ドライバーが、PnP されませんが受け取るようにする、現在の IRP を渡して[ **IRP\_MN\_の削除\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551738) power IRP の処理中に要求します。

    場合**IoAcquireRemoveLock** 、エラー状態が返されるドライバーは IRP の処理を続行しないでください。 代わりに、Windows Vista 以降、ドライバー、呼び出す必要があります[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343) IRP を完了して、エラー状態を返すにします。 ドライバーが呼び出すサーバーの Windows Server 2003、Windows XP、および Windows 2000、 [ **PoStartNextPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559776)、呼び出す**IoCompleteRequest** IRP の完了を返す、エラー状態です。

2.  ドライバーが、クエリ対象のシステム電源の状態をサポートできることを確認する」の説明に従って[フィルターまたは関数のドライバーで、システム クエリ性能の IRP を失敗](failing-a-system-query-power-irp-in-a-filter-or-function-driver.md)します。 ない場合は、そのセクションで説明した IRP がエラー状態を完了します。

    ただし、ドライバーをする必要があります失敗しないクエリ s4 (**PowerSystemHibernate**) 場合はウェイク アップのデバイスが有効になっているが、システムを休止状態からのスリープを解除できません。 この場合は、ドライバーの電源ポリシー所有者 (送信先となる、 [ **IRP\_MN\_待機\_WAKE**](https://msdn.microsoft.com/library/windows/hardware/ff551766)) 待機/ウェイク IRP をキャンセルし、システムのクエリが成功する必要があります。 詳細については、次を参照してください。[待機/ウェイク IRP のキャンセル](canceling-a-wait-wake-irp.md)します。

3.  場合は、ドライバーは、クエリ対象のシステム電源の状態をサポートできますが、呼び出す[ **IoMarkIrpPending**](https://msdn.microsoft.com/library/windows/hardware/ff549422)します。

4.  呼び出すことによって、次の下位のドライバーの IRP スタックの場所を設定[ **IoCopyCurrentIrpStackLocationToNext**](https://msdn.microsoft.com/library/windows/hardware/ff548387)します。

5.  設定、 *IoCompletion*システム クエリ power IRP のルーチンです。

6.  呼び出す[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336) (で Windows 7 および Windows Vista の場合) または[ **PoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff559654) (で Windows Server 2003、Windows XP、および Windows 2000)次の下位ドライバーには、IRP を渡す。

7.  状態を返す\_保留します。

[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチンは、次を行う必要があります。

1.  確認**Irp -&gt;IoStatus.Status**に下位のドライバーが IRP を正常に完了したことを確認します。 下位のドライバーには、非成功 NTSTATUS 値が指定した場合、 *IoCompletion*ルーチンが NTSTATUS 値を返す必要があります。

2.  呼び出す場合、下位のドライバーは IRP を正常に完了しました、 [ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734)クエリ power IRP のクエリ対象のシステムに対して有効であるデバイスの電源状態の電源の状態、デバイスを送信します。 必要に応じて、デバイスを参照してください\_状態配列で、 [**デバイス\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)クエリ対象のシステム電源の有効などのデバイスの電源状態を確認する構造体。状態。

3.  コールバック ルーチンを指定 (*CompletionFunction*パラメーター) への呼び出しで**PoRequestPowerIrp**システム IRP を渡すとで、*コンテキスト*領域。

4.  状態を返す\_詳細\_処理\_のために必要なドライバーは、コールバック ルーチンで、システム クエリ IRP の処理を終了できるようにします。

IRP が完了した後、すべて*IoCompletion* IRP の処理中に設定するルーチンを実行した電源マネージャー、I/O マネージャーを通じて、電源ポリシー マネージャーのコールバック ルーチンを呼び出す (、 *CompletionFunction*パラメーターを**PoRequestPowerIrp**)。 コールバック ルーチンでは、さらに、必要があります以下に示します。

1.  呼び出す[ **PoStartNextPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559776) IRP の [次へ] のパワーを開始します。 (Windows Server 2003、Windows XP、および Windows 2000 のみ。)

2.  完了、システム クエリ power IRP (呼び出し[ **IoCompleteRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548343)) デバイスに対して返される状態クエリ power IRP。

3.  呼び出す[ **IoReleaseRemoveLock** ](https://msdn.microsoft.com/library/windows/hardware/ff549560)を以前に取得したロックを解放します。

デバイスの電源ポリシーの所有者だけでなく、デバイスのクエリを送信しますがもデバイス スタックには、その方法で処理する必要がありますに注意してください。 詳細については、次を参照してください。 [IRP の処理\_MN\_クエリ\_デバイスの電源状態のための電力](handling-irp-mn-query-power-for-device-power-states.md)します。

 

 




