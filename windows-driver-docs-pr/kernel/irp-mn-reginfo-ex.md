---
title: IRP_MN_REGINFO_EX
description: この IRP は、ドライバーが IoWMIRegistrationControl を呼び出した後に、ドライバーの登録情報を照会または更新するために、WMI によって送信されます。
ms.date: 08/12/2017
ms.assetid: 2fdfd3b1-102d-4adb-af95-363201764bd5
keywords:
- IRP_MN_REGINFO_EX カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 87bd4eea2f9cc956e897a47a84bbed0af3e847da
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838565"
---
# <a name="irp_mn_reginfo_ex"></a>IRP\_\_REGINFO\_EX


この IRP は、ドライバーが[**Iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)を呼び出した後に、ドライバーの登録情報を照会または更新するために、WMI によって送信されます。 ドライバーは、wmi Irp を処理できます。詳細につい[**ては、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバーが、 **\_reginfo\_EX 要求の IRP\_** を処理するために、wmi を呼び出して、その[*ドライバーの*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback)[**設定を呼び出し**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)ます。

Microsoft Windows XP 以降のオペレーティングシステムでは、WMI をサポートするドライバーがこの IRP を処理する必要があります。 Microsoft Windows 98 および Windows 2000 をサポートするドライバーは、 [**IRP\_\_REGINFO**](irp-mn-reginfo.md)でも処理する必要があります。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)送信時
---------

Windows XP 以降では、ドライバーが[**Iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)を呼び出した後に、WMI がこの IRP を送信して、ドライバーの登録情報を照会または更新します。 Windows 98 および Windows 2000 では、WMI は**IRP\_の\_REGINFO**要求を代わりに送信します。

WMI は、システムスレッドのコンテキストで、この IRP を IRQL = パッシブ\_レベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


**Parameters. WMI. ProviderId**は、要求に応答する必要があるドライバーのデバイスオブジェクトを指します。 このポインターは、IRP 内のドライバーの i/o スタックの場所にあります。

**データパス**は、登録情報または更新のための**更新**を照会する**ために、** 設定に設定されています。

