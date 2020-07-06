---
title: デバイス固有のメソッド (_DSM)
description: テクノロジスタックを選択するための機能と拡張機能の向上をサポートするために、Windows はデバイスのデバイス固有のメソッド (_DSM) を定義します。
ms.assetid: E49BE897-28A5-42FE-875C-A8EB56EABF8B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e9c304e3a406e33ded9a1fc90bf114405bb6579
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968049"
---
# <a name="device-specific-methods-_dsm"></a>デバイス固有の方法 ( \_ DSM)


テクノロジスタックを選択するための機能と拡張機能の向上をサポートするために、Windows ではデバイスのデバイス固有のメソッド (DSM) を定義して \_ います。

[ACPI 5.0 仕様](https://uefi.org/specifications)では、チップ (SoC) の統合回線でシステムを使用するハードウェアプラットフォームをサポートするために Windows によって使用されるデバイス固有のメソッドがいくつか導入されています。 このセクションのトピックでは、これらのメソッドに対して定義されている引数と戻り値について説明します。

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
<td><p><a href="gpio-controller-device-specific-method---dsm-.md" data-raw-source="[GPIO controller Device-Specific Method (_DSM)](gpio-controller-device-specific-method---dsm-.md)">GPIO コント ローラーのデバイス固有のメソッド (_DSM)</a></p></td>
<td><p>Windows の汎用 i/o (GPIO) ドライバースタックとプラットフォームファームウェアの間で、デバイスクラス固有のさまざまな通信をサポートするために、Microsoft では、デバイス固有のメソッド (_DSM) を定義しています。これは、ACPI 名前空間の GPIO コントローラーの下に含めることができます。</p></td>
</tr>
<tr class="even">
<td><p><a href="battery-device-specific-method.md" data-raw-source="[Battery Device-Specific Method](battery-device-specific-method.md)">バッテリーのデバイス固有のメソッド</a></p></td>
<td><p>プラットフォームによるバッテリのパッシブな温度管理をサポートするために、Microsoft は、バッテリのサーマルゾーンによって設定された温度調整の制限をプラットフォームファームウェアと通信する _DSM 方法を定義します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="device-specific-method-for-microsoft-thermal-extensions.md" data-raw-source="[Device-Specific Method for Microsoft thermal extensions](device-specific-method-for-microsoft-thermal-extensions.md)">Microsoft 熱拡張機能に対するデバイス固有のメソッド</a></p></td>
<td><p>サーマルゾーンと温度センサーのより柔軟な設計をサポートするために、Windows は ACPI サーマルゾーンモデルの拡張機能をサポートしています。 具体的には、Windows では、各サーマルゾーンに対して温度センサーの最小スロットル制限 (.MTL) がサポートされています。また、温度センサーをサーマルゾーン間で共有することもできます。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-device-specific-method---dsm-.md" data-raw-source="[USB Device-Specific Method (_DSM)](usb-device-specific-method---dsm-.md)">USB のデバイス固有のメソッド (_DSM)</a></p></td>
<td><p>USB サブシステムのデバイスクラス固有の構成をサポートするために、Windows では、この記事で説明されている機能を備えたデバイス固有のメソッド (_DSM) を定義しています。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hidi2c-device-specific-method---dsm-.md" data-raw-source="[HIDI2C Device-Specific Method (_DSM)](hidi2c-device-specific-method---dsm-.md)">HIDI2C のデバイス固有のメソッド (_DSM)</a></p></td>
<td><p>_DSM メソッドは、 <a href="https://uefi.org/specifications" data-raw-source="[ACPI 5.0 specification](https://uefi.org/specifications)">ACPI 5.0 仕様</a>のセクション 9.14.1 "_DSM (デバイス固有のメソッド)" で定義されています。 このメソッドは、デバイス固有のその他のメソッドと競合することなくデバイスドライバーから呼び出すことができる、デバイス固有の個々のデータおよび制御関数に対してを提供します。</p></td>
</tr>
<tr class="even">
<td><p><a href="windows-button-array-device-specific-method---dsm-.md" data-raw-source="[Windows button array Device-Specific Method (_DSM)](windows-button-array-device-specific-method---dsm-.md)">Windows ボタン配列のデバイス固有のメソッド (_DSM)</a></p></td>
<td><p>Windows ボタンのユーザーインターフェイス (UI) の進化をサポートするために、windows は、この記事で説明されている機能を使用して、Windows ボタン配列デバイス用のデバイス固有のメソッド (_DSM) を定義します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="other-_dsms-defined-for-windows"></a>\_Windows 用に定義されたその他の dsm


Windows のドライバースタックとプラットフォームファームウェア間のデバイスクラス固有の通信をサポートするために、Microsoft では、ドライバーで使用されるデバイス固有のメソッド (DSM) を定義して \_ います。

**トピック**: 説明

**[ \_ バイトアドレッシング可能なエネルギー対応関数クラスの DSM インターフェイス (関数インターフェイス 1)](https://docs.microsoft.com/windows-hardware/drivers/storage/-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-)**: \_バイトアドレッシング可能なエネルギーサポート関数クラスの DSM インターフェイス (関数インターフェイス 1) は、BIOS の複雑さを最小限に抑えるために、JEDEC バイトのアドレス指定可能なエネルギーサポートインターフェイス標準にマップするように設計されています。 これは、デバイスの機能をレポートするための一般的な機能を提供します。これは、OS ソフトウェアが同じメカニズムを使用してさまざまな実装と対話できるようにするための機能 & ます。 さらに、I2C レジスタにアクセスすることによって、ベンダー固有の機能をサポートできます。

**[ \_ Sata 用 DSM (デバイス固有の方法)](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn613874(v=vs.85))**: この方法では、sata コントローラーの各ポートを、ホストコントローラー全体とは別に管理できます。


 

 

 




