---
title: WMI WNODE_XXX 構造体
description: WMI WNODE_XXX 構造体
ms.assetid: 9d059b9a-c129-42ba-8db6-53480003f56e
keywords:
- WMI WDK カーネル、要求
- WDK WMI を要求する
- Irp WDK WMI
- WNODE_XXX 構造体
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 813e2d8e4a8a25087d57885d0fbd81a8480a0be8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838301"
---
# <a name="wmi-wnode_xxx-structures"></a>WMI WNODE\_XXX 構造体





WMI は、 **Wnode\_* XXX*** と呼ばれる一連の標準的なデータ構造を使用して、ユーザーモードのデータコンシューマーと、ドライバーなどのカーネルモードデータプロバイダーとの間でデータを渡します。 ドライバーが、の WMI 要求を処理するとき[**に、の wmi 要求を処理**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)する場合は、このドライバーは、 **WNODE\_* XXX*** 構造の読み取りまたは書き込みを行う必要はありません。 それ以外の場合、ドライバーは入力**wnode node**を解釈する必要があります **。** または、出力**wnode\_* xxx*** をその場所に書き込みます。または書き込みを行います。

次の表は、WMI Irp とそれに対応する**Wnode\_* XXX*** 構造を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>WMI IRP</th>
<th>関連する WNODE_XXX 構造体</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-instance" data-raw-source="[&lt;strong&gt;IRP_MN_CHANGE_SINGLE_INSTANCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-instance)"><strong>IRP_MN_CHANGE_SINGLE_INSTANCE</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance" data-raw-source="[&lt;strong&gt;WNODE_SINGLE_INSTANCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)"><strong>WNODE_SINGLE_INSTANCE</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-item" data-raw-source="[&lt;strong&gt;IRP_MN_CHANGE_SINGLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-item)"><strong>IRP_MN_CHANGE_SINGLE_ITEM</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item" data-raw-source="[&lt;strong&gt;WNODE_SINGLE_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)"><strong>WNODE_SINGLE_ITEM</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method" data-raw-source="[&lt;strong&gt;IRP_MN_EXECUTE_METHOD&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)"><strong>IRP_MN_EXECUTE_METHOD</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item" data-raw-source="[&lt;strong&gt;WNODE_METHOD_ITEM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)"><strong>WNODE_METHOD_ITEM</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_ALL_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data)"><strong>IRP_MN_QUERY_ALL_DATA</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data" data-raw-source="[&lt;strong&gt;WNODE_ALL_DATA&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data)"><strong>WNODE_ALL_DATA</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_SINGLE_INSTANCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)"><strong>IRP_MN_QUERY_SINGLE_INSTANCE</strong></a></p></td>
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance" data-raw-source="[&lt;strong&gt;WNODE_SINGLE_INSTANCE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)"><strong>WNODE_SINGLE_INSTANCE</strong></a></p></td>
</tr>
</tbody>
</table>

 

2つの追加の**wnode\_* XXX*** 構造体、 [**wnode\_イベント\_ITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_event_item)および[**WNODE\_イベント\_参照**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_event_reference)) を使用して、有効なイベントの通知を送信します。 イベントブロックを登録するドライバーは、イベントが有効になっていて、イベントが発生した場合に、 [**IoWMIWriteEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiwriteevent)を呼び出して**wnode\_イベント\_* XXX*** 構造体を渡すことによって、WMI にイベントの通知を送信します。 WMI イベントの送信の詳細については、「 [Wmi イベントの送信](sending-wmi-events.md)」を参照してください。

各**Wnode\_* XXX*** 構造体は、次の要素で構成されています。

- すべての**wnode\_* xxx*** に共通の情報 (バッファーのサイズ、データブロックを表す GUID、wnode の種類を示すフラグ\_* xxx) を含む、埋め込まれた[**WNODE\_ヘッダー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-_wnode_header)構造。* 構造体、静的または動的なインスタンス名を使用するかどうか、およびその他のブロックの特性。

- インスタンス名とデータへのオフセットなど、特定の**Wnode\_* XXX*** 構造体の固定メンバー。

IRP バッファー (**Parameters. WMI. buffer**) 内の**wnode\_* XXX*** 構造体には、通常、動的インスタンス名、静的インスタンス名文字列、メソッドからの出力、またはデータなど、要求に関連する変数データが続きます。データブロックの1つ以上のインスタンス。 このため、バッファーのサイズは、必要な変数データの量によって**sizeof (WNODE\_*XXX*)** を超える必要があります。

WMI は、ドライバーによって指定された変数データに対して型チェックを実行しないことに注意してください。 ドライバーは、データコンシューマーがデータを正しく解析できるように、出力バッファー内の適切な境界に出力データを配置する必要があります。 特に、各インスタンスは8バイトの境界で開始する必要があり、各インスタンスは、ドライバーによって以前に登録されたデータブロックスキーマに従って、自然な境界上に配置する必要があります。 動的インスタンス名は2バイト境界に配置できます。

次の図は、 [**Wnode\_単一の\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)構造を含む irp バッファーのブロック図を示しています。これは、 [**1 つの\_インスタンス\_の irp\_の\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)に応答して返される場合があります。申請.

![wnode\-1 つの\-インスタンスを含む irp バッファーを示す図](images/wnode-single-instance.png)

前の図の上部から開始します。

