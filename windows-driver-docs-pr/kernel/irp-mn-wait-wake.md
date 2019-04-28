---
title: IRP_MN_WAIT_WAKE
description: この IRP では、スリープ状態のシステムがスリープ解除したり、スリープ状態のデバイスがスリープ解除するドライバーを使用できます。
ms.date: 08/12/2017
ms.assetid: b79fd057-bf95-457e-882a-42221789e6e6
keywords:
- IRP_MN_WAIT_WAKE カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: ee57b89cba2d0aeefee1621ab9c1f42182896d3e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381396"
---
# <a name="irpmnwaitwake"></a>IRP\_MN\_WAIT\_WAKE


この IRP では、スリープ状態のシステムがスリープ解除したり、スリープ状態のデバイスがスリープ解除するドライバーを使用できます。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_POWER** ](irp-mj-power.md)送信されるときに
---------

電源ポリシーを所有しているドライバーでは、着信呼び出しなどの外部イベントに応答がスリープ解除するには、そのデバイスを有効にするには、その PDO この IRP が対象とします。 ドライバーを呼び出す必要があります[ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734)この IRP を送信します。

一般的な規則として、ドライバーはウェイク アップのデバイスを有効にすることに決定するとすぐにこの IRP を送信する必要があります。 このようなほとんどのデバイス ドライバーが完了する前に自分のデバイスで強化後にこの IRP を送信するその結果、 [ **IRP\_MN\_開始\_デバイス**](irp-mn-start-device.md)要求.

ただし、ドライバーが動作中にいつでも、デバイスが IRP を送信する (**PowerDeviceD0**)。 デバイス スタックは遷移; に存在しません。これは、ドライバーは送信しないでください、 **IRP\_MN\_待機\_WAKE**他 power IRP がそのデバイス スタックのアクティブな状態です。

待機/ウェイク IRP では、デバイスまたはシステムの電源の状態は変更されません。 デバイスからウェイク アップの信号だけができます。 ウェイク アップのシグナルを受け取ったときに、ポリシーの所有者を呼び出す必要があります**PoRequestPowerIrp** D0 にそのデバイスを返すセット power IRP を送信します。

IRQL でドライバーを実行する必要があります = パッシブ\_この IRP を送信するレベル。 ただし、IRP を IRQL で完了できます = ディスパッチ\_レベル。

## <a name="input-parameters"></a>入力パラメーター


<a href="" id="parameters-waitwake-powerstate-contains-the-lowest--least-powered--system-power-state-from-which-the-device-should-be-allowed-to-awaken-the-system-"></a>**Parameters.WaitWake.PowerState**元は、システムがスリープ解除するデバイスを許可する最低 (最小を利用した) システム電源の状態が含まれています。  

## <a name="output-parameters"></a>出力パラメーター


なし。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーの設定**Irp -&gt;IoStatus.Status**次のいずれか。

<a href="" id="status-pending-"></a>ステータス\_PENDING   
ドライバーは IRP を受信し、ウェイク アップの通知をデバイスが待機しています。

<a href="" id="status-invalid-device-state-"></a>ステータス\_無効な\_デバイス\_状態   
デバイスがよりも低い電源の状態、 **DeviceWake**に指定された状態、 [**デバイス\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff543095)デバイスまたはデバイスの構造システムがスリープ解除できない、 **SystemWake** IRP で渡される状態。

<a href="" id="status-not-supported-"></a>ステータス\_いない\_サポートされています。   
デバイスは、ウェイク アップをサポートしていません。

<a href="" id="status-device-busy-"></a>ステータス\_デバイス\_ビジー   
**IRP\_MN\_待機\_WAKE**要求が既に保留中と完了または別の IRP の前にキャンセルする必要があります\_MN\_待機\_スリープ解除要求を指定できます発行されます。

<a href="" id="status-success"></a>ステータス\_成功  
デバイスには、ウェイク イベントがシグナル状態します。

<a href="" id="status-cancelled"></a>ステータス\_キャンセル  
IRP が取り消されました。

