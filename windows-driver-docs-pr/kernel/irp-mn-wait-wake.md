---
title: IRP_MN_WAIT_WAKE
description: この IRP により、ドライバーはスリープ状態のシステムを停止したり、スリープ状態のデバイスをスリープ解除したりすることができます。
ms.date: 08/12/2017
ms.assetid: b79fd057-bf95-457e-882a-42221789e6e6
keywords:
- IRP_MN_WAIT_WAKE カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: aad937a133a985389935178f700145bdf05f362f
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922551"
---
# <a name="irp_mn_wait_wake"></a>IRP\_の\_最大\_待機復帰


この IRP により、ドライバーはスリープ状態のシステムを停止したり、スリープ状態のデバイスをスリープ解除したりすることができます。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_の電源**](irp-mj-power.md)

<a name="when-sent"></a>送信時
---------

電源ポリシーを所有するドライバーは、この IRP を PDO にターゲットとして、着信通話などの外部イベントに応答してデバイスを目覚めできるようにします。 ドライバーは、この IRP を送信するために[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)を呼び出す必要があります。

一般的な規則として、ドライバーは、デバイスをウェイクアップ用に有効にする必要があると判断したら、直ちにこの IRP を送信する必要があります。 そのため、ほとんどのデバイスのドライバーは、デバイスの電源を入れた後、 [**irp\_の "\_デバイス\_の開始**](irp-mn-start-device.md)" 要求を完了する前に、この irp を送信します。

ただし、ドライバーは、デバイスが動作状態 (**PowerDeviceD0**) になるといつでも IRP を送信できます。 デバイススタックを移行中にすることはできません。つまり、他のすべての電源 IRP がデバイススタックでアクティブになっている間は、ドライバーが**IRP\_の\_待機状態の待機\_** を送信することはできません。

待機/ウェイク IRP は、デバイスまたはシステムの電源状態を変更しません。 デバイスからウェイクアップ信号を有効にするだけです。 ウェイクアップシグナルが到着したら、ポリシー所有者は**PoRequestPowerIrp**を呼び出して、そのデバイスを D0 に返す set-power IRP を送信する必要があります。

この IRP を送信するには、ドライバー\_が IRQL = パッシブレベルで実行されている必要があります。 ただし、IRP は IRQL = ディスパッチ\_レベルで完了できます。

## <a name="input-parameters"></a>入力パラメーター


<a href="" id="parameters-waitwake-powerstate-contains-the-lowest--least-powered--system-power-state-from-which-the-device-should-be-allowed-to-awaken-the-system-"></a>**PowerState**には、デバイスがシステムをウェイクアップできる最も低い (電力が低い) システム電源の状態が含まれています。  

## <a name="output-parameters"></a>出力パラメーター


ありません。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーは、次のいずれかの状態に設定**&gt;されます。**

<a href="" id="status-pending-"></a>状態\_保留中   
ドライバーは IRP を受信し、デバイスがウェイクアップを通知するのを待機しています。

<a href="" id="status-invalid-device-state-"></a>デバイス\_\_の\_状態が無効です   
デバイスのデバイス[**\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の構造に指定されている**devicewake**状態よりもデバイスの電源がオフになっているか、IRP で渡された**systemwake**状態からシステムをウェイクアップできません。

<a href="" id="status-not-supported-"></a>サポート\_さ\_れていない状態   
デバイスはウェイクアップをサポートしていません。

<a href="" id="status-device-busy-"></a>状態\_デバイス\_がビジーです   
**Irp\_の最大\_待機\_のウェイク**要求は既に保留中であるため、別の\_irp\_の\_待機時間の wake 要求を発行する前に完了するか、取り消す必要があります。

<a href="" id="status-success"></a>成功\_の状態  
デバイスがウェイクアップイベントを通知しました。

<a href="" id="status-cancelled"></a>取り消さ\_れた状態  
IRP はキャンセルされました。

ドライバーがこの IRP を失敗させる必要がある場合、IRP は直ちに完了し、次の下位のドライバーには IRP が渡されません。

<a name="operation"></a>Operation
---------

ドライバーは、次の2つの理由のいずれかにより、 **\_IRP\_を\_待機状態**にすることができます。

1.  外部ウェイクアップシグナルに応答してスリープ状態のシステムをそのデバイスがウェイクアップできるようにします。

2.  外部ウェイクアップシグナルに応答してデバイスがデバイスのスリープ状態から復帰できるようにする。

IRP はデバイスのバスドライバーにデバイススタックを渡す必要があります。これは[**Iomarkirppending**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)を呼び出し、\_ [*DispatchPower*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンから PENDING 状態を返します。 IRP は、ウェイクアップシグナルが発生するか、IRP を送信したドライバーがキャンセルされるまで保留状態のままになります。

特定の時点では、PDO に対して保留中の待機/ウェイク IRP は1つだけです。 ドライバーが PDO の待機/ウェイク IRP を既に保持している場合は、状態\_が [\_ビジー] の irp を追加する必要があります。 複数の子 PDO を列挙するドライバーは、そのような PDO ごとに待機/ウェイク IRP を保留にすることができます。

各ドライバーは、IRP がデバイススタックを移動するときに[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定します。 デバイスがウェイクアップイベントを通知すると、バスドライバーはウェイクアップシグナルを処理し、IRP を完了して状態\_の成功を返します。 次に、i/o マネージャーは、次に上位のドライバーの*Iocompletion*ルーチンを呼び出します。

ドライバーが待機/ウェイク IRP を送信する場合、 **PoRequestPowerIrp**呼び出しでコールバックルーチンを指定する必要があります。 コールバックルーチンでは、ドライバーは通常、デバイスをサービスします。 たとえば、デバイスの電源ポリシー所有者は、 **PoRequestPowerIrp**を呼び出して、デバイスの状態が D0 になるように[**IRP\_\_\_**](irp-mn-set-power.md)を使用した電源を送信する必要があります。

1つのデバイスのバスドライバーとして機能し、親デバイスのポリシー所有者は、子 PDO から**irp\_\_の2待機\_ウェイク**要求を受信したときに、親のデバイススタックに対して irp **\_\_\_** を使用した待機ウェイク irp を要求します。 ドライバーが複数の子 PDO を列挙する場合は、子 PDOs が待機/ウェイク要求を送信する回数にかかわらず、親のデバイススタックに対して待機/ウェイクアップ IRP を1つだけ要求する必要があります。 代わりに、このようなドライバーでは、要求を受信するたびにカウントをインクリメントし、要求が完了するたびにカウントをデクリメントすることで、待機またはスリープ状態の Irp の内部カウントを保持する必要があります。 待機/ウェイク IRP を完了した後にカウントが0以外の場合、ドライバーはデバイススタックに別の待機/ウェイク IRP を送信して、ウェイクアップ用に "rearm" 自体を送信する必要があります。 詳細については、「[デバイスツリーを使用した待機/ウェイク irp のパスについ](https://docs.microsoft.com/windows-hardware/drivers/kernel/understanding-the-path-of-wait-wake-irps-through-a-device-tree)て」を参照してください。

**\_IRP の最大\_待機\_ウェイク**を取り消すには、ドライバーは[**iocancelirp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocancelirp)を呼び出します。 IRP を開始したドライバーだけがキャンセルできます。 次のいずれかが発生すると、ドライバーは保留中の**IRP\_による\_待機\_状態の解除**をキャンセルします。

-   ドライバーは、デバイスを停止または削除する PnP IRP を受信します。

-   システムはスリープ状態になり、デバイスのウェイクアップ信号はスリープ解除できません。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)

 

 




