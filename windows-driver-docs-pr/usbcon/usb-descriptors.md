---
Description: USB デバイスは、USB 記述子と呼ばれるデータ構造自体に関する情報を提供します。 このセクションでは、クライアント ドライバーは、USB デバイスから入手できるさまざまな記述子について情報を提供します。
title: USB 記述子
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6623b236ccdd5ac287d79272c85542f4d749e660
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331632"
---
# <a name="usb-descriptors"></a>USB 記述子


USB デバイスと呼ばれるデータ構造自体に関する情報を提供する*の USB ディスクリプター*します。 このセクションでは、クライアント ドライバーは、USB デバイスから入手できるさまざまな記述子について情報を提供します。




ホストは、さまざまな標準のコントロール要求を送信することによって接続されたデバイスから記述子を取得 (GET\_記述子要求) 既定のエンドポイントにします。 これらの要求を取得する記述子の種類を指定します。 このような要求に応答して、デバイスは、デバイス、その構成、インターフェイスと、関連するエンドポイントについての情報を含む記述子を送信します。 *デバイス記述子*全体のデバイスに関する情報が含まれます。 *構成記述子*各デバイスの構成に関する情報が含まれます。 *記述子文字列*Unicode テキスト文字列が含まれます。

すべての USB デバイスは、クラスについては、デバイスのベンダーと製品の id、および構成の数を示すデバイス記述子を公開します。 各構成は、そのインターフェイスと電源の特徴の数を示す構成記述子を公開します。 各インターフェイスでは、各クラスとエンドポイントの数に関する情報を含む別の設定、インターフェイスの記述子を公開します。 各インターフェイス内の各エンドポイントは、エンドポイントの種類とパケットの最大サイズを示すエンドポイント記述子を公開します。

たとえばで説明した OSR FX2 ボード デバイス レイアウト[USB デバイス レイアウト](usb-device-layout.md)します。 デバイス レベルでは、デバイスはデバイス記述子と既定のエンドポイントのエンドポイント記述子を公開します。 構成レベルでは、デバイスは、0 の構成の構成記述子を公開します。 インターフェイス レベルでの代替設定 0 インターフェイスの 1 つの記述子を公開します。 エンドポイント レベルでは、次の 3 つのエンドポイント記述子が公開されます。

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
<td><p>デバイス記述子には、全体として、USB デバイスに関する情報が含まれています。 このトピックで説明します、 <a href="https://msdn.microsoft.com/library/windows/hardware/ff539280" data-raw-source="[&lt;strong&gt;USB_DEVICE_DESCRIPTOR&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539280)"> <strong>USB_DEVICE_DESCRIPTOR</strong> </a>構造体であり、クライアント ドライバーがデバイス記述子を取得する get 記述子の要求を送信する方法に関する情報が含まれています。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-configuration-descriptors.md" data-raw-source="[USB configuration descriptors](usb-configuration-descriptors.md)">USB 構成記述子</a></p></td>
<td><p>USB デバイスは、一連の USB 構成と呼ばれるインターフェイスの形式でその機能を公開します。 各インターフェイスは 1 つまたは複数の代替設定と各代替の設定は、一連のエンドポイントの構成されます。 このトピックでは、USB 構成に関連付けられたさまざまな記述子について説明します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="usb-string-descriptors.md" data-raw-source="[USB String Descriptors](usb-string-descriptors.md)">USB 文字列記述子</a></p></td>
<td><p>デバイス、構成、およびインターフェイスの記述子には、文字列記述子への参照を含めることができます。 このトピックでは、デバイスから特定の文字列記述子を取得する方法について説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-interface-association-descriptor.md" data-raw-source="[USB Interface Association Descriptor](usb-interface-association-descriptor.md)">USB インターフェイスの関連付けの記述子</a></p></td>
<td><p>USB インターフェイスの関連付け記述子 (IAD) では、関数に属しているグループのインターフェイスにデバイスを許可します。 このトピックでは、クライアント ドライバーを調べる方法、デバイスに、IAD 関数が含まれているかどうかについて説明します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>関連トピック
[USB デバイスのレイアウト](usb-device-layout.md)  
[USB ドライバー開発ガイド](usb-driver-development-guide.md)  



