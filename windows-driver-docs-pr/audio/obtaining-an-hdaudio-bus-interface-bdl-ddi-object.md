---
title: HDAUDIO_BUS_INTERFACE_BDL DDI オブジェクトの取得
description: HDAUDIO_BUS_INTERFACE_BDL DDI オブジェクトの取得
ms.assetid: 142eb2f0-6c6d-4441-8ad7-0875546c1ab2
keywords:
- HDAUDIO_BUS_INTERFACE_BDL 構造体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50efee7a85e88e362dc9f591459350fed0d4516a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355345"
---
# <a name="obtaining-an-hdaudiobusinterfacebdl-ddi-object"></a>取得、HDAUDIO\_BUS\_インターフェイス\_BDL DDI オブジェクト


前の説明、関数ドライバー、オーディオまたはモデムのコーデックが送信することによって、HD オーディオ DDI を持つオブジェクトへの参照をカウントを取得するため、 [ **IRP\_MN\_クエリ\_インターフェイス** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface) IOCTL HD オーディオ バス ドライバーにします。

次の表に、入力パラメーターの値を取得する IOCTL に書き込みを行う関数ドライバー、 [ **HDAUDIO\_BUS\_インターフェイス\_BDL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)構造体をこの構造体を定義する HD オーディオ DDI のバージョンのコンテキスト オブジェクト。

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
<td align="left"><p><strong>sizeof</strong>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_BDL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)"><strong>HDAUDIO_BUS_INTERFACE_BDL</strong></a>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>USHORT<em>バージョン</em></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE<em>インターフェイス</em></p></td>
<td align="left"><p>ポインター <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_BDL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)"> <strong>HDAUDIO_BUS_INTERFACE_BDL</strong> </a>構造体</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID <em>InterfaceSpecificData</em></p></td>
<td align="left"><p><strong>NULL</strong></p></td>
</tr>
</tbody>
</table>

 

Function ドライバーの記憶域の割り当て、 [ **HDAUDIO\_BUS\_インターフェイス\_BDL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)構造し、IOCTL でこの構造体へのポインターが含まれています。 前の表へのポインター、 **HDAUDIO\_BUS\_インターフェイス\_BDL**構造が型にキャスト**PINTERFACE**構造体へのポインターであります。型[**インターフェイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_interface)します。 名前と型の最初の 5 つのメンバーの**HDAUDIO\_BUS\_インターフェイス\_BDL**の 5 つのメンバーに合わせて**インターフェイス**します。 **HDAUDIO\_BUS\_インターフェイス\_BDL** DDI ルーチンへの関数ポインターであるその他のメンバーが含まれています。 関数ドライバーからの IOCTL の受信に応答してでは、HD オーディオ バス ドライバー、全体で塗りつぶします**HDAUDIO\_BUS\_インターフェイス\_BDL**構造体。

次の表は、値の最初の 5 つのメンバーに、HD オーディオ バス ドライバーを記述、 [ **HDAUDIO\_BUS\_インターフェイス\_BDL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)構造体。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Member</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>USHORT<strong>サイズ</strong></p></td>
<td align="left"><p><strong>sizeof</strong>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_BDL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)"><strong>HDAUDIO_BUS_INTERFACE_BDL</strong></a>)</p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT<strong>バージョン</strong></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID<strong>コンテキスト</strong></p></td>
<td align="left"><p>最初の呼び出しのパラメーターとして各 DDI ルーチンに渡すことが必要なコンテキスト情報</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE_REFERENCE <strong>InterfaceReference</strong></p></td>
<td align="left"><p>コンテキスト オブジェクトの参照カウントをインクリメントするルーチンへのポインター</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PINTERFACE_DEREFERENCE <strong>InterfaceDereference</strong></p></td>
<td align="left"><p>ルーチンへのポインターをコンテキスト オブジェクトの参照カウントをデクリメント</p></td>
</tr>
</tbody>
</table>

 

上記の表に、**コンテキスト**メンバーが、HDAUDIO の特定のインスタンスに固有の情報が含まれるコンテキスト オブジェクトを指す\_BUS\_インターフェイス\_BDL バージョンのこの DDI IOCTL からクライアントを取得します。 クライアント機能のドライバーが常に指定する必要があります、DDI でルーチンのいずれかを呼び出すときに、前の説明、**コンテキスト**最初の呼び出しのパラメーターとしてのポインターの値。

 

 




