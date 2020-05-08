---
title: IRP_MN_QUERY_POWER
description: この IRP は、デバイスを照会して、システムの電源状態またはデバイスの電源状態を変更できるかどうかを判断します。
ms.date: 08/12/2017
ms.assetid: fc4c5364-2160-4525-889a-96785a3c7a07
keywords:
- IRP_MN_QUERY_POWER カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: fac293187ca2abfaa7ab07fb2e8054c77d8601bf
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922529"
---
# <a name="irp_mn_query_power"></a>IRP\_の\_クエリ\_力


この IRP は、デバイスを照会して、システムの電源状態またはデバイスの電源状態を変更できるかどうかを判断します。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_の電源**](irp-mj-power.md)

<a name="when-sent"></a>送信時
---------

電源マネージャーまたはデバイスの電源ポリシー所有者は、この IRP を送信して、システムまたはデバイスの電源状態を変更できるかどうかを判断します。通常はスリープ状態に移行します。 ドライバーは、この IRP を割り当てて送信するために[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)を呼び出す必要があります。

パワーマネージャーは、この IRP を IRQL = パッシブ\_レベルで、PDO で DO\_パワー\_pagable フラグを設定したデバイススタックに送信します。

DO\_power\_突入電流フラグが設定されている場合\_、電源マネージャーは、IRQL = ディスパッチレベルで IRP を送信できます。 このようなドライバーは、ページングされたコードやデータに直接または間接的にアクセスすることはできません。

## <a name="input-parameters"></a>入力パラメーター


**SystemPowerState**または**DevicePowerState**のいずれかで、設定する電源の状態の種類を指定し**ます。**

**Parameters**は、次のように電源状態を指定します。

-   SystemPowerState**が指定されて**いる**SystemPowerState**場合、値は[**\_システムの電源\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_system_power_state)の種類の列挙子になります。

-   DevicePowerState**が指定されて**いる**DevicePowerState**場合、値は[**\_デバイスの電源\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_device_power_state)の種類の列挙子になります。

**パラメーター。 ShutdownType**は、要求された遷移に関する追加情報を指定します。 指定できる値は、 **POWER\_ACTION**型の列挙子です。

## <a name="output-parameters"></a>出力パラメーター


ありません。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーでは、 **Irp&gt;-Iostatus. status**が\_SUCCESS に設定され、デバイスが要求された状態になる可能性があることを示しています。 ドライバーは、要求された状態を入力できないことを示すために、適切なエラー状態を設定します。

<a name="operation"></a>Operation
---------

**\_Irp\_\_** を使用したクエリのパワーのパラメーターは、irp [**\_の\_完全\_なセットパワー**](irp-mn-set-power.md)のパラメーターと同じです。 ただし、後の電源状態の変更をドライバーに通知するのではなく、 **IRP\_\_\_** を使用したクエリパワーは、システムまたはデバイスが特定の電源状態に入ることができるかどうかをクエリします。

ドライバーでは、 **IRP\_\_\_** によるクエリのパワー要求に応じて、デバイスの電源状態を変更することはできません。

