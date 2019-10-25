---
title: IRP_MN_WAIT_WAKE
description: この IRP により、ドライバーはスリープ状態のシステムを停止したり、スリープ状態のデバイスをスリープ解除したりすることができます。
ms.date: 08/12/2017
ms.assetid: b79fd057-bf95-457e-882a-42221789e6e6
keywords:
- IRP_MN_WAIT_WAKE カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: fb4d5364c4ecde5f255ffea117ed2533f0b3cad9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827936"
---
# <a name="irp_mn_wait_wake"></a>IRP\_\_待機\_ウェイク


この IRP により、ドライバーはスリープ状態のシステムを停止したり、スリープ状態のデバイスをスリープ解除したりすることができます。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_の電源**](irp-mj-power.md)送信時
---------

電源ポリシーを所有するドライバーは、この IRP を PDO にターゲットとして、着信通話などの外部イベントに応答してデバイスを目覚めできるようにします。 ドライバーは、この IRP を送信するために[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)を呼び出す必要があります。

一般的な規則として、ドライバーは、デバイスをウェイクアップ用に有効にする必要があると判断したら、直ちにこの IRP を送信する必要があります。 そのため、ほとんどのデバイスのドライバーは、デバイスの電源を入れた後、Irp\_が完了する前にこの IRP を送信し、 [ **\_デバイス要求を開始\_** ](irp-mn-start-device.md)ます。

ただし、ドライバーは、デバイスが動作状態 (**PowerDeviceD0**) になるといつでも IRP を送信できます。 デバイススタックを移行中にすることはできません。つまり、ドライバーは、デバイススタックで他の電源 IRP がアクティブになっている間、 **\_待機\_スリープ状態**にすることはできません\_。

待機/ウェイク IRP は、デバイスまたはシステムの電源状態を変更しません。 デバイスからウェイクアップ信号を有効にするだけです。 ウェイクアップシグナルが到着したら、ポリシー所有者は**PoRequestPowerIrp**を呼び出して、そのデバイスを D0 に返す set-power IRP を送信する必要があります。

この IRP を送信するには、ドライバーが IRQL = パッシブ\_レベルで実行されている必要があります。 ただし、IRP は IRQL = ディスパッチ\_レベルで完了できます。

## <a name="input-parameters"></a>入力パラメーター


<a href="" id="parameters-waitwake-powerstate-contains-the-lowest--least-powered--system-power-state-from-which-the-device-should-be-allowed-to-awaken-the-system-"></a>**PowerState**には、デバイスがシステムをウェイクアップできる最も低い (電力が低い) システム電源の状態が含まれています。  

## <a name="output-parameters"></a>出力パラメーター


なし。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーは、 **Irp&gt;iostatus. status**を次のいずれかに設定します。

<a href="" id="status-pending-"></a>状態\_保留中   
ドライバーは IRP を受信し、デバイスがウェイクアップを通知するのを待機しています。

