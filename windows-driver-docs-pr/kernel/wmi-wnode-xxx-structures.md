---
title: WMI WNODE_XXX 構造体
description: WMI WNODE_XXX 構造体
ms.assetid: 9d059b9a-c129-42ba-8db6-53480003f56e
keywords:
- WMI の WDK カーネルでは、要求
- WDK の WMI の要求
- Irp WDK WMI
- WNODE_XXX 構造体
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53bb5d6bbc1713329753106b2063ebe526ca9157
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327251"
---
# <a name="wmi-wnodexxx-structures"></a>WMI れた WNODE\_XXX 構造体





WMI と呼ばれる標準的なデータ構造体のセットを使用して**れた WNODE\_* XXX*** 間ユーザー モードのデータ コンシューマーおよびカーネル モード ドライバーなどのデータ プロバイダーからデータを渡す。 ドライバーが呼び出すことによって WMI 要求を処理する場合[ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)、ドライバーは、読み取りまたは書き込みをする必要はありません**れた WNODE\_* XXX*** 構造体。 それ以外の場合、ドライバーは、入力を解釈する必要があります**れた WNODE\_* XXX*** で**Parameters.WMI.Buffer**または出力の書き込みを行う**れた WNODE\_* XXX*** するその場所。

次の表は、WMI の Irp とそれに対応する**れた WNODE\_* XXX*** 構造体。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>WMI の IRP</th>
<th>関連 WNODE_XXX 構造体</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550831" data-raw-source="[&lt;strong&gt;IRP_MN_CHANGE_SINGLE_INSTANCE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550831)"><strong>IRP_MN_CHANGE_SINGLE_INSTANCE</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566377" data-raw-source="[&lt;strong&gt;WNODE_SINGLE_INSTANCE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566377)"><strong>WNODE_SINGLE_INSTANCE</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550836" data-raw-source="[&lt;strong&gt;IRP_MN_CHANGE_SINGLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550836)"><strong>IRP_MN_CHANGE_SINGLE_ITEM</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566378" data-raw-source="[&lt;strong&gt;WNODE_SINGLE_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566378)"><strong>WNODE_SINGLE_ITEM</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550868" data-raw-source="[&lt;strong&gt;IRP_MN_EXECUTE_METHOD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff550868)"><strong>IRP_MN_EXECUTE_METHOD</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566376" data-raw-source="[&lt;strong&gt;WNODE_METHOD_ITEM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566376)"><strong>WNODE_METHOD_ITEM</strong></a></p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551650" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_ALL_DATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551650)"><strong>IRP_MN_QUERY_ALL_DATA</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566372" data-raw-source="[&lt;strong&gt;WNODE_ALL_DATA&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566372)"><strong>WNODE_ALL_DATA</strong></a></p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff551718" data-raw-source="[&lt;strong&gt;IRP_MN_QUERY_SINGLE_INSTANCE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff551718)"><strong>IRP_MN_QUERY_SINGLE_INSTANCE</strong></a></p></td>
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff566377" data-raw-source="[&lt;strong&gt;WNODE_SINGLE_INSTANCE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff566377)"><strong>WNODE_SINGLE_INSTANCE</strong></a></p></td>
</tr>
</tbody>
</table>

 