ドライバーが Windows Server 2003、Windows XP、および Windows 2000 で**IRP\_\_完了クエリ\_の電源**要求を受信した後、ドライバー[**は postartnextpowerirp を呼び**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)出す必要があります。詳細については、「 [ **postartnextpowerirp**の呼び出し](https://docs.microsoft.com/windows-hardware/drivers/kernel/calling-postartnextpowerirp)」を参照してください。 Windows Vista 以降では、 **Postartnextpowerirp**を呼び出す必要はなく、このような呼び出しは電源管理操作を実行しません。

**システム\_の\_電源\_状態に対する IRP のクエリ力**

この IRP は、ネットワーク接続の切断などの処理を中断することなく、システムの電源状態を変更できることを確認するために、電源マネージャーによって送信されます。

可能な限り、電源マネージャーは、システムのスリープ状態または通常のシステムのシャットダウンを要求するために、 **IRP\_の全\_セット\_パワー**を送信する前にクエリを実行します。 ただし、一部の重大な状況 (ユーザーが**電源オフ**ボタンを押したときや、バッテリの有効期限が切れている場合など) では、最初にクエリの電源要求を送信せずに、 **IRP\_\_\_** の全セットの電源要求を送信することがあります。 電源マネージャーは、スリープ状態の場合にのみクエリを行います。動作状態に戻る前にクエリを実行することはありません。

ドライバーがシステムの power query IRP を受信した場合、この irp は、照会されたシステム状態に対して有効なデバイスの状態をサポートできない場合、IRP を失敗させる必要があります。 詳細については、「 [**Devicestate**](https://docs.microsoft.com/windows-hardware/drivers/kernel/devicestate)」を参照してください。 それ以外の場合、ドライバーは IRP を次の下位のドライバーに渡す必要があります。 バスドライバーが IRP を完了します。

Windows Vista 以降では、システムスリープ状態への移行は重大な操作と見なされます。 ドライバーがシステムクエリを失敗させる可能性がありますが、停電の場合でも、電源マネージャーはシステムの電源状態をスリープ状態に変更することがあります。 ドライバーがシステムクエリを受信した後、システムの電源状態を変更するには、ドライバーを常に準備する必要があります。

デバイスの電源ポリシー所有者がシステムの power query IRP を受け取ると、IRP で[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンが渡される前に、その irp を設定する必要があります。 *Iocompletion*ルーチンでは、照会されたシステム状態に対して有効なデバイスの状態に対して、 **IRP\_\_\_** を使用したクエリパワーを送信する必要があります。 詳細については、「[システムクエリ-電源 IRP をデバイスの電源ポリシー所有者に処理する](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-a-system-query-power-irp-in-a-device-power-policy-owner)」を参照してください。

IRP で**Powersystemshutdown** (S5) が指定されている場合、shutdown**型**の値は、シャットダウンの理由を提供します。 **Shutdowntype**は、システムがリセットされているかどうか (**Poweractionshutdownreset**)、または後で再起動するために無期限に電源をオフにする (**PowerActionShutdownOff**) かどうかをドライバーに指示します。 ほとんどのデバイスのドライバーの場合、違いは重要ではありません。 ただし、DMA を実行するビデオストリーミングデバイスなど、特定のデバイスの場合、ドライバーはシステムをリセットするときにデバイスの電源を切ることを選択して、実行中の i/o を停止することがあります。

Microsoft Windows 2000 以降のシステムでは、 **Shutdowntype**の値も**poweractionshutdown**にすることができます。 この場合、ドライバーはどの種類のシャットダウンが要求されているかを識別できないため、リセットのために続行する必要があります。

システムの電源状態に**対する\_irp\_を\_** 使用したクエリの電源要求がドライバーによって失敗した場合、通常、電源マネージャーは、irp **\_\_\_** の全セットの電源 irp を発行することによって応答します。 通常、この IRP は、現在のシステム状態を reaffirm します。 ただし、ドライバーが、照会された状態またはその他の中間状態に対して**IRP\_\_\_** を使用した能力を持つ可能性があります。 ドライバーは、このような状況に対処できるように準備する必要があります。

**デバイス\_の\_電源\_状態に対する IRP のクエリ力**

デバイスの電源ポリシー所有者は、システムの**irp\_\_\_** を通したクエリのパワー要求に応じて、この IRP をスタックに送信します。

ドライバーがデバイスを要求されたデバイス状態にすると、 **iostatus. status**が\_SUCCESS に設定され、次の下位のドライバーに irp が渡されます。これは、irp がバスドライバーに到達するまで続きます。 スタック内のいずれかのドライバーが IRP を失敗させる必要がある場合、そのドライバーは**IoCompleteRequest**を呼び出してエラー状態を返すことで、直ちに irp を完了する必要があります。 IRP が失敗したドライバーは、スタックの下位に到達しません。

正常な状態\_を返すことにより、ドライバーは、要求された電源状態を設定する機能を変更する操作を開始しないことを保証します。 ドライバーは、デバイスを許容できる電力状態に返す set-電源 IRP を完了するまで、このような操作を必要とする任意の Irp をキューに入れます。

Windows 2000 以降のシステムでは、IRP で PowerDeviceD1、 **PowerDeviceD2**、または**PowerDeviceD3**が指定されている場合、システム電源 irp がアクティブになっていると、現在のシステム電源の状態に関する情報が、 **PowerDeviceD1**の値によって提供されます **。** この場合、 **Shutdowntype**の値は、現在要求されているシステム電源の状態を示します。システム要求が未処理でない場合は**poweractionnone**を示します。 Windows 98/Me では、IRP がデバイスの電源状態を要求した場合、このフィールドには常に**Poweractionnone**が含まれます。

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


[**IRP\_の\_クエリ\_力**](irp-mn-query-power.md)

[**IRP\_の\_全\_セットの電源**](irp-mn-set-power.md)

[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)

[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)

 

 