**パラメーター** . Wmi. BufferSize は、非ページバッファーの最大サイズを指定**し**ます。 このサイズは、(**sizeof**(の場合) + (*guidcount* \* **sizeof**(wmi regguid)) の合計以上である必要があります。ここで、 *guidcount*は、ドライバーによって登録されているデータブロックとイベントブロックの数、およびスペースで表されます。静的インスタンス名の場合 (存在する場合)。

## <a name="output-parameters"></a>出力パラメーター


ドライバーが *、の Wmi* irp を処理するときに、この[**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出すことによって、wmi irp を呼び出して、ドライバーのデータブロックの登録情報を取得します。

それ以外の場合、ドライバーは、次のように、パラメーターを指定し[**て、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmireginfow) **wmi. Buffer**に設定します。

-   **BufferSize**を、構成されているレジスタ**データとそれ**に関連付けられている登録データのサイズ (バイト単位) に設定します。

-   ドライバーが別のドライバーの代わりに WMI 要求を処理する場合、は、 **Nextwmireginfo**を、この情報の先頭から、登録情報を含む**別のユーザー設定の構造体**の**先頭までの**オフセット (バイト単位) に設定します。他のドライバーから。

-   **RegistryPath**を、ドライバーの[**driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンに渡されたレジストリパスに設定します。

-   データパスが " " に設定されている場合 **、は、** **MofResourceName**を、このこの**情報**の先頭から、そのイメージファイル内のドライバーの MOF リソースの名前を含むカウントされた Unicode 文字列へのオフセットに設定します。

-   **Guidcount**を、登録または更新するデータブロックとイベントブロックの数に設定します。

-   "Wmi **" で、** ドライバーによって公開されている各データブロックまたはイベントブロックに1つずつ、 [**wmi regguid 構造体**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)の配列を書き込みます。

ドライバーは、次のように各設定**Regguid**構造体を入力します。

-   **Guid**を、ブロックを識別する guid に設定します。

-   インスタンス名およびブロックのその他の特性に関する情報を提供する**フラグ**を設定します。 たとえば、ブロックが静的インスタンス名を使用して登録されている場合、ドライバーは、適切な WMI REG\_フラグ\_インスタンス\_*XXX*フラグを設定して**フラグ**を設定します。

ブロックが静的インスタンス名で登録されている場合、ドライバーは次のようになります。

-   **InstanceCount**をインスタンスの数に設定します。

-   次のいずれかのメンバーを、ブロックの静的インスタンス名データに対するバイト単位のオフセットに設定します。

    -   ドライバーに\_よって、InstanceNameList フラグ\_インスタンス\_一覧に**フラグ**が設定されている場合は、が静的インスタンス名の文字列のリストへのオフセットに設定されます。 WMI は、このリストにインデックスを指定して後続の要求のインスタンスを指定します。

    -   ドライバーによって、BaseNameOffset フラグが\_インスタンス\_インスタンス\_に**フラグ**が設定されている場合は、がベース名文字列へのオフセットに設定されます。 WMI はこの文字列を使用して、ブロックの静的インスタンス名を生成します。

    -   ドライバーによっ\_て、 [*ADDDEVICE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)フラグ\_インスタンス\_Pdo に**フラグ**が設定されている場合、pdo は、ドライバーのルーチンに渡される pdo へのポインターへのオフセット**に設定さ**れます。 WMI は PDO のデバイスインスタンスパスを使用して、ブロックの静的インスタンス名を生成します。 ドライバーは、 **Pdo**で渡された物理デバイスオブジェクトで[**obreferenceobject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)を呼び出す必要があります。 オブジェクトを逆参照するために、システムは[**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)を自動的に呼び出します。ドライバーはこれを行うことはできません。 (の場合は、 [**Wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を使用して irp を処理するドライバーでは、 **obreferenceobject**を呼び出す必要はありません。 WMI は、[*ドライバーの設定*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback)を呼び出す前に自動的にこれを実行します。

-   **InstanceNameList** **、基底クラス、また**は**pdo**によって示されるオフセットで、インスタンス名文字列、ベース名文字列、または pdo へのポインターを書き込みます。

ドライバーが別のドライバー (miniclass やミニポートドライバーなど) の代わりに WMI 登録を処理する場合は、他のドライバーの登録情報を使用して別の設定の**reginfo**構造体を設定し、前の構造で**Nextwmireginfo**に書き込みます。

**パラメーター**のバッファーが小さすぎてすべてのデータを受け取ることができない場合、ドライバーは、必要なサイズをバイト単位でパラメーターに書き込み**ます。** また、IRP は失敗し、ステータス\_バッファー\_\_小さすぎます。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーが、wmi[**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出すことによって irp を処理する場合、WMI は、i/o 状態ブロック内の**irp&gt;Iostatus. Status**と**Irp&gt;iostatus. 情報**を設定します。

それ以外の場合、ドライバーは**Irp&gt;iostatus. status**を STATUS\_SUCCESS に、または次のような適切なエラー状態に設定します。

状態\_バッファー\_\_小さすぎます

成功した場合、ドライバーは**Irp&gt;IoStatus**を設定します。これは、**パラメーター**によってバッファーに書き込まれたバイト数になります。

<a name="operation"></a>操作
---------

ドライバーが**IRP\_\_REGINFO\_EX**要求自体を処理している場合は、パラメーターが指定されている場合にのみ、ドライバーが[**Iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)に渡すポインターと同じデバイスオブジェクトを指している必要があり**ます。** それ以外の場合、ドライバーは、要求を次の下位のドライバーに転送する必要があります。

要求を処理する前に、ドライバーは**データパス**を確認して、wmi が登録情報を照会しているか (または **、更新を**要求している**か) を**確認する必要があります。

ドライバーは、この IRP を WMI レジスタと共に送信します。この場合、ドライバーは、wmi reg\_ACTION を使用して**Iowmiregistrationcontrol**を呼び出し、登録または wmi REG\_アクション\_再登録\_ます。 応答として、ドライバーは次のようにして、**パラメーター**にバッファーを格納する必要があります。

-   ドライバーのレジストリパス、その MOF リソースの名前、および登録するブロックの数を示す、 [**Wmi Reginfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmireginfow)構造体。

-   登録する各ブロックに対して1つの[**Wmi Regguid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)構造体。 ブロックが静的インスタンス名を使用して登録される場合、ドライバーは、そのブロックのため**に、適切**な\_フラグ\_インスタンス\_*XXX*フラグを設定します。

-   WMI では、静的インスタンス名を生成する必要があります。

ドライバーは、この IRP を WMI**更新**と共に送信します。これにより、ドライバーは、wmi REG\_ACTION\_UPDATE\_guid を使用して**Iowmiregistrationcontrol**を呼び出します。 応答として、ドライバーは、次に示すように、パラメーターには、 **wmi. buffer**の次のように入力します。

-   ブロックを削除するには、ドライバーによって、wmi の\_フラグが設定されます。このフラグは、その\_の構成体**Regguid**構造に\_GUID が削除されます。

-   ブロックを追加または更新する (たとえば、静的インスタンス名を変更する) には、ドライバーによって、WMI REG\_フラグがクリアされ、\_GUID\_削除され、ブロックの新しい登録値または更新された登録値が提供されます。

-   新規または既存のブロックを静的インスタンス名と共に登録するために、ドライバーは、適切な WMI REG\_フラグ\_インスタンス\_*XXX*に設定し、WMI が必要とするすべての文字列を指定して、静的インスタンス名を生成します。

ドライバーでは、ブロックを削除、追加、または更新するために、最初にすべてのブロックを登録するために使用されて**いるものと同じ構成**要素を使用できます。更新するブロックのフラグとデータのみを変更します。 このように、このような wmi **Reginfo** **構造内の**すべての wmi regguid が、そのブロックを最初に登録したときにドライバーによっ**て渡され**たものと一致する場合、WMI はブロックの更新に関連する処理をスキップします。

Wmi はドライバーからの追加情報を必要としないので、ドライバーは、wmi[**によっ\_\_て**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol) **\_REGINFO\_EX**要求を\_に送信します。 通常、ドライバーは\_デバイスの要求を[**削除\_\_IRP**](irp-mn-remove-device.md)に応答してブロックを解除します。

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


[*この情報を持つ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**WMB\_のコンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[ **"WMI REGGUID"** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)

[**WMI REGINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmireginfow)

[**Wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

[**IRP\_\_REGINFO**](irp-mn-reginfo.md)

 

 




