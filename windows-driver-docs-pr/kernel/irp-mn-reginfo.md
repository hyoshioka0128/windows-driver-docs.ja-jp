---
title: IRP_MN_REGINFO
description: Microsoft Windows 98 および Microsoft Windows 2000 で WMI をサポートするドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: db93b64b-a2e4-429d-850e-921fb438467c
keywords:
- IRP_MN_REGINFO カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: bf9eff4f32befa3262e7891ef2030fad99de51fb
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922569"
---
# <a name="irp_mn_reginfo"></a>IRP\_の\_全レジストリ情報


Microsoft Windows 98 および Microsoft Windows 2000 で WMI をサポートするドライバーは、この IRP を処理する必要があります。 (Windows XP でもサポートされているドライバーは[**、\_irp\_の全\_レジストリ情報**](irp-mn-reginfo-ex.md)を処理する必要があります)。ドライバーは、wmi Irp を処理できます。詳細につい[**ては、**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)

<a name="when-sent"></a>送信時
---------

Windows 98 および Windows 2000 では、ドライバーが[**Iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)を呼び出した後に、WMI がこの IRP を送信して、ドライバーの登録情報を照会または更新します。 Windows XP 以降では、WMI によっ**て\_IRP\_の新しい\_reginfo EX**要求が代わりに送信されます。

WMI は、システムスレッドのコンテキストで\_、この IRP を IRQL = パッシブレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


**Parameters. WMI. ProviderId**は、要求に応答する必要があるドライバーのデバイスオブジェクトを指します。 このポインターは、IRP 内のドライバーの i/o スタックの場所にあります。

**データパス**は、登録情報または更新のための**更新**を照会する**ために、** 設定に設定されています。

