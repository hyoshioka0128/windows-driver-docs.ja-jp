---
Description: USB デバイスは、それ自体に関する情報を USB 記述子と呼ばれるデータ構造に提供します。 このセクションでは、クライアントドライバーが USB デバイスから取得できるさまざまな記述子について説明します。
title: USB 記述子
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1caf2a5da4aacf9ed5f067fd0a8b1aa4cbc6a2e1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844830"
---
# <a name="usb-descriptors"></a>USB 記述子


USB デバイスは、それ自体に関する情報を*usb 記述子*と呼ばれるデータ構造に提供します。 このセクションでは、クライアントドライバーが USB デバイスから取得できるさまざまな記述子について説明します。




ホストは、さまざまな標準コントロール要求 (GET\_DESCRIPTOR 要求) を既定のエンドポイントに送信することによって、接続されているデバイスから記述子を取得します。 これらの要求は、取得する記述子の種類を指定します。 デバイスは、このような要求に応答して、デバイス、その構成、インターフェイス、および関連するエンドポイントに関する情報を含む記述子を送信します。 デバイス*記述子*には、デバイス全体に関する情報が含まれています。 *構成記述子*には、各デバイスの構成に関する情報が含まれています。 *文字列記述子*には Unicode テキスト文字列が含まれます。

すべての USB デバイスは、デバイスのクラス情報、ベンダーと製品の識別子、および構成の数を示すデバイス記述子を公開します。 各構成は、インターフェイスの数と電源特性を示す構成記述子を公開します。 各インターフェイスは、クラスとエンドポイントの数に関する情報を含むそれぞれの代替設定のインターフェイス記述子を公開します。 各インターフェイス内の各エンドポイントは、エンドポイントの種類と最大パケットサイズを示すエンドポイント記述子を公開します。

たとえば、「 [USB デバイスレイアウト](usb-device-layout.md)」で説明されている OSR FX2 board デバイスレイアウトについて考えてみます。 デバイスレベルでは、デバイスは既定のエンドポイントのデバイス記述子とエンドポイント記述子を公開します。 構成レベルでは、デバイスは構成0の構成記述子を公開します。 インターフェイスレベルでは、別の設定0に対して1つのインターフェイス記述子を公開します。 エンドポイントレベルでは、3つのエンドポイント記述子が公開されます。

## <a name="in-this-section"></a>このセクションの内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>トピック</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="usb-device-descriptors.md" data-raw-source="[USB device descriptors](usb-device-descriptors.md)">USB デバイス記述子</a></p></td>
<td><p>デバイス記述子には、USB デバイス全体に関する情報が含まれています。 このトピックでは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_device_descriptor" data-raw-source="[&lt;strong&gt;USB_DEVICE_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_device_descriptor)"><strong>USB_DEVICE_DESCRIPTOR</strong></a>構造体について説明します。また、クライアントドライバーが get 記述子要求を送信してデバイス記述子を取得する方法についても説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-configuration-descriptors.md" data-raw-source="[USB configuration descriptors](usb-configuration-descriptors.md)">USB 構成記述子</a></p></td>
<td><p>USB デバイスは、USB 構成と呼ばれる一連のインターフェイスの形式で機能を公開します。 各インターフェイスは、1つまたは複数の代替設定で構成され、各代替設定は一連のエンドポイントで構成されます。 このトピックでは、USB 構成に関連付けられているさまざまな記述子について説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-string-descriptors.md" data-raw-source="[USB String Descriptors](usb-string-descriptors.md)">USB 文字列記述子</a></p></td>
<td><p>デバイス、構成、およびインターフェイス記述子には、文字列記述子への参照を含めることができます。 このトピックでは、デバイスから特定の文字列記述子を取得する方法について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-interface-association-descriptor.md" data-raw-source="[USB Interface Association Descriptor](usb-interface-association-descriptor.md)">USB インターフェイスの関連付け記述子</a></p></td>
<td><p>USB インターフェイスの関連付け記述子 (IAD) を使用すると、デバイスは、関数に属しているインターフェイスをグループ化できます。 このトピックでは、クライアントドライバーが関数の IAD を含むかどうかを判断する方法について説明します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[USB デバイスレイアウト](usb-device-layout.md)  
[USB ドライバー開発ガイド](usb-driver-development-guide.md)  



