---
title: IRP_MN_QUERY_CAPABILITIES
description: PnP マネージャーでは、デバイスをロックまたは取り出すかどうかなど、デバイスの機能を取得するには、この IRP を送信します。関数とフィルター ドライバーは、バス ドライバーでサポートされる機能を変更する場合、この要求を処理できます。
ms.date: 08/12/2017
ms.assetid: 3c968a46-5bfb-4579-b09a-ad6bce4d9e3b
keywords:
- IRP_MN_QUERY_CAPABILITIES Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: cb2091e2b1ddbd4197e7c3a72c070e9e45ea06e2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383291"
---
# <a name="irpmnquerycapabilities"></a>IRP\_MN\_クエリ\_機能


PnP マネージャーでは、デバイスをロックまたは取り出すかどうかなど、デバイスの機能を取得するには、この IRP を送信します。

関数とフィルター ドライバーは、バス ドライバーでサポートされる機能を変更する場合、この要求を処理できます。 バス ドライバーには、その子デバイスは、この要求を処理する必要があります。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP** ](irp-mj-pnp.md)送信されるときに
---------

PnP マネージャーでは、デバイスが列挙された後すぐに、この IRP をデバイスのバス ドライバーに送信します。 デバイスが起動した後デバイスのすべてのドライバー、PnP マネージャーをもう一度この IRP は送信します。 ドライバーは、デバイスの機能を取得するには、この IRP を送信できます。

PnP マネージャーとドライバーは、この IRP を送信 IRQL パッシブで\_任意のスレッド コンテキストでします。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.DeviceCapabilities.Capabilities**のメンバー、 [ **IO\_スタック\_場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_stack_location) を指す構造体[**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)デバイスの機能に関する情報を含む構造体。

## <a name="output-parameters"></a>出力パラメーター


**Parameters.DeviceCapabilities.Capabilities**を指す、**デバイス\_機能**IRP の処理のドライバーによって行われた変更を反映する構造体。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功や状態などの適切なエラー状態に\_失敗しました。

呼び出す関数またはフィルター ドライバーがこの IRP を処理しない場合[ **IoSkipCurrentIrpStackLocation** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)し、[次へ] のドライバーに IRP を渡します。 このようなドライバーを変更する必要がありますいない**Irp -&gt;IoStatus.Status** IRP を完了する必要があります。

バス ドライバー設定**Irp -&gt;IoStatus.Status** IRP が完了するとします。

<a name="operation"></a>操作
---------

デバイスが列挙されて、PnP マネージャーが送信するデバイスには、関数とフィルター ドライバーが読み込まれる、前に、 **IRP\_MN\_クエリ\_機能**の親のバス ドライバーへの要求デバイスです。 バス ドライバーで、関連する値を設定する必要があります、 [**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)構造体し、マネージャー、PnP を返します。

デバイス スタックを構築すると、デバイス ドライバーを開始、PnP マネージャーは、デバイス スタックの上部にある、ドライバー、続いて各下位のドライバー スタックで最初に処理するためにもう一度この IRP を送信します。 関数とフィルター ドライバーを設定できる、 [ *IoCompletion* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-io_completion_routine)ルーチンとハンドルが途中では、この IRP がデバイス スタックをバックアップします。

ドライバーは IRP を次の下位のドライバーに渡される前に、機能を追加する必要があります。

ドライバーでは、下位のすべてのドライバーが IRP が完了したら機能を削除する必要があります。 ドライバーは通常、その他のドライバーによって設定されている機能を削除していませんが、特定の構成では、デバイスの機能に関する特別な情報がある場合はその可能性があります。 参照してください[プラグ アンド プレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)IRP が下位のドライバーが完了するまでに処理を延期することについてです。

デバイスが列挙され、そのドライバーが読み込まれて、その機能は変更しないでください。 デバイスの機能を変更する場合は、デバイスが削除され再列挙可能性があります。

処理するときに、 **IRP\_MN\_クエリ\_機能**IRP、デバイスの電源ポリシー マネージャーであるドライバーを設定する必要があります、 *IoCompletion*ルーチンとS-D 電源の状態マッピングのバックアップ デバイス スタックを IRP の方法など、デバイスの電源機能をコピーします。 子デバイスの電源機能を確認するのには、親のバス ドライバーは、別のクエリ機能 IRP を作成し、その親ドライバーに IRP を送信します。 参照してください[デバイスの電源機能の報告](https://docs.microsoft.com/windows-hardware/drivers/kernel/reporting-device-power-capabilities)詳細についてはします。

ドライバーは、この IRP を処理する場合は確認する必要があります、**デバイス\_機能** **バージョン**値。 その値が、ドライバーをサポートするバージョンでない場合、ドライバーは IRP を失敗する必要があります。 ドライバーを確認する必要があります、バージョンがサポートされている場合、**サイズ**フィールド。 ドライバーは、入力として受信した機能の構造体の境界内にあるフィールドのみを設定する必要があります。

この IRP を処理するドライバーは、いくつかを設定できます**デバイス\_機能**フィールドしますが、設定されていない必要があります、**サイズ**と**バージョン**フィールド。 これらのフィールドは IRP を送信するコンポーネントによってのみ設定されます。

参照してください[プラグ アンド プレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)処理のための一般的な規則[プラグ アンド プレイ マイナー Irp](plug-and-play-minor-irps.md)します。

**この IRP を送信します。**

バス ドライバーが処理する場合に、親デバイス スタックにこの IRP を送信する**IRP\_MN\_クエリ\_機能**その子デバイスの 1 つの要求。 また、ドライバーは、そのデバイスの 1 つのデバイス機能を取得するには、この IRP を送信することができます。 スタック内の 1 つのドライバーがデバイスの機能情報の一部のみデバイス スタックに IRP を送信することによって、フィルター ドライバー、およびその他の変更を含む、完全な画像を収集するために有効にします。

参照してください[Irp の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)Irp を送信する方法について。 この IRP に具体的には、次の手順が適用されます。

-   割り当て、 [**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)からページ プールは、構造体し、呼び出すことによってゼロに初期化[ **RtlZeroMemory** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlzeromemory). 初期化、**サイズ**に**sizeof**(**デバイス\_機能**)、**バージョン**1、および**アドレス**と**UINumber**を-1 にします。

-   IRP の I/O スタック内の次の場所の値を設定します設定**MajorFunction**に[ **IRP\_MJ\_PNP**](irp-mj-pnp.md)設定 **。MinorFunction**に**IRP\_MN\_クエリ\_機能**、設定と**Parameters.DeviceCapabilities**へのポインターには割り当てられた**デバイス\_機能**構造体。

-   初期化**IoStatus.Status**ステータス\_いない\_サポートされています。

-   IRP の割り当てを解除し、**デバイス\_機能**不要になったときに構造体します。

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


[**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)

 

 




