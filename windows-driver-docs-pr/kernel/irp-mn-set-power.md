---
title: IRP_MN_SET_POWER
description: この IRP は、システム電源状態の変更をドライバーに通知するか、デバイスの電源状態を設定します。
ms.date: 08/12/2017
ms.assetid: 1294183a-bd0b-4ead-bd64-669d5b3725ce
keywords:
- IRP_MN_SET_POWER カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 41625176056f0cc384c6f8f065340df89b2f1c3b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838564"
---
# <a name="irp_mn_set_power"></a>IRP\_\_設定\_電源


この IRP は、システム電源状態の変更をドライバーに通知するか、デバイスの電源状態を設定します。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_の電源**](irp-mj-power.md)送信時
---------

システム電源マネージャーまたはデバイスの電源ポリシーの所有者が、この IRP を送信できます。

電源マネージャーは、システムの電源状態の変更をドライバーに通知するために、この IRP を送信します。 ドライバーがアイドル状態の検出のためにデバイスを登録した場合、電源マネージャーはこの IRP を送信して、アイドル状態のデバイスの電源状態を変更します。

電源ポリシーを所有するドライバーは、この IRP を送信して、デバイスのデバイスの電源状態を設定します。 ドライバーは、この IRP を送信するために[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)を呼び出す必要があります。

パワーマネージャーは、この IRP を IRQL = パッシブ\_レベルで、PDO の DO\_パワー\_PAGABLE フラグを設定するデバイススタックに送信します。 このようなスタック内のドライバーは、ページングされたコードまたはデータをタッチして要求を完了することができます。

DO\_電源\_突入電流フラグが設定されている場合、電源マネージャーは、IRQL = ディスパッチ\_レベルで IRP を送信できます。 このようなドライバーは、ページングされたコードやデータに直接または間接的にアクセスすることはできません。

## <a name="input-parameters"></a>入力パラメーター


SystemPowerState メンバーは、設定される電源の状態の種類 (または**DevicePowerState**) を指定します **。**

次のように、 **Parameters. power. State**メンバーは電源状態を指定します。

-   **SystemPowerState**が**の場合、** この値は[ **\_システムの\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_system_power_state)の種類の列挙子になります。

-   **DevicePowerState**がの場合、この値は[ **\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_device_power_state)の列挙子\_状態の**種類です。**

