---
title: センサーパラメーターの型について
description: パラメーターの型について
ms.assetid: 392ea7b9-df6f-4d47-9367-a167c0656dd4
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0b7f4e362dbc0d913e2d8029e8a218f2ecf79658
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842377"
---
# <a name="about-sensor-parameter-types"></a>センサーパラメーターの型について


センサークラス拡張によって、いくつかのデータ型がメソッドパラメーターとしてどのように使用されるかを理解する必要があります。 次の表では、これらのデータ型について説明します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>タスクバーの検索ボックスに</th>
<th>パラメーター名</th>
<th>意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile" data-raw-source="[IWDFFile](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile)">IWDFFile</a></p></td>
<td><p>pClientFile</p></td>
<td><p>この UMDF COM インターフェイスは、プラットフォームがクライアントアプリケーションに関連付けているファイルオブジェクトを表します。 センサーメソッドの呼び出しでは、常にこの型を有効なインターフェイスポインターとして指定しますが、アプリケーションの ID として使用することを意図しています。 ポインターに含まれるアドレスは、クライアントアプリケーションを識別できる一意の番号です。 この値は、ポインター自体のアドレスとは異なることに注意してください。 ID を取得するには、アドレス演算子 (&) を使用しないでください。 ポインター自体を使用します。</p>
<p>このポインターを使用して基になるオブジェクトにアクセスする場合は、最初にポインターを使用して AddRef を呼び出し、終了したときに Release を呼び出すようにしてください。</p></td>
</tr>
<tr class="even">
<td><p><strong>LPWSTR</strong></p></td>
<td><p>pwszSensorID</p></td>
<td><p>この文字列は、特定のセンサーのドライバーによって提供される一意の ID です。 この ID は、特定のデバイスのセンサーごとに一意である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=131486" data-raw-source="[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)">IPortableDeviceValues</a></p></td>
<td><p>ppDataValues</p>
<p>ppPropertyValues</p>
<p>pPropertiesToSet</p>
<p>ppResults</p></td>
<td><p>この WPD インターフェイスは、名前と値のペアのプロパティバッグを作成する便利な方法を提供します。 <strong>Propertykey</strong>s は名前を表し、 <strong>propvariant</strong>は値を表します。 DDI は、このインターフェイスを使用して値のセットを設定および取得します。単一の値の場合はを使用します。</p>
<p>このインターフェイスは、メソッドから取得することも、新しいオブジェクトが必要な場合は、 <strong>CLSID_PortableDeviceValues</strong>で CoCreateInstance を呼び出すことによって取得することもできます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=131487" data-raw-source="[IPortableDeviceValuesCollection](https://go.microsoft.com/fwlink/p/?linkid=131487)">IPortableDeviceValuesCollection</a></p></td>
<td><p>pEventCollection</p>
<p>ppSensorObjectCollection</p></td>
<td><p>この WPD インターフェイスには、 <a href="https://go.microsoft.com/fwlink/p/?linkid=131486" data-raw-source="[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)">Iportabledevicevalues</a>オブジェクトのコレクションが含まれています。 このインターフェイスを使用する DDI メソッドを使用すると、複数のイベントや複数のセンサーに関する情報など、複数のデータセットを同時に提供できます。</p>
<p>このインターフェイスは、メソッドから取得することも、新しいオブジェクトが必要な場合は、 <strong>CLSID_PortableDeviceValuesCollection</strong>で CoCreateInstance を呼び出すことによって取得することもできます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=131484" data-raw-source="[IPortableDeviceKeyCollection](https://go.microsoft.com/fwlink/p/?linkid=131484)">IPortableDeviceKeyCollection</a></p></td>
<td><p>pDataFields</p>
<p>pProperties</p>
<p>ppSupportedDataFields</p>
<p>ppSupportedProperties</p></td>
<td><p>この WPD インターフェイスには、 <strong>Propertykey</strong>s のコレクションが含まれています。 これらのキーは、 <a href="https://go.microsoft.com/fwlink/p/?linkid=131486" data-raw-source="[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)">Iportabledevicevalues</a>で格納できるプロパティ名を表します。 DDI は、プロパティ名のセットの設定と取得の両方、または1つの名前を使用して、このコレクションオブジェクトを使用します。</p>
<p>このインターフェイスは、メソッドから取得することも、新しいオブジェクトが必要な場合は、 <strong>CLSID_PortableDeviceKeyCollection</strong>で CoCreateInstance を呼び出すことによって取得することもできます。</p></td>
</tr>
</tbody>
</table>

 

 

 