<a href="" id="status-invalid-device-state-"></a>状態\_無効\_デバイス\_の状態   
デバイスのデバイス[ **\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の構造に指定されている**devicewake**の状態よりも、デバイスの電源がオフになっている状態であるか、またはデバイスが IRP で渡された**systemwake**状態からシステムを目覚めできません。

<a href="" id="status-not-supported-"></a>ステータス\_\_サポートされていません   
デバイスはウェイクアップをサポートしていません。

<a href="" id="status-device-busy-"></a>状態\_デバイス\_ビジー状態です   
**Irp\_\_待機\_ウェイク**要求が既に保留中であるため、別の irp\_\_完了していないと、ウェイクアップ要求を発行できるようになる前に、完了またはキャンセルする必要があります。

<a href="" id="status-success"></a>状態\_成功  
デバイスがウェイクアップイベントを通知しました。

<a href="" id="status-cancelled"></a>状態\_取り消されました  
IRP はキャンセルされました。

ドライバーがこの IRP を失敗させる必要がある場合、IRP は直ちに完了し、次の下位のドライバーには IRP が渡されません。

<a name="operation"></a>操作
---------

ドライバーは、次の2つのいずれかの理由により、 **IRP\_\_待機\_ウェイクアップ**を送信します。

1.  外部ウェイクアップシグナルに応答してスリープ状態のシステムをそのデバイスがウェイクアップできるようにします。

2.  外部ウェイクアップシグナルに応答してデバイスがデバイスのスリープ状態から復帰できるようにする。

IRP はデバイスのバスドライバーにデバイススタックを渡す必要があります。これにより[**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)が呼び出され、 [*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンから保留中のステータス\_が返されます。 IRP は、ウェイクアップシグナルが発生するか、IRP を送信したドライバーがキャンセルされるまで保留状態のままになります。

特定の時点では、PDO に対して保留中の待機/ウェイク IRP は1つだけです。 ドライバーが PDO 用の待機/ウェイク IRP を既に保持している場合は、状態\_デバイス\_ビジー状態のその他の Irp をすべて失敗させる必要があります。 複数の子 PDO を列挙するドライバーは、そのような PDO ごとに待機/ウェイク IRP を保留にすることができます。

各ドライバーは、IRP がデバイススタックを移動するときに[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定します。 デバイスがウェイクアップイベントを通知すると、バスドライバーはウェイクアップシグナルを処理し、IRP を完了して、STATUS\_SUCCESS を返します。 次に、i/o マネージャーは、次に上位のドライバーの*Iocompletion*ルーチンを呼び出します。

ドライバーが待機/ウェイク IRP を送信する場合、 **PoRequestPowerIrp**呼び出しでコールバックルーチンを指定する必要があります。 コールバックルーチンでは、ドライバーは通常、デバイスをサービスします。 たとえば、デバイスの電源ポリシー所有者は、 **PoRequestPowerIrp**を呼び出して、デバイスの状態が D0 の[ **\_電源\_設定**](irp-mn-set-power.md)された IRP\_送信する必要があります。

1つのデバイスのバスドライバーとして機能するドライバーと親デバイスのポリシー所有者が irp を完了したことを示す irp\_を要求した場合は、\_ウェイクアップ irp\_を受信したときに、親のデバイススタックに対して **\_待機**\_ます。子 PDO からの 7_ WAKE 要求。 ドライバーが複数の子 PDO を列挙する場合は、子 PDOs が待機/ウェイク要求を送信する回数にかかわらず、親のデバイススタックに対して待機/ウェイクアップ IRP を1つだけ要求する必要があります。 代わりに、このようなドライバーでは、要求を受信するたびにカウントをインクリメントし、要求が完了するたびにカウントをデクリメントすることで、待機またはスリープ状態の Irp の内部カウントを保持する必要があります。 待機/ウェイク IRP を完了した後にカウントが0以外の場合、ドライバーはデバイススタックに別の待機/ウェイク IRP を送信して、ウェイクアップ用に "rearm" 自体を送信する必要があります。 詳細については、「[デバイスツリーを使用した待機/ウェイク irp のパスについ](https://docs.microsoft.com/windows-hardware/drivers/kernel/understanding-the-path-of-wait-wake-irps-through-a-device-tree)て」を参照してください。

**IRP\_完了\_** を取り消すには、\_ウェイクを待機します。ドライバーは[**Iocancelirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)を呼び出します。 IRP を開始したドライバーだけがキャンセルできます。 ドライバーは、次のいずれかが発生したときに、保留中の**IRP\_完了\_待機\_解除**します。

-   ドライバーは、デバイスを停止または削除する PnP IRP を受信します。

-   システムはスリープ状態になり、デバイスのウェイクアップ信号はスリープ解除できません。

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
<td>Wdm (Wdm .h、Ntddk、または Ntifs を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)

 

 




