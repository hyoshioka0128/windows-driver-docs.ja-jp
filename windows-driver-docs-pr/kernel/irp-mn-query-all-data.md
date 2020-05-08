---
title: IRP_MN_QUERY_ALL_DATA
description: WMI をサポートするすべてのドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 9d4e1c2e-73ad-4fc3-99e6-391a64edfa5c
keywords:
- IRP_MN_QUERY_ALL_DATA カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: b8dea79565dd0f25bc996217b452b7d871692981
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922478"
---
# <a name="irp_mn_query_all_data"></a>IRP\_は\_すべて\_\_のデータを照会します


WMI をサポートするすべてのドライバーは、この IRP を処理する必要があります。 ドライバーは、wmi Irp を処理できます。詳細につい[**ては、**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバーが、**すべて\_\_\_のデータ要求の IRP\_** を処理[**するために**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)、呼び出し元を呼び出す場合、WMI はその[*ドライバーの設定*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)されたクエリを呼び出します。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)

<a name="when-sent"></a>送信時
---------

WMI は、特定のデータブロックのすべてのインスタンスを照会するために、この IRP を送信します。

WMI は、任意のスレッドコンテキストで\_この IRP を IRQL = パッシブレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


パラメーター。 IRP 内のドライバーの i/o スタックの場所にある**WMI. ProviderId**は、要求に応答するドライバーのデバイスオブジェクトを指します。

**データパス**は、データブロックを識別する GUID を指します。

**パラメーター** 。 Wmi. BufferSize は、要求から出力データを**受け取る、非**ページバッファーの最大サイズを示します。 バッファーサイズは、 **sizeof**(**\_wnode すべて\_のデータ**) と、すべてのインスタンスのインスタンス名とデータのサイズを加算した値以上である必要があります。

## <a name="output-parameters"></a>出力パラメーター


ドライバーが WMI [**irp を処理**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)する場合には、wmi は、ドライバーによって登録された各ブロックに対して、*ドライバーの* **\_すべて\_のデータ**を渡します。

それ以外の場合、ドライバーは[**Wnode\_の\_すべてのデータ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data)構造を次のようにパラメーターに入力**し**ます。

-   **Wnodeheader. BufferSize**を、返される**\_すべて\_のデータ**のバイト数に設定し、 **wnodeheader. Timestamp**を**kequerysystemtime**によって返される値に設定し、返されるデータに適切な**wnodeheader. フラグ**を設定します。

-   **InstanceCount**を、返されるインスタンスの数に設定します。

-   ブロックで動的インスタンス名が使用されている場合、は**OffsetInstanceNameOffsets**を、 **wnode\_\_** の先頭からのオフセット (バイト単位) に設定します。これにより、ULONG オフセットの配列が開始されます。 この配列の各要素は、各動的インスタンス名が格納される**\_wnode すべて\_のデータ**からのオフセットです。 各動的インスタンス名はカウントされた Unicode 文字列として格納され、カウントの後に Unicode 文字列が続きます。 このカウントには、Unicode 文字列に含まれる可能性のある終端の null 文字は含まれません。 Unicode 文字列に終端の null 文字が含まれている場合でも、この null 文字は**Wnodeheader. BufferSize**で設定されたサイズ内に収まる必要があります。

-   すべてのインスタンスが同じサイズの場合:
    -   Wnodeheader\_の\_wnode フラグ固定\_インスタンス\_サイズを設定し、 **FixedInstanceSize**をそのサイズ (バイト単位) に設定し**ます。**
    -   各インスタンスが8バイト境界にアラインされるように、データを埋め込み、データを埋め込み、インスタンス**データを書き込み**ます。 たとえば、 **FixedInstanceSize**が6の場合、ドライバーはインスタンス間に2バイトのパディングを追加します。
-   インスタンスのサイズが異なる場合:
    -   Wnodeheader\_の\_\_wnode\_フラグ固定インスタンスサイズをクリアし、 **OFFSETINSTANCEDATAANDLENGTH**から始まる**InstanceCount** **OFFSETINSTANCEDATAANDLENGTH**構造体の配列を書き込み**ます。** 各**OFFSETINSTANCEDATAANDLENGTH**構造体は、 **wnode\_\_すべてのデータ**構造体の先頭から各インスタンスのデータの先頭までのオフセット (バイト単位)、およびデータの長さを指定します。 使用**されて**いません。

    -   **OffsetInstanceDataAndLength**配列の最後の要素の後にインスタンスデータを書き込み、各インスタンスを8バイトの境界に合わせて埋め込みます。

**パラメーター**のバッファーが小さすぎてすべてのデータを受け取ることができない場合、ドライバーは、wnode では、必要なサイズが小さすぎて[**wnode\_\_**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_too_small)によって小さすぎる構造**になります**。 バッファーが**sizeof**(**wnode\_が\_小さすぎる**) より小さい場合、ドライバーは IRP に失敗し、ステータス\_バッファー\_が\_小さすぎます。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーが、wmi[**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出すことによって irp を処理する場合、WMI は、i/o 状態ブロック内の**irp-&gt;Iostatus. status**と**irp-&gt;iostatus. 情報**を設定します。

それ以外の場合は、ドライバーによって、 **Irp-&gt;Iostatus. STATUS**が正常状態\_に設定されるか、次のような適切なエラー状態に設定されます。

ステータス\_バッファー\_が\_小さすぎます

状態\_WMI\_GUID\_が\_見つかりません

成功した場合、ドライバーは、 **Irp-&gt;iostatus**を設定します。これは、**パラメーター**によってバッファーに書き込まれたバイト数になります。

<a name="operation"></a>Operation
---------

ドライバーは、wmi Irp を処理できます。詳細につい[**ては、**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバー[**が、この**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)ルーチンを呼び出して、Wmi の irp を処理する場合、このルーチンは、[*ドライバーの、そのルーチンを*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)呼び出します。

ドライバーが**\_IRP\_\_\_** を処理するすべてのデータ要求を処理する場合は、パラメーターが指定されている場合にのみ、ドライバーが[**iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)に渡す同じデバイスオブジェクトを指すようにする必要があります **。** それ以外の場合、ドライバーは、要求を次の下位のドライバーに転送する必要があります。

ドライバーは、要求を処理する前に、**データパス**がドライバーでサポートされている GUID を指しているかどうかを判断する必要があります。 一致していない場合は、ドライバーが IRP を\_失敗\_さ\_せ\_、ステータス WMI GUID が見つからないことを返します。

ドライバーがデータブロックをサポートしている場合は、次の操作を行う必要があります。

-   **パラメーター**で、ドライバーが返すすべてのデータを受け取るのに十分な大きさのバッファーが指定されていることを確認します。

-   [**Wnode\_のすべて\_のデータ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data)構造に、そのデータブロックのすべてのインスタンスのデータを格納します。 **Parameters.WMI.Buffer**

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


[*すべてのクエリを*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**KeQuerySystemTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequerysystemtime)

[**WMB\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**Wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE\_すべて\_のデータ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data)

 

 