2 つ追加**れた WNODE\_* XXX*** 構造体、 [**れた WNODE\_イベント\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff566373)と[ **れた WNODE\_イベント\_参照**](https://msdn.microsoft.com/library/windows/hardware/ff566374)、有効なイベントの通知を送信するために使用します。 イベント ブロックを登録するドライバー、イベントが有効になっているし、イベントが発生した場合に通知を送信、イベントの WMI 呼び出しによって[ **IoWMIWriteEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff550520)を渡して、**れた WNODE\_イベント\_* XXX*** 構造体。 WMI イベントを送信する方法については、次を参照してください。 [WMI イベントの送信](sending-wmi-events.md)します。

各**れた WNODE\_* XXX***、次の構造で構成されます。

- 埋め込まれた[**れた WNODE\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff566375)すべてに共通の情報を含む構造体**れた WNODE\_* XXX***、バッファーのサイズなど種類を示す GUID をデータ ブロックを表し、フラグ**れた WNODE\_* XXX*** 構造体、静的または動的なインスタンス名、およびブロックの他の特性を使用するかどうか。

- 特定の固定メンバー**れた WNODE\_* XXX*** インスタンス名とデータのオフセットなどの構造体。

A**れた WNODE\_* XXX*** IRP バッファー内の構造 (**Parameters.WMI.Buffer**)、動的なインスタンス名の静的インスタンス名など、要求に関連する変数のデータは通常、その後入力文字列またはからメソッド、またはデータ ブロックの 1 つまたは複数のインスタンスのデータを出力します。 バッファーのサイズを超えることはそのため**sizeof (れた WNODE\_*XXX*)** 変数のデータの量が関係します。

ドライバーにより提供される変数のデータの型チェックを実行はない WMI ことに注意してください。 データ コンシューマーは、データを正しく解析できるように、ドライバーは出力バッファー内の適切な境界で出力データを配置する必要があります。 具体的には、各インスタンスが 8 バイト境界で開始する必要があり、その項目の各はドライバーによって以前登録されたデータ ブロックのスキーマによる自然な境界に配置する必要があります。 動的なインスタンス名は、2 バイト境界に配置できます。

次の図は、含んでいる IRP バッファーのブロック図、 [**れた WNODE\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff566377)ドライバーは、への応答で返す可能性のある構造体[ **IRP\_MN\_クエリ\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff551718)要求。

![れた wnode を含む、irp バッファーを示す図\-単一\-インスタンス](images/wnode-single-instance.png)

前の図の上部にある開始。

-   [**れた WNODE\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff566375)構造体の先頭に、 [**れた WNODE\_単一\_インスタンス**](https://msdn.microsoft.com/library/windows/hardware/ff566377)に含まれている、 **WnodeHeader**メンバー。 WMI のすべてのメンバーを設定、**れた WNODE\_ヘッダー**要求を送信する前にします。 **れた WNODE\_ヘッダー**:

    -   **WnodeHeader.Buffersize**のサイズを示します、**れた WNODE\_単一\_インスタンス**データ、構造体の固定のメンバーに依存してが含まれます。 (値の**WnodeHeader.Buffersize**が通常より小さい**Parameters.WMI.Buffersize**、ドライバーからの出力を受信する WMI によって割り当てられたバッファーのサイズを示します)。
    -   **WnodeHeader.Guid**データ ブロックを識別する GUID が含まれています。
    -   この例で**WnodeHeader.Flags**この構造体があることを示します、**れた WNODE\_単一\_インスタンス**静的データ ブロックを使用してインスタンス名。
-   WMI の設定、データ ブロックは、静的なインスタンス名を使用するため**InstanceIndex**ブロックが登録されているときに、ドライバーによって渡される静的なインスタンス名の一覧でインスタンスのインデックスにします。 **OffsetInstanceNames**は使用されません。

-   WMI セット**DataBlockOffset**をバッファーの先頭からインスタンス データの最初のバイトまでのオフセットを示します。 (ドライバーではこの値を変更する必要があります)もう一度データ ブロックは、静的なインスタンス名を使用しているため、このオフセットと同じ場所を示します**VariableData**します。 データ ブロックは、動的なインスタンス名を使用する場合、インスタンス名からスタート**VariableData**と**DataBlockOffset**はバッファーに大きいオフセットを指定します。

-   ドライバー セット**SizeDataBlock**に返されるインスタンス データのバイト数。

-   **VariableData** (データの後のインスタンス名、存在する場合)、ドライバーは出力バッファーに要求されたインスタンスのインスタンス データを書き込みます。

ドライバーの読み取りし、書き込み[**れた WNODE\_メソッド\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff566376)と[**れた WNODE\_単一\_項目**](https://msdn.microsoft.com/library/windows/hardware/ff566378)構造体と同様に**れた WNODE\_単一\_インスタンス**します。 これらの構造のように他の固定のメンバーがあるそれぞれに**OffsetInstanceName**、 **InstanceIndex**、 **DataBlockOffset**、 **SizeDataBlock** (またはの場合に**れた WNODE\_単一\_項目**、 **SizeDataItem**) と**VariableData**. **れた WNODE\_メソッド\_項目**が含まれています、**メソッド Id**と**れた WNODE\_単一\_項目**が含まれています、 **ItemId**を**れた WNODE\_単一\_インスタンス**が不足しています。

[**れた WNODE\_すべて\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff566372)を動的にインスタンス名を含めることも、データ ブロックの場合によってさまざまなサイズの複数のインスタンスを渡すために使用されるので、上記の構造は異なります。

次の図は、含んでいる IRP バッファーのブロック図、**れた WNODE\_すべて\_データ**ドライバーが応答を返す可能性のある、 [ **IRP\_MN\_クエリ\_すべて\_データ**](https://msdn.microsoft.com/library/windows/hardware/ff551650)要求。

![れた wnode を含む、irp バッファーを示す図\-すべて\-データ](images/wnode-all-data.png)

前の図の上部にある開始。

- 前の図の説明に従って、 [**れた WNODE\_ヘッダー** ](https://msdn.microsoft.com/library/windows/hardware/ff566375)構造体の先頭に、 [**れた WNODE\_すべて\_データ** ](https://msdn.microsoft.com/library/windows/hardware/ff566372)に含まれている、 **WnodeHeader**メンバー。 **WnodeHeader.Buffersize**と**WnodeHeader.Guid**のサイズを示す、**れた WNODE\_すべて\_データ**と、データ ブロックの GUID それぞれします。

  この例では、WMI 設定**WnodeHeader.Flags**をこの構造体があることを示す、**れた WNODE\_すべて\_データ**動的インスタンス データ ブロックが登録されていることと名前 (つまり、WMI はれた WNODE をクリアします。\_フラグ\_静的\_インスタンス\_名およびれた WNODE\_フラグ\_PDO\_インスタンス\_名)。 出力では、ドライバーがれた WNODE を設定\_フラグ\_固定\_インスタンス\_サイズのすべてのインスタンスが同じサイズでことを示します。

- WMI セット**DataBlockOffset**をバッファーの先頭からインスタンス データの最初のバイトまでのオフセットを示します。 (ドライバーは、この値を変更する必要がありますされません。) この例であるインスタンスの名前に依存してインスタンス データ**OffsetInstanceNameOffsets**します。

- ドライバー セット**InstanceCount**返されるインスタンスの数を示します。

- **れた WNODE\_* XXX*** データは、常に動的なインスタンス名を使用するブロックは、インスタンス名の文字列を含めることができます。 この例は、動的なインスタンス名を使用するため**OffsetInstanceNameOffsets**バッファー内の動的インスタンス名にオフセットの配列には、バッファーの先頭からのオフセットを示します。

- **FixedInstanceSize**ドライバーによって返される各インスタンス内のデータのバイト数を示します。 インスタンスがこのデータ ブロックのサイズが変化する場合は、ドライバーをれた WNODE オフ\_フラグ\_固定\_インスタンス\_サイズ**WnodeHeader.Flags**設定と**OffsetInstanceDataAndLength**の配列に**OFFSETINSTANCEDATAANDLENGTH**構造体の設定ではなく、そのインスタンス内のオフセット位置に 1 つのインスタンスとのバイト数のデータを指定する各**FixedInstanceSize**します。

詳細については**れた WNODE\_* XXX*** 構造体を参照してください[システム構造](https://msdn.microsoft.com/library/windows/hardware/ff564540)します。

 

 




