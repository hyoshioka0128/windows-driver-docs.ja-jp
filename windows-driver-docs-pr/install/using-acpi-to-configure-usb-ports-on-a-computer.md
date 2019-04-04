---
title: ACPI を使用したコンピューターへの USB ポートの構成
description: ACPI を使用したコンピューターへの USB ポートの構成
ms.assetid: 999f9fef-512c-415a-abc6-d64560c5c2f8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1eaaee115eb76b3652dd335ecff7d56145bdbeb
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349303"
---
# <a name="using-acpi-to-configure-usb-ports-on-a-computer"></a>ACPI を使用したコンピューターへの USB ポートの構成


システムでは、USB ポートの構成を正確に反映するように、ACPI BIOS の変更が必要とする場合は、ポート、ポートを構成するときにデバイスを接続するユーザーの機能を検討してください。

ACPI を使用して、USB ポートの構成を指定する場合は、USB ポート機能を定義する必要があります (**_UPC**) と物理的な場所の説明 (**_PLD**) オブジェクト。 具体的には、ACPI 6.0 仕様にのみの使用が禁止されていませんが、 **_UPC**オブジェクト、正確なことを示します、ポートにデバイスを接続するユーザーの権限の詳細の両方のオブジェクトを使用します。 のみを使用して、 **_UPC**オブジェクトが正しく、または期待どおりにグループ化するデバイスのコンテナーを設定します。

ポートに接続されているデバイスがハブからリムーバブル場合、 **DeviceRemovable**ビットが設定されます。 次の表は、特定のポートの ACPI オブジェクトの値は、USB ハブ既述子の値に与える影響**DeviceRemovable**ビット Windows がデバイスのレポートです。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">USB ポートの状態</th>
<th align="left">例</th>
<th align="left">_UPC します。PortIsConnectable バイト</th>
<th align="left">_PLD します。UserVisible ビット (64 ビット)</th>
<th align="left">結果として得られる DeviceRemovable ビット値</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ポートが表示され、ユーザーは自由に接続し、デバイスを取り外します。</p></td>
<td align="left"><p>ポートは、ユーザーに表示されているコンピューター上のパネルの表面に公開されます。</p></td>
<td align="left"><p>(0 xff) の設定します。</p></td>
<td align="left"><p>(1) の設定します。</p></td>
<td align="left"><p>Set</p></td>
</tr>
<tr class="even">
<td align="left"><p>ポートが非表示か内部とユーザーの接続しデバイスを切断できません自由に。</p></td>
<td align="left"><p>ポートは、ラップトップの web カメラや内部の USB ハブなど、統合されたデバイスに直接組み込みです。</p></td>
<td align="left"><p>(0 xff) の設定します。</p></td>
<td align="left"><p>オフ</p></td>
<td align="left"><p>オフ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ポートは、USB ホスト コント ローラーによって物理的に実装されますは使用されません。</p></td>
<td align="left"><p>ポートには、ターミナル ポート プラグまたは統合されたデバイスに接続されていない余分なポートです。</p></td>
<td align="left"><p>消去 (0x00)</p></td>
<td align="left"><p>[クリア]</p></td>
<td align="left"><p>オフ</p></td>
</tr>
</tbody>
</table>

 

**注**  が接続可能ですが、ユーザーに表示されるポートを定義する構成が無効です。

 

次の例では、ACPI ソース言語 (ASL) の使用方法を示す正しい形式で、 **_UPC**と **_PLD** USB ポートを記述するオブジェクト。

-   内部にあるポートを指定するユーザーではなく表示される) と統合された、デバイスに接続することができます、 **_UPC します。PortIsConnectable** 0 xff までバイトを設定する必要があります、 **_PLD します。UserVisible**ビットを 0 に設定する必要があります。

    次の例では、デバイスは、コンピューターのデバイスのコンテナーをグループ化されます。

    ```cpp
    Name(_UPC, Package(){
        0xFF,         // Port is connectable
        0xFF,         // Connector type (N/A for non-visible ports)
        0x00000000,   // Reserved 0, must be zero
        0x00000000})  // Reserved 1, must be zero

    Name(_PLD, Buffer(0x10){
        0x81, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
        0x30, 0x1C, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00})
    ```

-   外部にあるポートを指定する (ユーザー表示可能である) 外部のデバイスに接続できると、 **_UPC します。PortIsConnectable** 0 xff までバイトを設定する必要があります、 **_PLD します。UserVisible**ビットを 1 に設定する必要があります。 _**UPC**.**PortConnectorType**バイトは、ACPI 3.0 仕様で指定されている 9.13 として適切な USB コネクタの種類に設定する必要があります。

    次の例では、デバイスはデバイスの新しいコンテナーが割り当てられているし、は別の物理デバイスとして表示されます。

    ```cpp
    Name(_UPC, Package(){
        0xFF,         // Port is connectable
        0x00,         // Connector type, Type 'A' in this case
        0x00000000,   // Reserved 0, must be zero
        0x00000000})  // Reserved 1, must be zero

    Name(_PLD, Buffer(0x10){
        0x81, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00,
        0x31, 0x1C, 0x00, 0x00, 0x00, 0x00, 0x00, 0x00})
    ```
    
USB 型-C# のコネクタを記述する必要が正しく ACPI に渡すために、 [USB 型 C ACPI 検証](https://msdn.microsoft.com/library/windows/hardware/mt770585(v=vs.85).aspx)ハードウェア ラボ キット テストします。

例 _UPC USB 型-C# のコネクタの場合。
```cpp
      Name(_UPC, Package(4){
        0x01,                       // Port is connectable
        0x09,                       // Connector type: Type C connector - USB2 and SS with Switch
        0x00000000,                 // Reserved0 – must be zero
        0x00000000})                // Reserved1 – must be zero
```

ACPI 6.0 インターフェイスの詳細については、[Advanced Configuration and Power インターフェイス仕様 Revision 6.0](https://go.microsoft.com/fwlink/?LinkId=827852)を参照してください。

 

 