ドライバーには、この IRP が失敗した場合必要があります、IRP を直ちに完了して、IRP を次の下位ドライバーにパスしませんでした。

<a name="operation"></a>操作
---------

ドライバーの送信**IRP\_MN\_待機\_WAKE** 2 つの理由のいずれかの。

1.  外部のウェイク アップ シグナルへの応答中のシステムがスリープ解除するには、そのデバイスを有効にするには

2.  外部のウェイク アップ シグナルへの応答でデバイスのスリープ状態から再開するには、そのデバイスを有効にするには

呼び出すと、デバイスのバス ドライバーに IRP デバイス スタックを渡す必要がある[ **IoMarkIrpPending** ](https://msdn.microsoft.com/library/windows/hardware/ff549422)ステータスを返す\_から PENDING その[ *DispatchPower* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン。 保留中の IRP がドライバー IRP を送信するまで、ウェイク アップのシグナルが発生するまでまたはキャンセルします。

1 つだけ待機/ウェイク IRP 保持できる保留中の PDO の特定の時点。 ドライバーは、PDO の待機/ウェイク IRP を既に保持している、追加される、失敗状態でこのような Irp\_デバイス\_ビジーです。 1 つ以上の子の PDO を列挙するドライバーには、このような各 PDO の待機/ウェイク IRP の保留ことができます。

各ドライバーの設定、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチンの IRP がデバイス スタックを下へ移動します。 バス ドライバーがウェイク アップの信号をサービスし、状態を返す、IRP が完了すると、デバイスがウェイク アップ イベント、シグナル、ときに\_成功します。 I/O マネージャーを呼び出して、 *IoCompletion*デバイス スタックまで、[次へ] 以上のドライバーの日常的な。

内のコールバック ルーチンを指定する必要があります、ドライバーは、待機/ウェイク IRP を送信するとき、 **PoRequestPowerIrp**呼び出します。 コールバック ルーチンで、ドライバーは、デバイスを通常サービスです。 たとえば、デバイスの電源ポリシーの所有者を呼び出す必要があります**PoRequestPowerIrp**を送信する、 [ **IRP\_MN\_設定\_POWER** ](irp-mn-set-power.md)D0 の状態のデバイス。

1 つのデバイスのバス ドライバーと親デバイスのポリシーの所有者として動作するドライバーは、要求、 **IRP\_MN\_待機\_WAKE** を受信したときに、親のデバイススタックのIRP**IRP\_MN\_待機\_WAKE** PDO 子からの要求。 ドライバーは、1 つ以上の子の PDO を列挙する場合 1 つだけ待機/ウェイク IRP の子 Pdo 送信待機またはスリープ解除要求の数に関係なく、親のデバイス スタックを要求する必要があります。 代わりに、このようなドライバーが待機/ウェイク Irp の内部でカウントを保持する必要があります、毎回インクリメント受信要求とカウントをデクリメントする操作を要求を完了するたびにします。 待機/ウェイク IRP の完了後に、カウントが 0 以外の場合、ドライバーは"rearm"自体のウェイク アップするもう 1 つの待機またはスリープ解除 IRP をそのデバイス スタックに送信する必要があります。 詳細については、次を参照してください。[デバイス ツリーを通じて待機/ウェイク Irp のパスを理解する](https://msdn.microsoft.com/library/windows/hardware/ff564867)します。

キャンセル、 **IRP\_MN\_待機\_WAKE**、ドライバーを呼び出す[ **IoCancelIrp**](https://msdn.microsoft.com/library/windows/hardware/ff548338)。 IRP を発生させたドライバーだけをキャンセルできます。 ドライバーをキャンセル、保留中**IRP\_MN\_待機\_WAKE**次のいずれかに発生します。

-   ドライバーは、停止するか、デバイスを削除する PnP IRP を受信します。

-   システムがスリープ状態になると、デバイスのウェイク信号で再開しない必要があります。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h など)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**PoRequestPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559734)

 

 