-   Wnode の先頭にある[**wnode\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-_wnode_header)構造体[ **\_1 つの\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)は、 **wnodeheader**メンバーに含まれています。 WMI は、要求を送信する前に**Wnode\_ヘッダー**のすべてのメンバーを入力します。 **Wnode\_ヘッダー**で、次のようにします。

    -   **Wnodeheader. Buffersize**は、構造体の固定メンバーの後に続くデータを含む、 **WNODE\_単一の\_インスタンス**のサイズを示します。 ( **Wnodeheader. buffersize**の値は通常、ドライバーからの出力を受信するために wmi によって割り当てられたバッファーのサイズを示し**ます)。**
    -   **Wnodeheader. guid**には、データブロックを識別する guid が含まれます。
    -   この例では、 **Wnodeheader. Flags**は、この構造体が**1 つの\_インスタンス\_wnode**であり、データブロックが静的インスタンス名を使用していることを示します。
-   データブロックでは静的インスタンス名が使用されるため、WMI は、ブロックの登録時にドライバーによって渡される静的インスタンス名のリスト内のインスタンスのインデックスに**Instanceindex**を設定します。 **OffsetInstanceNames**は使用されません。

-   WMI は、バッファーの先頭からインスタンスデータの最初のバイトまでの**オフセットを示すために、** データセットを設定します。 (ドライバーがこの値を変更することはできません)ここでも、データブロックは静的インスタンス名を使用するため、このオフセットは、**変数データ**と同じ場所を示します。 データブロックで動的インスタンス名が使用さ**れている**場合、インスタンス名は**変数 data**で開始され、データバッファーにはより大きいオフセットが指定されます。

-   ドライバーは、返されるインスタンスデータのバイト数に**sizesets ロック**を設定します。

-   **変数 data** (インスタンス名データがある場合) の場合、ドライバーは要求されたインスタンスのインスタンスデータを出力バッファーに書き込みます。

ドライバーは、wnode [ **\_メソッド\_item**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)と[**wnode\_単一\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)構造体を読み取り、書き込みます。これは、 **WNODE\_単一の\_インスタンス**とほぼ同じです。 これらの構造体は互いに似ていますが、それぞれに固定メンバー OffsetInstanceName、 **instanceindex**、 **lockoffset**、 **Size lock** (または **wnode node が SINGLE\_ITEM** **の場合は、SizeDataItem**) と**変数データ**。 **Wnode\_メソッド\_項目**には**MethodId**および**WNODE\_単一\_項目**が含まれています。1つの項目には、1つの\_インスタンスに存在しない**wnode\_** の**ItemId**が含まれます。

[**Wnode\_すべての\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data)は、データブロックの複数のインスタンスを渡すために使用されるという点で、前の構造とは異なります。動的なインスタンス名や、場合によっては、サイズが異なる可能性があります。

次の図は、 **Wnode\_すべての\_データ**を含む irp バッファーのブロック図を示しています。これにより、[**すべての\_データ要求\_irp\_の\_クエリ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data)に応答して、ドライバーが返す可能性があります。

![すべての\-データ\-wnode を含む irp バッファーを示す図](images/wnode-all-data.png)

前の図の上部から開始します。

- 前の図で説明したように、wnode の先頭にある[**wnode\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-_wnode_header)構造体は、[**すべての\_データ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data) **wnodeheader**メンバーに含まれています。 **Wnodeheader. Buffersize**および**Wnodeheader. Guid**は、wnode のサイズを示します。この値は、データブロックの**すべて\_データ**と Guid\_ます。

  この例では、WMI は**Wnodeheader. フラグ**を設定して、この構造体が**すべての\_データ\_wnode**であること、およびデータブロックが動的なインスタンス名で登録されたことを示します (つまり、wmi は wnode\_フラグ\_静的にクリア @no__ インスタンス\_NAMES と WNODE\_フラグ\_PDO\_インスタンス\_名)。 出力時に、ドライバーは WNODE\_フラグ\_固定\_\_インスタンスのサイズを設定して、すべてのインスタンスが同じサイズであることを示します。

- WMI は、バッファーの先頭からインスタンスデータの最初のバイトまでの**オフセットを示すために、** データセットを設定します。 (ドライバーはこの値を変更しないでください)。 この例では、インスタンスデータは**OffsetInstanceNameOffsets**のインスタンス名の後に続きます。

- ドライバーは、返されるインスタンスの数を示すように**InstanceCount**を設定します。

- **Wnode\_* XXX*** 動的インスタンス名を使用するデータブロックの場合は、常にインスタンス名文字列を格納します。 この例では動的なインスタンス名を使用しているため、 **OffsetInstanceNameOffsets**は、バッファーの先頭からバッファー内の動的インスタンス名へのオフセットの配列へのオフセットを示します。

- **FixedInstanceSize**は、ドライバーによって返される各インスタンス内のデータのバイト数を示します。 このデータブロックのインスタンスのサイズが変更された場合、ドライバーは**Wnodeheader**の wnode\_フラグ\_固定\_インスタンス\_サイズをクリアし、 **OffsetInstanceDataAndLength**をの**配列に設定します。OFFSETINSTANCEDATAANDLENGTH**構造体は、 **FixedInstanceSize**を設定する代わりに、1つのインスタンスのデータへのオフセットとそのインスタンスのバイト数を指定します。

**Wnode\_* XXX*** 構造体の詳細については、「[システム構造](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

 

 




