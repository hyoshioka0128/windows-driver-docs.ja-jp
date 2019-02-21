---
title: IRP_MN_QUERY_POWER
description: この IRP では、システム電源の状態またはデバイスの電源状態を変更できるかどうかを判断するデバイスを照会します。
ms.date: 08/12/2017
ms.assetid: fc4c5364-2160-4525-889a-96785a3c7a07
keywords:
- IRP_MN_QUERY_POWER カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 2f9df260fdf923b619a5c3298724044b0b8ed6dc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556909"
---
# <a name="irpmnquerypower"></a>IRP\_MN\_クエリ\_電源


この IRP では、システム電源の状態またはデバイスの電源状態を変更できるかどうかを判断するデバイスを照会します。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_POWER** ](irp-mj-power.md)送信されるときに
---------

電源マネージャーまたはデバイスの電源ポリシー所有者は、変更が決定するかどうかにできますシステムまたはデバイスの電源状態で、通常にスリープ状態にするには、この IRP を送信します。 ドライバーを呼び出す必要があります[ **PoRequestPowerIrp** ](https://msdn.microsoft.com/library/windows/hardware/ff559734)を割り当てて、この IRP を送信します。

電源マネージャー IRQL でこの IRP の送信 = パッシブ\_レベル設定デバイス スタックを\_POWER\_pdo PAGABLE フラグを設定します。

電源マネージャーは IRQL で IRP を送信することができます = ディスパッチ\_レベルの場合、操作を行います\_POWER\_突入フラグを設定します。 このようなドライバー直接的または間接的にアクセスできません、ページのコードやデータ。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.Power.Type**か、設定されている電源状態の種類を指定します**SystemPowerState**または**DevicePowerState**します。

**Parameters.Power.State**自体には、電源の状態を次のように指定します。

-   場合**Parameters.Power.Type**は**SystemPowerState**、値の列挙子は、 [**システム\_POWER\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff564565)型。

-   場合**Parameters.Power.Type**は**DevicePowerState**、値の列挙子は、 [**デバイス\_POWER\_状態**](https://msdn.microsoft.com/library/windows/hardware/ff543160)型。

**Parameters.Power.ShutdownType**要求された移行に関する追加情報を指定します。 指定できる値はの列挙子、 **POWER\_アクション**型。

## <a name="output-parameters"></a>出力パラメーター


なし。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_をデバイスが要求された状態を入力できることを示すために成功します。 ドライバーは、要求された状態を入力できないことを示すすべての適切なエラー状態を設定します。

<a name="operation"></a>操作
---------

パラメーターを**IRP\_MN\_クエリ\_POWER**がの場合と同じ[ **IRP\_MN\_設定\_電源**](irp-mn-set-power.md). ただし、電源状態を後の変更のドライバーを通知するのではなく**IRP\_MN\_クエリ\_POWER**システムまたはデバイスが特定の電源状態を入力することができるかどうかを照会します。

ドライバーはへの応答には、そのデバイスの電源状態を変更する必要があります、 **IRP\_MN\_クエリ\_POWER**要求。

ドライバーを受信した後、 **IRP\_MN\_クエリ\_POWER**ドライバーを呼び出す必要があります要求を Windows server 2003、Windows XP、および Windows 2000、 [ **PoStartNextPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559776)」の説明に従って、[呼び出す**PoStartNextPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff540724)します。 Windows Vista 以降、通話**PoStartNextPowerIrp**は必要ありませんし、このような呼び出しには電源管理操作は実行されません。

**IRP\_MN\_クエリ\_システム電源の状態の電源**

電源マネージャーは、ネットワーク接続を削除するなどの作業を中断せずシステム電源の状態を変更できるように、この IRP を送信します。

電源マネージャーが送信する前にクエリ可能であれば、 **IRP\_MN\_設定\_POWER**システムのスリープ状態または通常のシステムのシャット ダウンを要求します。 ただし、いくつかの重要な条件下 (ユーザー キーを押してなど、**電源オフ**ボタンや、バッテリの期限切れ)、電源マネージャーが送信することがあります、 **IRP\_MN\_設定\_POWER**電源要求のクエリを最初に送信せずに要求します。 スリープ状態にのみ電源マネージャーのクエリ動作状態に戻る前に決してを照会します。

ドライバーは、システム電源クエリ IRP を受信したときに、クエリ対象のシステム状態の有効なデバイスの状態のいずれかをサポートできない場合に IRP が失敗する必要があります。 詳細については、次を参照してください。 [ **DeviceState**](https://msdn.microsoft.com/library/windows/hardware/ff543087)します。 それ以外の場合、ドライバーは、[次へ] の下のドライバーに IRP を渡す必要があります。 バス ドライバーは IRP を完了します。

システムのスリープ状態に遷移の Windows Vista 以降、重要な操作と見なされます。 ドライバーが失敗する、システムが引き続きクエリ性能の IRP 電源マネージャーでは、次のスリープ状態にシステムの電源状態を変更可能性があります。 ドライバーは IRP のクエリ機能、ドライバーは常にシステムを受信した後は、システムの電源状態の後続の変更を準備します。

設定する必要がありますが、デバイスの電源ポリシー所有者は、システム電源クエリ IRP を受信したときに、 [ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)渡す前に IRP のルーチンです。 *IoCompletion*ルーチンを送る、 **IRP\_MN\_クエリ\_POWER**のクエリ対象のシステム状態の有効なデバイスの状態。 詳細については、次を参照してください。[電源ポリシー所有者のデバイスでのシステム クエリ Power IRP の処理](https://msdn.microsoft.com/library/windows/hardware/ff546725)します。

IRP を指定した場合**PowerSystemShutdown** (S5) にある値**Parameters.Power.ShutdownType**シャット ダウンの理由を示します。 **ShutdownType**ドライバーに指示するかどうか、システムがリセットされています (**PowerActionShutdownReset**) または後で再起動するには、無期限に電源をオフ (**PowerActionShutdownOff**). ほとんどのデバイス ドライバー、違いは重要ではありません。 ただし、DMA を実行するデバイスをストリーミング ビデオなど、特定のデバイス ドライバーを選択する場合、デバイスの電源をシステムをリセットすると、そのため、継続的な I/O を停止するときにします。

Microsoft Windows 2000 以降のシステム、ある値で**ShutdownType**することもできます**PowerActionShutdown**します。 この場合、ドライバーでは、シャット ダウンの種類が要求され、このためとリセットを実行する必要がありますを見分けることはできません。

ドライバーが失敗した場合、 **IRP\_MN\_クエリ\_POWER**を発行して電源マネージャーが通常は応答のシステム電源の状態を要求する**IRP\_MN\_設定\_POWER** IRP します。 通常、この IRP ことを再確認する現在のシステム状態。 ただし、ドライバーを受信する可能性があることは、 **IRP\_MN\_設定\_POWER**照会された状態またはその他の中間状態にします。 ドライバーは、このような状況を処理するために準備する必要があります。

**IRP\_MN\_クエリ\_デバイスの電源状態の電源**

デバイスの電源ポリシー所有者は、この IRP をシステムへの応答には、そのスタックに送信**IRP\_MN\_クエリ\_POWER**要求。

設定されている場合は、ドライバーは、要求されたデバイスの状態にそのデバイスを置くことが、 **IoStatus.Status**ステータス\_ドライバーを削減し、バス ドライバーが IRP に到達するまでになど成功を次に IRP を渡します。 スタック内の任意のドライバーは IRP を失敗する必要があります場合、ドライバーをする必要があります IRP 直ちに完了呼び出して**IoCompleteRequest**エラー状態を返すとします。 ドライバーは IRP を失敗を渡さないでくださいさらに下位のスタック。

状態を返すことによって\_成功すると、ドライバーの保証が、要求された電源の状態を設定するには、その機能を変更する操作は開始されません。 ドライバーを許容可能な電源状態のデバイスを返すセット power IRP が完了するまで、このような操作を必要とする任意の Irp キューに入れる必要があります。

Windows 2000 および IRP を指定すると、以降のシステムで**PowerDeviceD1**、 **PowerDeviceD2**、または**PowerDeviceD3**にある値**Parameters.Power.ShutdownType**システム電源 IRP がアクティブな場合は、現在のシステム電源 IRP、に関する情報を提供します。 この場合、ある値**ShutdownType**現在要求されているシステムの電源状態を示しますまたは**PowerActionNone**システム要求が存在しない場合。 Windows 98 でこのフィールドは常に格納する、/ **PowerActionNone** IRP がデバイスの電源状態を要求したときにします。

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


[**IRP\_MN\_クエリ\_電源**](irp-mn-query-power.md)

[**IRP\_MN\_SET\_POWER**](irp-mn-set-power.md)

[**PoRequestPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559734)

[**PoStartNextPowerIrp**](https://msdn.microsoft.com/library/windows/hardware/ff559776)

 

 




