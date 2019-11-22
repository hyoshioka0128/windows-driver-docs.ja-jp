---
title: IRP_MN_QUERY_ALL_DATA
description: WMI をサポートするすべてのドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 9d4e1c2e-73ad-4fc3-99e6-391a64edfa5c
keywords:
- IRP_MN_QUERY_ALL_DATA カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: d1ef368fe4437e52f9bc02061de0bb051cc23677
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838577"
---
# <a name="irp_mn_query_all_data"></a>IRP\_\_クエリ\_すべての\_データ


WMI をサポートするすべてのドライバーは、この IRP を処理する必要があります。 ドライバーは、wmi Irp を処理できます。詳細につい[**ては、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバーが、**すべての\_データ要求\_\_クエリ**を実行するために、条件によって\_が実行された場合、WMI はその[*ドライバーのその*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)ドライバーの[**設定を呼び出し**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)ます。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)送信時
---------

WMI は、特定のデータブロックのすべてのインスタンスを照会するために、この IRP を送信します。

WMI は、任意のスレッドコンテキストで、IRQL = パッシブ\_レベルでこの IRP を送信します。

## <a name="input-parameters"></a>入力パラメーター


パラメーター。 IRP 内のドライバーの i/o スタックの場所にある**WMI. ProviderId**は、要求に応答するドライバーのデバイスオブジェクトを指します。

**データパス**は、データブロックを識別する GUID を指します。

**パラメーター** 。 Wmi. BufferSize は、要求から出力データを**受け取る、非**ページバッファーの最大サイズを示します。 バッファーサイズは、 **sizeof**(**wnode\_すべての\_データ**) と、返されるすべてのインスタンスのインスタンス名とデータのサイズを足した値以上である必要があります。

## <a name="output-parameters"></a>出力パラメーター


ドライバーが、の WMI Irp を処理する[**場合、wmi は、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)ドライバーによって登録された各ブロックに対して1回、*ドライバーの設定*を呼び出して、すべての **\_データを\_** します。

それ以外の場合は、次のように、ドライバーは[**Wnode\_すべての\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data)構造を**パラメーター. WMI. Buffer**に入力します。

-   **Wnodeheader. BufferSize**を、返される**すべての\_データ\_の wnode**全体のバイト数に設定し、 **Wnodeheader. Timestamp**を**kequerysystemtime**によって返される値に設定して、 **wnodeheader. Flags を設定します。** 返されるデータに適しています。

-   **InstanceCount**を、返されるインスタンスの数に設定します。

-   ブロックで動的インスタンス名が使用されている場合、は、 **OffsetInstanceNameOffsets**を wnode の先頭からのオフセット (バイト単位) に設定します。これにより、**すべての\_データ\_** 、ULONG オフセットの配列が開始されます。 この配列の各要素は、Wnode からのオフセットであり、各動的インスタンス名が格納されている**すべての\_データ\_** ます。 各動的インスタンス名はカウントされた Unicode 文字列として格納され、カウントの後に Unicode 文字列が続きます。 このカウントには、Unicode 文字列に含まれる可能性のある終端の null 文字は含まれません。 Unicode 文字列に終端の null 文字が含まれている場合でも、この null 文字は**Wnodeheader. BufferSize**で設定されたサイズ内に収まる必要があります。

-   すべてのインスタンスが同じサイズの場合:
    -   Wnodeheader の\_固定\_インスタンス\_サイズに WNODE\_フラグを設定し、 **FixedInstanceSize**をそのサイズ (バイト単位) に設定し**ます。**
    -   各インスタンスが8バイト境界にアラインされるように、データを埋め込み、データを埋め込み、インスタンス**データを書き込み**ます。 たとえば、 **FixedInstanceSize**が6の場合、ドライバーはインスタンス間に2バイトのパディングを追加します。
-   インスタンスのサイズが異なる場合:
    -   Wnodeheader の WNODE\_フラグ\_固定\_インスタンス\_サイズをクリアし、 **OFFSETINSTANCEDATAANDLENGTH**から始まる**InstanceCount** **OFFSETINSTANCEDATAANDLENGTH**構造体の配列を書き込み**ます。** 各**OFFSETINSTANCEDATAANDLENGTH**構造体は、 **Wnode\_node**の先頭から、各インスタンスのデータの先頭とデータの長さまでのオフセットをバイト単位で指定します。\_ 使用**されて**いません。

    -   **OffsetInstanceDataAndLength**配列の最後の要素の後にインスタンスデータを書き込み、各インスタンスを8バイトの境界に合わせて埋め込みます。

**パラメーター**のバッファーが小さすぎてすべてのデータを受け取ることができない場合、ドライバーは[**wnode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_too_small)に必要なサイズを入力するだけで、**パラメーター**の\_の小さな構造\_ます。 バッファーが**sizeof**(**wnode\_が\_小さい**) より小さい場合、ドライバーは IRP に失敗し、ステータス\_バッファー\_\_小さすぎることを返します。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーが、wmi[**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出すことによって irp を処理する場合、WMI は、i/o 状態ブロック内の**irp&gt;Iostatus. Status**と**Irp&gt;iostatus. 情報**を設定します。

それ以外の場合、ドライバーは**Irp&gt;iostatus. status**を STATUS\_SUCCESS に、または次のような適切なエラー状態に設定します。

状態\_バッファー\_\_小さすぎます

ステータス\_WMI\_GUID\_見つかりませんでした\_

成功した場合、ドライバーは**Irp&gt;IoStatus**を設定します。これは、**パラメーター**によってバッファーに書き込まれたバイト数になります。

<a name="operation"></a>操作
---------

ドライバーは、wmi Irp を処理できます。詳細につい[**ては、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバー[**が、この**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)ルーチンを呼び出して、Wmi の irp を処理する場合、このルーチンは、[*ドライバーの、そのルーチンを*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)呼び出します。

ドライバーが**IRP\_\_クエリ**を処理する場合は、すべての\_データ要求\_、**パラメーター**が指定されている場合にのみ、ドライバーが[**iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)に渡された同じデバイスオブジェクトを指している必要があります。 それ以外の場合、ドライバーは、要求を次の下位のドライバーに転送する必要があります。

ドライバーは、要求を処理する前に、**データパス**がドライバーでサポートされている GUID を指しているかどうかを判断する必要があります。 それ以外の場合は、ドライバーが IRP を失敗させ、ステータスを返す必要があります。 WMI\_GUID\_見つかりませ\_ん\_ます。

ドライバーがデータブロックをサポートしている場合は、次の操作を行う必要があります。

-   **パラメーター**で、ドライバーが返すすべてのデータを受け取るのに十分な大きさのバッファーが指定されていることを確認します。

-   [**Wnode\_すべての\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data)構造を、そのデータブロックのすべてのインスタンスの**データと共に格納します**。

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


[*すべてのクエリを*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**KeQuerySystemTime**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kequerysystemtime)

[**WMB\_のコンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**Wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE\_すべての\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data)

 

 