**Parameters. ShutdownType**メンバーは、要求された遷移に関する追加情報を指定します。 このメンバーに指定できる値は、 **POWER\_アクション**の列挙値です。 詳細については、「[システム電源動作](https://docs.microsoft.com/windows-hardware/drivers/kernel/system-power-actions)」を参照してください。

Windows Vista 以降では、 **Parameters. SystemPowerStateContext**メンバーは読み取り専用で、部分的に不透明な[**システム\_Power\_STATE\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_system_power_state_context)構造で、以前のシステムに関する情報が含まれています。コンピューターの電源状態。 **SystemPowerState**がパラメーターで**ある場合は**、パラメーターが有効であることを示し**ます。電力状態**は**powersystemworking**で、この構造体の2つのフラグビットは、高速スタートアップまたは休止状態からの復帰によってコンピューターの入力が発生したかどうかを示します。S0 (動作している) システム状態。 詳細については、「[ウェイクアップからの高速スタートアップの違い](https://docs.microsoft.com/windows-hardware/drivers/kernel/distinguishing-fast-startup-from-wake-from-hibernation)」を参照してください。

次の表は、IRP_MN_SET_POWER の内容を示して**います。Parameters。{State |ShutdownType}** と**currentsystemstate**、 **Targetsystemstate**、および**EffectiveSystemState**ビットの各フィールドを、システムの電源遷移ごとに[**SYSTEM_POWER_STATE_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_system_power_state_context)構造体にします。  各行は1つの**IRP_MN_SET_POWER**を表します。

|Transition|状態|シャットダウンの種類|現在のシステム状態|ターゲットシステムの状態|有効な SystemState|コメント|
|--- |--- |--- |--- |--- |--- |--- |
|スリープ状態...|S3|スリープ|S0|S3|S3||
|...ウェイクアップ|S0|スリープ|S3|S0|S0||
|ハイブリッドスリープ状態...|S4|休止状態|S0|S3|S4|休止状態ファイルを使用したスリープ (高速 S4)|
|...ウェイクアップ|S0|スリープ|S3|S0|S0||
|...ウェイク/PwrLost|S0|スリープ|S4|S0|S0||
|休止状態...|S4|休止状態|S0|S4|S4|||
|...ウェイクアップ|S0|スリープ|S4|S0|S0||
|ハイブリッドシャットダウン先...|S4|休止状態|S0|S5|S4|終了したアプリ、ユーザーがシャットダウン (Hiber ブート) としてログオフした|
|...高速スタートアップ|S0|スリープ|S4|S0|S0||
|シャットダウン先...|S5|シャットダウン/リセット/オフ|S0|S5|S5||
|...システムブート||||||起動するための S-IRP がありません|

## <a name="output-parameters"></a>出力パラメーター


**パラメーター。 SystemContext**はシステムで使用するために予約されています。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーは、 **Irp&gt;iostatus. status**を STATUS\_SUCCESS に設定して、デバイスが要求された状態になったことを示します。

ドライバーは、システムの電源状態を設定する要求を失敗させることはできません。

バスドライバーの上にある関数ドライバーとフィルタードライバーは、デバイスの電源状態を設定する要求を失敗させることはできません。 デバイスが取り外された場合、または削除中の場合、バスドライバーはデバイスの電源要求を失敗させる可能性があります。

<a name="operation"></a>操作
---------

電源マネージャーまたはドライバーは、 **irp\_\_設定**された電源 irp\_要求できます。 電源マネージャーは、次のいずれかの理由でこの IRP を送信します。

-   システム電源状態の変更をドライバーに通知するには

-   電源マネージャーがアイドル検出を実行しているデバイスの電源状態を変更するには

-   ドライバーが IRP\_に失敗した後に現在のシステム状態を reaffirm するには **\_クエリ\_** システム電源状態の電源要求を実行します。  詳細については、「 [**IRP_MN_QUERY_POWER**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-power#operation)」を参照してください。

デバイスの電源ポリシーを所有しているドライバーが IRP\_を送信し、デバイスの電源状態を変更する **\_電源\_設定**します。

どの時点でも、各デバイスオブジェクトに対して1つの IRP がアクティブになることが許可されます。

各ドライバーは、 [**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) (windows Vista 以降) または[**pocalldriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) (Windows SERVER 2003、Windows XP、および windows 2000) を呼び出すことによって、各電源 IRP を次の下位のドライバーに渡す必要があります。 **Pocalldriver**インターフェイスは**IoCallDriver**と似ていますが、電源管理サブシステムが IRP を遅延させてから次のドライバーに渡すことができます。 たとえば、デバイスが突入電流を現在必要としていて、そのようなデバイスと直列に電源を入れる必要がある場合、 **PowerDeviceD0**要求で遅延が発生する可能性があります。

ドライバーが\_Windows Server 2003、Windows XP、または Windows 2000 で**電源要求\_設定**された IRP\_を受け取った後、ドライバーは postartnextpowerirp を呼び出す必要があります。詳細については、「 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp) [Postartnextpowerirp の呼び出し](https://docs.microsoft.com/windows-hardware/drivers/kernel/calling-postartnextpowerirp)」を参照してください。 Windows Vista 以降では、 **Postartnextpowerirp**を呼び出す必要はなく、このような呼び出しは電源管理操作を実行しません。

**システム電源の状態の\_電力\_設定された IRP\_**

システムパワーマネージャーのみがシステムセット-電源 IRP を送信できます。

ドライバーは、システムの電源状態を設定する要求を失敗させることはできません。

可能な場合は常に、電源マネージャーが irp を送信\_する前に[ **\_クエリ\_電力を\_** ](irp-mn-query-power.md)送信します。これにより、システムのスリープ状態を要求するための **\_電力\_設定**されます。 ただし、状況によっては (ユーザーが **[電源オフ]** ボタンを押すか、バッテリの有効期限が切れているなど)、最初にクエリを実行せずに、電源管理者が**IRP\_\_設定して電源を入れ\_** ことがあります。 電源マネージャーは、スリープ状態の場合にのみクエリを行います。電源を入れる前にクエリを実行することはありません。

**電源要求\_IRP\_\_セット**は、デバイスのデバイススタックの最上位のドライバーに送信されます。 上位のドライバーは、irp が次の下位のドライバーに渡されるまで、irp がバスドライバーに到達するまで、irp を完了する必要があります。

フィルタードライバーは、通常、システムセットを渡すのではなく、システムの set-power IRP で動作する必要はありません。

ただし、デバイスの電源ポリシー所有者は、IRP を渡す前に[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定します。 *Iocompletion*ルーチンでは、デバイスの電源 IRP の**電源要求\_\_設定**された IRP\_を送信します。 詳細については、「[デバイスの電源ポリシー所有者におけるシステムセット-電源 IRP の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-a-system-set-power-irp-in-a-device-power-policy-owner)」を参照してください。

システム設定-電源 IRP は、システムの電源状態が近づいていること、およびドライバーが準備する必要があることをドライバーに通知します。 ただし、ドライバーでは、デバイス*の電源状態*の **\_電源\_設定**された IRP\_を受信するまで、デバイスの電源状態を変更しないでください。

**パラメーター**の値は、保留中のアクションに関する追加情報を提供します。 IRP が**Powersystemshutdown** (S5) を指定すると、ドライバーはシステムがリセットされている (**Poweractionshutdownreset**) か、後で再起動するために無期限に電源をオフにするか (**PowerActionShutdownOff**) を判断できます。 ほとんどのデバイスのドライバーの場合、違いは重要ではありません。 ただし、ビデオストリーミングデバイスなどの特定のデバイスでは、システムがリセットされたときに i/o を停止するために、ドライバーがデバイスの電源をオフにすることがあります。

Windows 2000 以降のバージョンのオペレーティングシステムでは、 **Shutdowntype**の値も**poweractionshutdown**にすることができます。 この場合、ドライバーはどの種類のシャットダウンが要求されているかを識別できないため、リセットのために続行する必要があります。

**デバイスの電源状態**

バスドライバーの上にある関数ドライバーとフィルタードライバーは、デバイスの電源状態を設定する要求を失敗させることはできません。 デバイスが取り外された場合、または削除中の場合、バスドライバーはデバイスの電源要求を失敗させる可能性があります。

ドライバーは、IRP を完了する前に、デバイスを要求された状態に設定する必要があります。

IRP が低電力状態への遷移を要求すると、ドライバーはデバイススタックを経由したときに IRP を処理する必要があります。これにより、ドライバーがデバイスを動作状態に復元するために必要なすべてのコンテキストが保存されます。 バスドライバーが IRP を受信した後、ドライバーは次のようになります。

-   デバイスを動作状態に復元するためにドライバーが必要とするすべてのコンテキストを保存します。

-   デバイスを要求された電源の状態に設定します。

-   [**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)を呼び出して、電源マネージャーに通知します。

-   **Postartnextpowerirp**を呼び出して、次の電源 IRP を開始します (windows Server 2003、windows XP、および windows 2000 のみ)。

-   デバイスの電源 IRP を完了します。

ドライバーは、この IRP を適切なタイミングで完了する必要があります。 一般に、ドライバーは、一般的なユーザーが著しく低速であるという遅延を回避する必要があります。 たとえば、ドライバーは、キャッシュされたディスクまたはネットワークデータをフラッシュするためにシステムの状態の変更を遅延させることがありますが、ネットワーク接続を維持したり、テープをフォーマットしたりすることはできません。 詳細については、「[電源 irp の受け渡し](https://docs.microsoft.com/windows-hardware/drivers/kernel/passing-power-irps)」を参照してください。

Windows 2000 以降のバージョンのオペレーティングシステムでは、IRP で**PowerDeviceD1**、 **PowerDeviceD2**、または**PowerDeviceD3**が指定されていて、システムセット-power irp がアクティブである場合、パラメーターの値はになります **。** システムの IRP に関する情報。

休止状態のデバイスのドライバーは、この値を検査する必要があります。 IRP requests **PowerDeviceD3**と**Shutdowntype**が**poweractionhibernate**の場合、このようなドライバーでは、デバイスを復元するために必要なすべてのコンテキストを保存する必要がありますが、デバイスの電源を切ることはできません。コンピューターの電源が切断されると、デバイスは D3 状態になります。

Windows 2000 以降のバージョンのオペレーティングシステムでは、要求された電源の状態が**PowerDeviceD0**の場合、ドライバーは**shutdowntype**の値に依存しないようにする必要があります。

Windows 98/Me で、IRP がデバイスの電源状態を要求した場合、 **Shutdowntype**は常に**poweractionnone**になります。

デバイスの電源を切るタイミングは、デバイスクラスによって異なります。

デバイスの電源をオンにするタイミングを決定するドライバーは、ほとんどの場合、デバイスレジスタにアクセスするドライバーです。 ドライバーは、デバイスのハードウェアレジスタにアクセスする前に、デバイスが D0 状態であることを確認する必要があります。 デバイスが D0 状態でない場合、ドライバーは**PoRequestPowerIrp**を呼び出して、デバイスの電源を入れて IRP を送信する必要があります。 デバイスが D0 状態の場合を除き、ドライバーはデバイスにアクセスできません。

ドライバーは、デバイスの状態 D0 に対して set-power IRP を受け取ると、 *Iocompletion*ルーチンを設定し、IRP を次の下位のドライバーに渡します。

IRP がバスドライバーに到達すると、そのドライバーはデバイスに電力を適用 (またはリセット) し、 **Postartnextpowerirp** (windows Server 2003、windows XP、および windows 2000 のみ) を呼び出し、 **PoSetPowerState**を呼び出して新しい電源のパワーマネージャーに通知します。デバイスの状態。

バスドライバーが電源投入時の IRP を完了すると、関数とフィルタードライバーは、デバイススタックをバックアップするときに、 *Iocompletion*ルーチン内の irp を処理します。 *Iocompletion*ルーチンでは、各ドライバーがデバイスコンテキストを復元または再初期化し、その他の必要なスタートアップタスクを実行します。

詳細については、「[デバイスの電源状態の\_電力を設定する\_IRP\_を処理する](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irp-mn-set-power-for-device-power-states)」を参照してください。

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
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**デバイス\_電源\_状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_device_power_state)

[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)

[**IRP\_\_クエリ\_電力**](irp-mn-query-power.md)

[**IRP\_\_設定\_電源**](irp-mn-set-power.md)

[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver)

[**PoStartNextPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-postartnextpowerirp)

[**PoSetPowerState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-posetpowerstate)

[**PoRequestPowerIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp)

[**システム\_電源\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_system_power_state)

[**システム\_電源\_状態\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_system_power_state_context)

 

 




