---
title: HDAUDIO_BUS_INTERFACE DDI オブジェクトの取得
description: HDAUDIO_BUS_INTERFACE DDI オブジェクトの取得
ms.assetid: 78667254-62a6-41fe-af36-43dbdea63aa8
keywords:
- HDAUDIO_BUS_INTERFACE 構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b7fa4c6387fdf310e43789cef60d9e5e215cb01
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832551"
---
# <a name="obtaining-an-hdaudio_bus_interface-ddi-object"></a>HDAUDIO\_BUS\_INTERFACE DDI オブジェクトの取得


次の表は、関数ドライバーが[**IRP\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)に書き込まれた入力パラメーターの値を示しています。これは、\_インターフェイス IOCTL を使用して、 [**HDAUDIO\_バス\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface)構造とコンテキストオブジェクトを取得します。この構造体で定義されている HD audio DDI のバージョン。

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
<td align="left"><p><strong>GUID_HDAUDIO_BUS_INTERFACE</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT<em>サイズ</em></p></td>
<td align="left"><p><strong>sizeof</strong>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface)"><strong>HDAUDIO_BUS_INTERFACE</strong></a>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>USHORT<em>バージョン</em></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE<em>インターフェイス</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface)"><strong>HDAUDIO_BUS_INTERFACE</strong></a>構造体へのポインター</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID <em>InterfaceSpecificData</em></p></td>
<td align="left"><p><strong>空白</strong></p></td>
</tr>
</tbody>
</table>

 

関数ドライバーは、 [**Hdaudio\_BUS\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface)構造のストレージを割り当て、IOCTL 内のこの構造体へのポインターを含みます。 上の表で、 **Hdaudio\_BUS\_インターフェイス**構造へのポインターは、型**pinterface**にキャストされています。これは、型[**インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface)の構造体へのポインターです。 **Hdaudio\_BUS\_インターフェイス**の最初の5つのメンバーの名前と型は、**インターフェイス**の5つのメンバーの名前と型に一致します。 **Hdaudio\_BUS\_インターフェイス**には、DDI ルーチンへの関数ポインターである追加のメンバーが含まれています。 関数ドライバーから IOCTL を受信すると、HD オーディオバスドライバーによって、 **hdaudio\_bus\_インターフェイス**構造全体がいっぱいになります。

次の表は、HD オーディオバスドライバーが、 [**hdaudio\_bus\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface)構造の最初の5つのメンバーに書き込む値を示しています。

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
<td align="left"><p><strong>sizeof</strong>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface)"><strong>HDAUDIO_BUS_INTERFACE</strong></a>)</p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT<strong>バージョン</strong></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID<strong>コンテキスト</strong></p></td>
<td align="left"><p>すべての DDI ルーチンに最初の呼び出しパラメーターとして渡す必要があるコンテキスト情報</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE_REFERENCE <strong>InterfaceReference</strong></p></td>
<td align="left"><p>コンテキストオブジェクトの参照カウントをインクリメントするルーチンへのポインター</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PINTERFACE_DEREFERENCE <strong>Interfacedereference 参照</strong></p></td>
<td align="left"><p>コンテキストオブジェクトの参照カウントをデクリメントするルーチンへのポインター</p></td>
</tr>
</tbody>
</table>

 

上の表では、**コンテキスト**メンバーは、クライアントが IOCTL から取得したベースライン HD オーディオ DDI の特定のインスタンスに固有の情報を含むコンテキストオブジェクトを指しています。 DDI 内のいずれかのルーチンを呼び出す場合、クライアント関数ドライバーは、常に最初の呼び出しパラメーターとして**コンテキスト**ポインター値を指定する必要があります。 コンテキスト情報はクライアントに対して非透過的です。 HD オーディオバスドライバーは、クライアントごとに異なるコンテキストオブジェクトを作成します。 コンテキストオブジェクトが不要になった場合、クライアントは、前の表に示されている**Interfacedereference 参照**ルーチンを呼び出すことによってコンテキストオブジェクトを解放します。 必要に応じて、クライアントは**InterfaceReference**ルーチンを呼び出すことによってオブジェクトへの追加の参照を作成できますが、クライアントは、不要になったときにこれらの参照を解放する必要があります。

 

 




