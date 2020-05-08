---
title: IRP_MN_QUERY_CAPABILITIES
description: PnP マネージャーは、デバイスをロックまたは取り出すことができるかどうかなど、デバイスの機能を取得するために、この IRP を送信します。関数とフィルタードライバーは、バスドライバーでサポートされている機能を変更すると、この要求を処理できます。
ms.date: 08/12/2017
ms.assetid: 3c968a46-5bfb-4579-b09a-ad6bce4d9e3b
keywords:
- IRP_MN_QUERY_CAPABILITIES カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 8308d412092dbe2a8507371174489eeb77eb7c2f
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922533"
---
# <a name="irp_mn_query_capabilities"></a>IRP\_の\_全\_クエリ機能


PnP マネージャーは、デバイスをロックまたは取り出すことができるかどうかなど、デバイスの機能を取得するために、この IRP を送信します。

関数とフィルタードライバーは、バスドライバーでサポートされている機能を変更すると、この要求を処理できます。 バスドライバーは、子デバイスに対してこの要求を処理する必要があります。

## <a name="value"></a>値

0x09

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>送信時
---------

PnP マネージャーは、デバイスが列挙された直後にこの IRP をデバイスのバスドライバーに送信します。 デバイスのすべてのドライバーがデバイスを起動した後、PnP マネージャーはこの IRP を再び送信します。 ドライバーは、この IRP を送信して、デバイスの機能を取得できます。

PnP マネージャーとドライバーは、任意のスレッドコンテキストで\_この IRP を IRQL パッシブレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


[**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)の構造体の**DeviceCapabilities**メンバーは、デバイスの機能に関する情報を含む[**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の構造体を指します。

## <a name="output-parameters"></a>出力パラメーター


**DeviceCapabilities**は、IRP を処理するドライバーによって行われた変更を反映する**デバイス\_機能**構造を指します。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーは、 **Irp-&gt;iostatus**を、status が\_SUCCESS に設定されているか、状態\_が "失敗" などの適切なエラー状態に設定されています。

関数またはフィルタードライバーがこの IRP を処理しない場合は、 [**Ioskipfinalentifinallocation**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)を呼び出し、次のドライバーに irp を渡します。 このようなドライバーでは、 **irp&gt;** を変更することはできません。 irp を完了することはできません。

バスドライバーは、 **irp&gt;の状態**を設定し、irp を完了します。

<a name="operation"></a>Operation
---------

デバイスが列挙される前に、関数とフィルタードライバーがデバイス用に読み込まれる前に、PnP マネージャーは、デバイスの親バスドライバーに対して、 **IRP\_\_\_** を使用したクエリ機能要求を送信します。 バスドライバーは、[**デバイス\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の構造に関連する値を設定し、PnP マネージャーに返す必要があります。

デバイススタックが構築され、ドライバーによってデバイスが開始されると、PnP マネージャーはこの IRP を再送信して、デバイススタックの最上位にあるドライバーによって最初に処理され、その後、スタック内の下位の各ドライバーによって処理されるようになります。 関数ドライバーとフィルタードライバーは、 [*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンを設定し、デバイススタックをバックアップするようにこの IRP を処理できます。

ドライバーは、IRP を次の下位のドライバーに渡す前に、機能を追加する必要があります。

ドライバーは、すべての下位ドライバーが IRP で終了した後に機能を削除する必要があります。 ドライバーでは、通常、他のドライバーによって設定された機能は削除されませんが、特定の構成におけるデバイスの機能に関する特別な情報が含まれている場合は、そのような機能が必要になります。 低いドライバーが終了するまで IRP 処理を延期する方法の詳細については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

デバイスが列挙され、ドライバーが読み込まれた後、その機能を変更することはできません。 デバイスが削除され、再列挙されると、デバイスの機能が変更される可能性があります。

Irp が完了**し\_た\_クエリ\_機能**の irp を処理するときは、デバイスの電源ポリシーマネージャーであるドライバーが*Iocompletion*ルーチンを設定し、S-D 電源状態マッピングなどのデバイスの電源機能を irp によってデバイススタックをバックアップするようにコピーする必要があります。 親バスドライバーは、子デバイスの電源機能を確認するために、別のクエリ機能の IRP を作成し、その親ドライバーに IRP を送信します。 詳細については、「[レポートデバイスの電源機能](https://docs.microsoft.com/windows-hardware/drivers/kernel/reporting-device-power-capabilities)」を参照してください。

ドライバーがこの IRP を処理する場合は、 **\_デバイスの機能****バージョン**の値を確認する必要があります。 この値がドライバーでサポートされているバージョンではない場合、ドライバーは IRP を失敗させる必要があります。 バージョンがサポートされている場合、ドライバーは [**サイズ**] フィールドを確認する必要があります。 ドライバーは、入力として受け取った機能構造の境界内にあるフィールドのみを設定する必要があります。

この IRP を処理するドライバーは、一部の**デバイス\_機能**フィールドを設定できますが、[**サイズ**] フィールドと [**バージョン**] フィールドを設定することはできません。 これらのフィールドは、IRP を送信したコンポーネントによってのみ設定されます。

[プラグアンドプレイの小さな irp](plug-and-play-minor-irps.md)を処理するための一般的な規則については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。

**この IRP を送信しています**

バスドライバーは、その子デバイスの1つに対する**\_irp\_の\_クエリ機能**要求を処理するときに、この irp を親デバイススタックに送信します。 また、ドライバーは、そのデバイスの1つのデバイス機能を取得するために、この IRP を送信する場合があります。 スタック内の1つのドライバーには、デバイスの機能情報の一部だけが含まれます。IRP をデバイススタックに送信すると、すべてのフィルタードライバーによる変更を含む全体像を収集できます。

Irp の送信の詳細については、「 [irp の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-irps)」を参照してください。 次の手順は、この IRP に特に適用されます。

-   [**\_デバイス機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)の構造をページプールから割り当て、 [**rtlゼロメモリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlzeromemory)を呼び出してゼロに初期化します。 **サイズ**を**sizeof**(**デバイス\_機能**) に、**バージョン**を1に、**アドレス**を-1**に初期**化します。

-   IRP の次の i/o スタックの場所の値を設定します: set **MajorFunction**を[**irp\_MJ\_PNP**](irp-mj-pnp.md)、 **minorfunction**を**\_irp の\_クエリ\_機能**に設定し、 **DeviceCapabilities**を割り当てられている**デバイス\_機能**の構造へのポインターに設定します。

-   **Iostatus を初期化します。** 状態はサポートされて\_いません\_。

-   不要になったときに、IRP および**デバイス\_機能**の構造の割り当てを解除します。

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


[**デバイス\_の機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_capabilities)

 

 




