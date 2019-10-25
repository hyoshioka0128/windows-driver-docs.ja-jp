---
title: HDAUDIO_BUS_INTERFACE_BDL DDI オブジェクトの取得
description: HDAUDIO_BUS_INTERFACE_BDL DDI オブジェクトの取得
ms.assetid: 142eb2f0-6c6d-4441-8ad7-0875546c1ab2
keywords:
- HDAUDIO_BUS_INTERFACE_BDL 構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2531eac53ea9155fa46a45002aa11e31cfe1aa16
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830308"
---
# <a name="obtaining-an-hdaudio_bus_interface_bdl-ddi-object"></a>HDAUDIO\_BUS\_インターフェイス\_BDL DDI オブジェクトの取得


前に説明したように、オーディオまたはモデムコーデックの関数ドライバーは、hd audio DDI を使用してオブジェクトへのカウントされた参照を取得します。これによって、 [**IRP\_\_クエリ\_インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)IOCTL が hd オーディオバスドライバーに送信されます。

次の表は、関数ドライバーが IOCTL に書き込んで、 [**hdaudio\_BUS\_インターフェイス\_BDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)構造体と、この構造体である HD audio DDI のバージョンのコンテキストオブジェクトを取得するために、IOCTL に書き込む入力パラメーターの値を示しています。決まり.

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
<td align="left"><p><strong>GUID_HDAUDIO_BUS_INTERFACE_BDL</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT<em>サイズ</em></p></td>
<td align="left"><p><strong>sizeof</strong>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_BDL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)"><strong>HDAUDIO_BUS_INTERFACE_BDL</strong></a>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>USHORT<em>バージョン</em></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE<em>インターフェイス</em></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_BDL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)"><strong>HDAUDIO_BUS_INTERFACE_BDL</strong></a>構造体へのポインター</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID <em>InterfaceSpecificData</em></p></td>
<td align="left"><p><strong>空白</strong></p></td>
</tr>
</tbody>
</table>

 

関数ドライバーは、 [**Hdaudio\_BUS\_インターフェイス\_BDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)構造体にストレージを割り当て、IOCTL にこの構造体へのポインターを含めます。 上の表で、 **Hdaudio\_BUS\_インターフェイス\_BDL**構造体へのポインターは、型**pinterface**にキャストされています。これは、型[**インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface)の構造体へのポインターです。 **Hdaudio\_BUS\_インターフェイス\_BDL**の最初の5つのメンバーの名前と型は、**インターフェイス**の5つのメンバーのものと一致します。 **Hdaudio\_BUS\_インターフェイス\_BDL**には、DDI ルーチンへの関数ポインターである追加のメンバーが含まれています。 関数ドライバーからの IOCTL の受信に応答して、HD オーディオバスドライバーは、 **hdaudio\_bus\_インターフェイス\_BDL**構造全体に入力します。

次の表は、HD オーディオバスドライバーが、 [**hdaudio\_bus\_インターフェイス\_BDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)構造体の最初の5つのメンバーに書き込む値を示しています。

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
<td align="left"><p><strong>sizeof</strong>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_BDL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)"><strong>HDAUDIO_BUS_INTERFACE_BDL</strong></a>)</p></td>
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

 

上の表では、**コンテキスト**メンバーは、hdaudio\_BUS\_\_インターフェイスの特定のインスタンスに固有の情報を含むコンテキストオブジェクトを指しています。この情報は、クライアントがIOCTL. 前に説明したように、DDI でルーチンを呼び出すと、クライアント関数ドライバーは常に最初の呼び出しパラメーターとして**コンテキスト**ポインターの値を指定する必要があります。

 

 