**パラメーター** . Wmi. BufferSize は、非ページバッファーの最大サイズを指定**し**ます。 このサイズは、(**sizeof****(の場合) +**(*guidcount* \* **sizeof**(設定された**regguid**)) の合計以上である必要があります。ここで、 *guidcount*は、ドライバーによって登録されるデータブロックとイベントブロックの数、および静的インスタンス名 (存在する場合) の領域になります。

## <a name="output-parameters"></a>出力パラメーター


ドライバーが[*、の Wmi*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback) irp を処理するときに、この[**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出すことによって、wmi irp を呼び出して、ドライバーのデータブロックの登録情報を取得します。

それ以外の場合、ドライバーは、次のように、パラメーターを指定し[**て、**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmireginfow) **wmi. Buffer**に設定します。

-   **BufferSize**を、構成されているレジスタ**データとそれ**に関連付けられている登録データのサイズ (バイト単位) に設定します。

-   ドライバーが別のドライバーの代わりに WMI 要求を処理する場合、は、 **Nextwmireginfo**を、この参照元**から他の**ドライバーからの登録情報を含む別のユーザー設定構造の**先頭までの**オフセット (バイト単位) に設定します。

-   **RegistryPath**を、ドライバーの[**driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンに渡されたレジストリパスに設定します。

-   データパスが " **Parameters.WMI.Datapath** " に設定されている場合 **、は、** **MofResourceName**を、このこの**情報**の先頭から、そのイメージファイル内のドライバーの MOF リソースの名前を含むカウントされた Unicode 文字列へのオフセットに設定します。

-   **Guidcount**を、登録または更新するデータブロックとイベントブロックの数に設定します。

-   "Wmi **" で、** ドライバーによって公開されている各データブロックまたはイベントブロックに1つずつ、 [**wmi regguid 構造体**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)の配列を書き込みます。

ドライバーは、次のように各設定**Regguid**構造体を入力します。

-   **Guid**を、ブロックを識別する guid に設定します。

-   インスタンス名およびブロックのその他の特性に関する情報を提供する**フラグ**を設定します。 たとえば、ブロックが静的インスタンス名を使用して登録されている場合、ドライバーは、適切な\_wmi\_reg\_フラグインスタンス*XXX*フラグを使用して**フラグ**を設定します。

ブロックが静的インスタンス名で登録されている場合、ドライバーは次のようになります。

-   **InstanceCount**をインスタンスの数に設定します。

-   次のいずれかのメンバーを、ブロックの静的インスタンス名データに対するバイト単位のオフセットに設定します。
    -   ドライバーによって**フラグ**が設定さ\_れ\_て\_いるとして、インスタンスの一覧を表示する、 **InstanceNameList**静的インスタンス名の文字列のリストへのオフセットを設定します。 WMI は、このリストにインデックスを指定して後続の要求のインスタンスを指定します。
    -   ドライバーが WMI REG **Flags** \_FLAG\_インスタンス\_ベースのフラグを設定すると、 **BaseNameOffset**がベース名文字列へのオフセットに設定されます。 WMI はこの文字列を使用して、ブロックの静的インスタンス名を生成します。
    -   ドライバーによって **、フラグ**が AddDevice\_reg\_フラグ\_インスタンス PDO に設定されている場合、 **pdo**は、ドライバーの[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)ルーチンに渡される pdo へのポインターへのオフセットに設定されます。 WMI は PDO のデバイスインスタンスパスを使用して、ブロックの静的インスタンス名を生成します。
-   **InstanceNameList** **、基底クラス、また**は**pdo**によって示されるオフセットで、インスタンス名文字列、ベース名文字列、または pdo へのポインターを書き込みます。

ドライバーが別のドライバー (miniclass やミニポートドライバーなど) の代わりに WMI 登録を処理する場合は、他のドライバーの登録情報を使用して別の設定の REGINFO 構造体を設定し、前の構造で**Nextwmireginfo**に書き込みます。

**パラメーター**に格納されているバッファーが小さすぎてすべてのデータを受信できない場合、ドライバーは、必要なサイズをバイト単位で **、パラメーター**に ULONG として書き込み、IRP に失敗\_し\_、\_ステータスバッファーを返します。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーが、wmi[**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出すことによって irp を処理する場合、WMI は、i/o 状態ブロック内の**irp-&gt;Iostatus. status**と**irp-&gt;iostatus. 情報**を設定します。

それ以外の場合は、ドライバーによって、 **Irp-&gt;Iostatus. STATUS**が正常状態\_に設定されるか、次のような適切なエラー状態に設定されます。

ステータス\_バッファー\_が\_小さすぎます

成功した場合、ドライバーは、 **Irp-&gt;iostatus**を設定します。これは、**パラメーター**によってバッファーに書き込まれたバイト数になります。

<a name="operation"></a>Operation
---------

ドライバーは、wmi Irp を処理できます。詳細につい[**ては、**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバー[**が、この**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)ルーチンを呼び出して、wmi irp を処理する場合は、そのルーチンは、[*ドライバーの \n*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback)呼び出しを呼び出します。

ドライバーが**\_\_IRP**を処理する reginfo 要求自体を処理する場合は、ドライバーが[**iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)に渡すポインターと同じデバイスオブジェクトを指す場合にのみ、このようにし**ます。** それ以外の場合、ドライバーは、要求を次の下位のドライバーに転送する必要があります。

要求を処理する前に、ドライバーは**データパス**を確認して、wmi が登録情報を照会しているか (または **、更新を**要求している**か) を**確認する必要があります。

この IRP は、ドライバーによって、呼び出し元の\_アクション\_レジスタまたは wmi\_reg action\_の再登録を使用して**iowmiregistrationcontrol**が呼び出された後に、wmi によってこの IRP が送信されます。 応答として、ドライバーは次のようにして、**パラメーター**にバッファーを格納する必要があります。

-   ドライバーのレジストリパス、その MOF リソースの名前、および登録するブロックの数を示す、 [**Wmi Reginfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmireginfow)構造体。

-   登録する各ブロックに対して1つの[**Wmi Regguid**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)構造体。 ブロックが静的インスタンス名を使用して登録される場合、ドライバーは、そのブロック\_の\_ため\_の適切なインターフェイス reg フラグインスタンス*XXX*フラグを**設定します**。

-   WMI では、静的インスタンス名を生成する必要があります。

WMI は、ドライバーが wmi\_reg ACTION\_\_Update Guid を使用して**iowmiregistrationcontrol**を呼び出した後に、この IRP を wmi**更新**と共に送信します。 応答として、ドライバーは、次に示すように、パラメーターには、 **wmi. buffer**の次のように入力します。

-   ブロックを削除するために、ドライバーは、\_その\_よう\_に設定された**regguid**構造内の wmi reg フラグを削除します。

-   ブロックを追加または更新する (たとえば、静的インスタンス名を変更する) には、ドライバーによっ\_て\_、\_wmi reg フラグの削除 GUID がクリアされ、ブロックの新規または更新された登録値が提供されます。

-   新規または既存のブロックを静的インスタンス名と共に登録するために、ドライバー\_は\_適切\_な wmi reg フラグインスタンス*XXX*を設定し、WMI が必要とするすべての文字列を指定して、静的インスタンス名を生成します。

ドライバーでは、ブロックを削除、追加、または更新するために、最初にすべてのブロックを登録するために使用されて**いるものと同じ構成**要素を使用できます。更新するブロックのフラグとデータのみを変更します。 このように、このような wmi **Reginfo** **構造内の**すべての wmi regguid が、そのブロックを最初に登録したときにドライバーによっ**て渡され**たものと一致する場合、WMI はブロックの更新に関連する処理をスキップします。

Wmi は、ドライバーからの追加情報を必要としないため、wmi では、呼び出し元の\_アクション\_の登録を使用して[**iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)を呼び出すと、IRP **\_\_** が完了した reginfo 要求を送信しません。 通常、ドライバーは、 [**IRP\_\_\_**](irp-mn-remove-device.md)によって削除されたデバイスの要求に応じてブロックを解除します。

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


[*この情報を持つ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**WMB\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**"WMI REGGUID"**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)

[**WMI REGINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmireginfow)

[**Wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

[**IRP\_の\_全レジストリ\_情報 EX**](irp-mn-reginfo-ex.md)

 

 




