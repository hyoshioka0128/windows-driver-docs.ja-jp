---
title: HDAUDIO_BUS_INTERFACE_V2 DDI オブジェクトの取得
description: HDAUDIO_BUS_INTERFACE_V2 DDI オブジェクトの取得
ms.assetid: 3aad8c7a-8c89-499a-bfe8-e3facdffcd15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9f726cdcc0e3dd1a08f0b000966f9c989880103
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830301"
---
# <a name="obtaining-an-hdaudio_bus_interface_v2-ddi-object"></a>\_V2 DDI オブジェクトの HDAUDIO\_BUS\_INTERFACE の取得


次の表は、関数ドライバーが[**IRP\_\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)に書き込まれた入力パラメーター値を示しています。これは、 [**HDAUDIO\_BUS\_interface\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)構造体とこの構造体で定義されている HD audio DDI のバージョンのコンテキストオブジェクト。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>CONST GUID *<em>InterfaceType</em></p></td>
<td align="left"><p><strong>GUID_HDAUDIO_BUS_INTERFACE_V2</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT<em>サイズ</em></p></td>
<td align="left"><p><strong>sizeof</strong>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_V2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)"><strong>HDAUDIO_BUS_INTERFACE_V2</strong></a>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>USHORT<em>バージョン</em></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE<em>インターフェイス</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_V2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)"><strong>HDAUDIO_BUS_INTERFACE_V2</strong></a>構造体へのポインター</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID <em>InterfaceSpecificData</em></p></td>
<td align="left"><p><strong>空白</strong></p></td>
</tr>
</tbody>
</table>

 

関数ドライバーは、 [**Hdaudio\_BUS\_INTERFACE\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)構造体のストレージを割り当て、IOCTL にこの構造体へのポインターを含めます。 上の表で、 **Hdaudio\_BUS\_INTERFACE\_V2**構造体へのポインターは、型**pinterface**にキャストされています。これは、型[**インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface)の構造体へのポインターです。 **Hdaudio\_BUS\_interface\_V2**の最初の5つのメンバーの名前と種類は、**インターフェイス**の5つのメンバーの名前と型に一致します。 **Hdaudio\_BUS\_INTERFACE\_V2**には、DDI ルーチンへの関数ポインターである追加のメンバーが含まれています。 関数ドライバーからの IOCTL の受信に応答して、HD オーディオバスドライバーは、 **hdaudio\_bus\_INTERFACE\_V2**構造体を設定します。

次の表は、HD オーディオバスドライバーが、 [**hdaudio\_bus\_INTERFACE\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)構造体の最初の5つのメンバーに書き込む値を示しています。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メンバー</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>USHORT<strong>サイズ</strong></p></td>
<td align="left"><p><strong>sizeof</strong>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_V2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)"><strong>HDAUDIO_BUS_INTERFACE_V2</strong></a>)</p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT<strong>バージョン</strong></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID<strong>コンテキスト</strong></p></td>
<td align="left"><p>すべての DDI ルーチンに最初の呼び出しパラメーターとして渡す必要があるコンテキスト情報。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE_REFERENCE <strong>InterfaceReference</strong></p></td>
<td align="left"><p>コンテキストオブジェクトの参照カウントをインクリメントするルーチンへのポインター。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PINTERFACE_DEREFERENCE <strong>Interfacedereference 参照</strong></p></td>
<td align="left"><p>コンテキストオブジェクトの参照カウントをデクリメントするルーチンへのポインター。</p></td>
</tr>
</tbody>
</table>

 

前の表では、**コンテキスト**メンバーは、ベースライン HD オーディオ DDI の特定のインスタンスに固有の情報を含むコンテキストオブジェクトを指しています。 クライアントは、このベースライン HD オーディオ DDI を IOCTL から取得します。 クライアント関数ドライバーが、DDI 内のいずれかのルーチンを呼び出す場合は、常に最初の呼び出しパラメーターとして**コンテキスト**メンバーの値を指定する必要があります。 コンテキスト情報はクライアントに対して非透過的です。 HD オーディオバスドライバーは、クライアントごとに異なるコンテキストオブジェクトを作成します。 コンテキストオブジェクトが不要になった場合、クライアントは、前の表に示した**Interfacedereference 参照**ルーチンを呼び出すことによってコンテキストオブジェクトを解放します。 必要に応じて、クライアントは**Interfacedereference**参照ルーチンを呼び出すことによって、オブジェクトへの追加の参照を作成できますが、クライアントは、これらの参照を不要になったときに解放する必要があります。

 

 




