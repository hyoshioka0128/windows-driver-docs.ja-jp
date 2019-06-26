---
title: V4 ドライバー接続アーキテクチャ
description: V4 印刷ドライバー モデルは、単に Bidi と呼ばれる、双方向のスキーマを使用して双方向通信の豊富なサポートを提供します。
ms.assetid: ED7C4A2D-449E-4271-9348-86EAC03B6E64
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14323756135ef542c0f306f8ce7f4bd83674a69a
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393156"
---
# <a name="v4-driver-connectivity-architecture"></a>V4 ドライバー接続アーキテクチャ


V4 印刷ドライバー モデルの接続コンポーネントの主な目標 Bidi とだけ呼ば、双方向のスキーマを使用して双方向通信の豊富なサポートを提供することです。

V4 印刷ドライバー モデルは、v3 プリンター ドライバー モデルと比較して簡素化された接続スタックをサポートします。

**ポート モニタおよび言語モニタ**

V4 ドライバー モデル、または印刷クラス ドライバーで、サード パーティのポート モニターおよび言語モニターはサポートされません。 V4 印刷ドライバー モデルは、SNMP 双方向の拡張機能のファイル形式と同様に、WSDMon 双方向の拡張機能のファイル形式を使用し続けます。 新しい v4 の USBMon 双方向の拡張 XML と JavaScript ファイルを使用して USB 経由での Bidi をサポートする機能は、します。

**双方向のスキーマ**

次の表は、ファイルと情報をサポートするために必要な機能と、印刷デバイス用に選択した通信プロトコルの種類に応じて、提供する必要があります。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>通信の種類</th>
<th>拡張機能ファイルはありません。</th>
<th>双方向の拡張ファイル</th>
<th>強化された自動構成</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>USB</td>
<td><p>次のプロパティは、ポート モニタによって Bidi スキーマに表示されます。</p>
<p>\Printer.DeviceInfo:Manufacturer</p>
<p>\Printer.DeviceInfo:ModelName</p>
<p>\Printer.DeviceInfo:IEEE1284DeviceId</p>
<p>\Printer.DeviceInfo:HardwareId</p>
<p>\Printer.DeviceInfo:CompatibleId</p>
<p>\Printer.DeviceInfo:SerialNumber</p></td>
<td><p>次のファイルを提供する必要があります。</p>
- 拡張ファイルの XML Bidi - JavaScript Bidi 拡張ファイル</td>
<td>印刷デバイスがこの機能をサポートする必要があり、双方向の拡張機能のファイルを提供する必要があります。</td>
</tr>
<tr class="even">
<td>WSD</td>
<td>標準のプロパティから、 <a href="https://docs.microsoft.com/windows-hardware/design/whitepapers/implementing-web-services-on-devices-for-printing" data-raw-source="[WS-Print Specification](https://docs.microsoft.com/windows-hardware/design/whitepapers/implementing-web-services-on-devices-for-printing)">Ws-print 仕様</a>または Ws-print v1.1 の仕様は、ポート モニターによって Bidi スキーマに設定されます。</td>
<td><p>次のファイルを提供する必要があります。</p>
双方向の XML 拡張ファイル</td>
<td>印刷デバイスには、Ws-print v1.1 プロトコルをサポートする必要があります。</td>
</tr>
<tr class="odd">
<td>TCP/IP (SNMP)</td>
<td><p>ポート モニター MIB が実装されている場合、次のプロパティによって設定された Bidi スキーマに、ポート モニター。</p>
<p>\Printer.DeviceInfo:Manufacturer</p>
<p>\Printer.DeviceInfo:ModelName</p>
<p>\Printer.DeviceInfo:IEEE1284DeviceId</p>
<p>\Printer.DeviceInfo:HardwareId</p>
<p>\Printer.DeviceInfo:CompatibleId</p>
<p>\Printer.DeviceInfo.NetworkingInfo:PresentationUrl</p>
<p>\Printer.Configuration.Memory:Size</p>
<p>\Printer.Configuration.HardDisk:Installed</p>
<p>\Printer.Configuration.DuplexUnit:Installed</p></td>
<td><p>次のファイルを提供する必要があります。</p>
双方向の XML 拡張ファイル</td>
<td>印刷デバイスがこの機能をサポートする必要があり、双方向の拡張機能のファイルを提供する必要があります。</td>
</tr>
</tbody>
</table>

 

詳細については、次を参照してください。[双方向通信スキーマ](https://docs.microsoft.com/windows-hardware/drivers/print/bidirectional-communication-schema)と[WSDMon ポート モニター](wsdmon-port-monitor.md)します。 Bidi スキーマを拡張するポート モニターをカスタマイズする方法について説明を参照してください[プリンター ポート モニターをカスタマイズする](https://docs.microsoft.com/windows-hardware/drivers/print/customizing-the-printer-port-monitors)します。

## <a name="related-topics"></a>関連トピック
[双方向通信のスキーマ](https://docs.microsoft.com/windows-hardware/drivers/print/bidirectional-communication-schema)  
[プリンタ ポート モニターをカスタマイズします。](https://docs.microsoft.com/windows-hardware/drivers/print/customizing-the-printer-port-monitors)  
[V4 プリンター ドライバーの接続](v4-printer-driver-connectivity.md)  
[WSDMon ポート モニター](wsdmon-port-monitor.md)  



