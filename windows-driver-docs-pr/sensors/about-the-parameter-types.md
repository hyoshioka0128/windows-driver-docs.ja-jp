---
title: センサー パラメーターの型について
description: パラメーターの型について
ms.assetid: 392ea7b9-df6f-4d47-9367-a167c0656dd4
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0983a97bc6a230501a9593a3d2baf25e336d6f5a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360924"
---
# <a name="about-sensor-parameter-types"></a>センサー パラメーターの型について


メソッドのパラメーターとして、センサー クラスの拡張機能が一部のデータ型を使用する方法を理解する必要があります。 次の表では、これらのデータ型について説明します。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>種類</th>
<th>パラメーター名</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdffile" data-raw-source="[IWDFFile](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdffile)">IWDFFile</a></p></td>
<td><p>pClientFile</p></td>
<td><p>この UMDF COM インターフェイスでは、プラットフォームがクライアント アプリケーションに関連付けるファイル オブジェクトを表します。 センサー メソッドの呼び出しが常に有効なインターフェイス ポインターとは、この型を指定していますが、アプリケーションの ID として使用するものでは。 ポインターを含むアドレスは、クライアント アプリケーションを識別できる一意の番号です。 この値がポインター自体のアドレスと異なることに注意します。 Address-of 演算子を使用しないでください (&amp;) ID を取得するには ポインター自体を使用します。</p>
<p>このポインターを使用して、基になるオブジェクトにアクセスする場合は、最初に、ポインターを通じて AddRef を呼び出すが完了したら、Release を呼び出すに注意してください。</p></td>
</tr>
<tr class="even">
<td><p><strong>LPWSTR</strong></p></td>
<td><p>pwszSensorID</p></td>
<td><p>この文字列は、特定のセンサー ドライバーによって提供される一意の ID です。 この ID は、特定のデバイス上の各センサーに対して一意である必要があります。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=131486" data-raw-source="[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)">IPortableDeviceValues</a></p></td>
<td><p>ppDataValues</p>
<p>ppPropertyValues</p>
<p>pPropertiesToSet</p>
<p>ppResults</p></td>
<td><p>この WPD インターフェイスでは、名前/値ペアのプロパティ バッグを作成する便利な手段を提供します。 <strong>PROPERTYKEY</strong>s は、名前を表すと<strong>PROPVARIANT</strong>s が値を表します。 DDI では、このインターフェイスを使用して、両方を設定し、値、または 1 つの値のセットを取得します。</p>
<p>このインターフェイスを取得するには、メソッドから、CoCreateInstance を呼び出して、新しいオブジェクトが必要な場合または<strong>CLSID_PortableDeviceValues</strong>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=131487" data-raw-source="[IPortableDeviceValuesCollection](https://go.microsoft.com/fwlink/p/?linkid=131487)">IPortableDeviceValuesCollection</a></p></td>
<td><p>pEventCollection</p>
<p>ppSensorObjectCollection</p></td>
<td><p>この WPD インターフェイスのコレクションを格納する<a href="https://go.microsoft.com/fwlink/p/?linkid=131486" data-raw-source="[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)">IPortableDeviceValues</a>オブジェクト。 このインターフェイスを使用する DDI メソッドを使用して、複数のイベントや複数のセンサーに関する情報など、同時に複数のデータ セットを提供できます。</p>
<p>このインターフェイスを取得するには、メソッドから、CoCreateInstance を呼び出して、新しいオブジェクトが必要な場合または<strong>CLSID_PortableDeviceValuesCollection</strong>します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=131484" data-raw-source="[IPortableDeviceKeyCollection](https://go.microsoft.com/fwlink/p/?linkid=131484)">IPortableDeviceKeyCollection</a></p></td>
<td><p>pDataFields</p>
<p>pProperties</p>
<p>ppSupportedDataFields</p>
<p>ppSupportedProperties</p></td>
<td><p>この WPD インターフェイスのコレクションを格納する<strong>PROPERTYKEY</strong>秒。 これらのキーを格納できるプロパティの名前を表す<a href="https://go.microsoft.com/fwlink/p/?linkid=131486" data-raw-source="[IPortableDeviceValues](https://go.microsoft.com/fwlink/p/?linkid=131486)">IPortableDeviceValues</a>します。 DDI は、両方の設定およびプロパティ名のセットまたは単一の名前を取得するためにこのコレクション オブジェクトを使用します。</p>
<p>このインターフェイスを取得するには、メソッドから、CoCreateInstance を呼び出して、新しいオブジェクトが必要な場合または<strong>CLSID_PortableDeviceKeyCollection</strong>します。</p></td>
</tr>
</tbody>
</table>

 

 

 




