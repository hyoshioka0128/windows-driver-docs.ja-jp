---
title: デバイス固有のメソッド (_DSM)
description: 高度な機能とテクノロジ スタックを選択する拡張機能をサポートするには、は、Windows は、デバイスのデバイスに固有のメソッド (_DSM) を定義します。
ms.assetid: E49BE897-28A5-42FE-875C-A8EB56EABF8B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78d49bb40956cca3c8312d8aec4bf6d109385b94
ms.sourcegitcommit: d334150abe0b189faf33049908af7aab1458c13d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2019
ms.locfileid: "57464065"
---
# <a name="device-specific-methods-dsm"></a>デバイス固有のメソッド (\_DSM)


高度な機能とテクノロジ スタックを選択する拡張機能をサポートする Windows デバイスに固有のメソッドを一切定義 (\_DSM) デバイス。

[ACPI 5.0 仕様](https://www.uefi.org/specifications)チップ (SoC) 統合の回線でシステムを使用するハードウェア プラットフォームをサポートするために Windows で使用されるいくつかのデバイス固有のメソッドが導入されています。 このセクションのトピックでは、引数を説明し、これらのメソッドに対して定義されている値を返します。

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
<td><p><a href="gpio-controller-device-specific-method---dsm-.md" data-raw-source="[GPIO controller Device-Specific Method (_DSM)](gpio-controller-device-specific-method---dsm-.md)">GPIO コント ローラー デバイスに固有のメソッド (_DSM)</a></p></td>
<td><p>Microsoft、さまざまなデバイス固有クラス通信は Windows では、汎用の I/O (GPIO) ドライバー スタックとプラットフォームのファームウェアをサポートするには、特定のデバイス メソッド (_DSM)、ACPI に GPIO コント ローラーの下に含めることができるを定義します名前空間。</p></td>
</tr>
<tr class="even">
<td><p><a href="battery-device-specific-method.md" data-raw-source="[Battery Device-Specific Method](battery-device-specific-method.md)">バッテリのデバイスに固有のメソッド</a></p></td>
<td><p>プラットフォームで、バッテリのパッシブの温度管理をサポートするためには、Microsoft は、プラットフォーム ファームウェア バッテリの熱のゾーンによって設定された制限を調整する温度と通信する _DSM メソッドを定義します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="device-specific-method-for-microsoft-thermal-extensions.md" data-raw-source="[Device-Specific Method for Microsoft thermal extensions](device-specific-method-for-microsoft-thermal-extensions.md)">Microsoft の熱の拡張機能のデバイス固有のメソッド</a></p></td>
<td><p>温度のゾーンと温度センサーのより柔軟なデザインをサポートするためには、Windows は、ACPI 熱ゾーン モデルの拡張機能をサポートします。 具体的には、Windows では、温度ゾーンごとに温度の最小スロットルの制限 (MTL) をサポートしも熱ゾーン間での温度センサーの共有をサポートします。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-device-specific-method---dsm-.md" data-raw-source="[USB Device-Specific Method (_DSM)](usb-device-specific-method---dsm-.md)">USB デバイスに固有のメソッド (_DSM)</a></p></td>
<td><p>USB サブシステムのデバイス固有クラスの構成をサポートするためには、Windows は、特定のデバイス メソッド (_DSM) この記事で説明されている関数を持つを定義します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hidi2c-device-specific-method---dsm-.md" data-raw-source="[HIDI2C Device-Specific Method (_DSM)](hidi2c-device-specific-method---dsm-.md)">HIDI2C デバイス固有のメソッド (_DSM)</a></p></td>
<td><p>_DSM メソッドが、9.14.1"_DSM (デバイスの特定のメソッド)"でのセクションで定義されている、 <a href="https://www.uefi.org/specifications" data-raw-source="[ACPI 5.0 specification](https://www.uefi.org/specifications)">ACPI 5.0 仕様</a>します。 このメソッドは、個々 のデバイス固有のデータとデバイス ドライバーなど他のデバイスに固有のメソッドで競合することがなく呼び出すことができるコントロール関数を提供します。</p></td>
</tr>
<tr class="even">
<td><p><a href="windows-button-array-device-specific-method---dsm-.md" data-raw-source="[Windows button array Device-Specific Method (_DSM)](windows-button-array-device-specific-method---dsm-.md)">ボタン配列の Windows デバイスに固有のメソッド (_DSM)</a></p></td>
<td><p>Windows のボタン ユーザー インターフェイス (UI) の進化をサポートするためには、Windows は、この記事では、特定のデバイス メソッド (_DSM) 説明されている関数を使用した Windows ボタン配列のデバイスを定義します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="other-dsms-defined-for-windows"></a>その他の\_Windows に対して定義されている DSMs


Microsoft Windows でドライバー スタックとプラットフォームのファームウェアのデバイス固有クラスの通信をサポートするにはデバイス固有のメソッドを定義します (\_DSM) ドライバーで使用します。

|                                                                                                                                                                                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| トピック                                                                                                                                                                                       | 説明                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| [\_バイトのアドレス指定可能なエネルギーの DSM インターフェイス関数クラス (関数インターフェイス 1) のバックアップ](https://msdn.microsoft.com/library/windows/hardware/mt604741) | \_DSM クラスのインターフェイスをバイト アドレス指定可能なエネルギー バックアップ関数 (関数のインターフェイスの 1) が BIOS の複雑さを軽減するために、JEDEC バイト アドレス指定可能なエネルギー バックアップ インターフェイスの標準にマップするように設計します。 OS ソフトウェアが同じメカニズムを通じてさまざまな実装が操作できるよう、デバイスの機能と機能、レポートの共通の基盤を提供します。 さらに、I2C レジスタへのアクセスによりベンダー固有の機能をサポートできます。 |
| [\_SATA 用 DSM (デバイスの特定のメソッド)](https://msdn.microsoft.com/library/windows/hardware/dn613874)                                                                               | このメソッドは、全体として、SATA コント ローラー ホスト コント ローラーから個別の各ポートの管理を使用します。                                                                                                                                                                                                                                                                                                                                                                           |

 

 

 




