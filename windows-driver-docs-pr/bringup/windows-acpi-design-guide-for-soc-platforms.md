---
title: SoC のプラットフォーム用の Windows ACPI 設計ガイド
description: ACPI 5.0 では、コネクテッド スタンバイ電源モデルを実装する SoC ICs に基づく低電力、モバイル デバイスをサポートする新しい機能を定義します。
ms.assetid: 661BFB7E-D190-450D-A466-7D6AD0EAAAB0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6479aa3ec938df80a873bac6f9dbad01f2f475a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559148"
---
# <a name="windows-acpi-design-guide-for-soc-platforms"></a>SoC のプラットフォーム用の Windows ACPI 設計ガイド


Advanced Configuration and Power Interface Specification、リビジョン 5.0 ([ACPI 5.0 仕様](https://www.uefi.org/specifications))、チップ (SoC) 統合の回線でシステムに基づく低電力、モバイル デバイスをサポートする機能の新しいセットを定義します。およびスタンバイ電源が接続されているモデルを実装します。 Windows 8 および Windows 8.1 以降、Windows は、SoC ベースのプラットフォームの ACPI 5.0 の新機能をサポートします。

このセクションには、ACPI 5.0 仕様で新しい機能をサポートする Windows Pc およびデバイスを実装するためのガイドラインが含まれています。 ファームウェアの開発者およびシステム設計者は、そのプラットフォームで Windows を正しく実行するかどうかを確認する次のガイドラインを使用できます。 Windows のすべてのファームウェア要件の一覧は、のドキュメントを参照してください、 [Windows 認定プログラム](https://go.microsoft.com/fwlink/p/?linkid=227314)します。

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
<td><p><a href="overview-of-windows-support-for-acpi-5-0.md" data-raw-source="[Overview of Windows support for ACPI 5.0](overview-of-windows-support-for-acpi-5-0.md)">ACPI 5.0 に対する Windows サポートの概要</a></p></td>
<td><p><a href="https://www.uefi.org/specifications" data-raw-source="[ACPI 5.0 specification](https://www.uefi.org/specifications)">ACPI 5.0 仕様</a>以降を実行する Windows 8、SoC ベースのモバイル プラットフォームのサポートを有効には、Windows の以前のバージョンで導入された多くの便利な機能をサポートするために続行されます。 この設計ガイドでは、ACPI 5.0 の SoC ベースのプラットフォームに個別に適用する部分を実装者に指示し、これらのプラットフォームで Windows を実行する ACPI の SoC 固有の機能を実装するためのベスト プラクティスについて説明します。</p></td>
</tr>
<tr class="even">
<td><p><a href="acpi-system-description-tables.md" data-raw-source="[ACPI system description tables](acpi-system-description-tables.md)">説明の ACPI システム テーブル</a></p></td>
<td><p>SoC ベースのプラットフォームまたは BIOS ベースである Windows Server システムでは、Advanced Configuration and Power Interface (ACPI) ハードウェアの仕様の実装は必要はありませんが、ACPI ソフトウェアの仕様の多くは (または、) 必要です。 ACPI は、ジェネリック、拡張可能なテーブルを渡すメカニズム、およびオペレーティング システム プラットフォームを記述するための特定のテーブルを定義します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="device-management-namespace-objects.md" data-raw-source="[Device management namespace objects](device-management-namespace-objects.md)">デバイス管理の名前空間のオブジェクト</a></p></td>
<td><p><a href="https://www.uefi.org/specifications" data-raw-source="[ACPI 5.0 specification](https://www.uefi.org/specifications)">ACPI 5.0 仕様</a>いくつかの種類のデバイスを管理するために使用する名前空間オブジェクトを定義します。 たとえば、デバイスの id オブジェクトには、子デバイスのハードウェアの列挙をサポートしていない、I2C などのバスに接続するデバイスの id 情報が含まれます。 その他の種類の名前空間のオブジェクトでは、システム リソースを指定、デバイス依存関係を記述、およびデバイスを無効にすることができますを示すことができます。</p></td>
</tr>
<tr class="even">
<td><p><a href="general-purpose-i-o--gpio-.md" data-raw-source="[General-purpose I/O (GPIO)](general-purpose-i-o--gpio-.md)">汎用入出力 (GPIO)</a></p></td>
<td><p>SoC integrated 回線ことを汎用入出力 (GPIO) ピンの広範に使用します。 SoC ベースのプラットフォームでは、Windows は、GPIO ハードウェアには、一般的な抽象化を定義し、この抽象化には、Advanced Configuration and Power Interface (ACPI) 名前空間からのサポートが必要です。</p></td>
</tr>
<tr class="odd">
<td><p><a href="simple-peripheral-bus--spb-.md" data-raw-source="[Simple peripheral bus (SPB)](simple-peripheral-bus--spb-.md)">SPB (Simple Peripheral Bus)</a></p></td>
<td><p>SoC integrated 回線は、単純な低-pin-カウントの広範に使用を行い、低電力シリアルがプラットフォームの周辺機器に接続するために相互接続します。 例には、I²C、SPI Uart などがあります。 SoC ベースのプラットフォームでは、Windows が単純な周辺機器 sp バス (B) のハードウェアには、一般的な抽象化に示し、この抽象化には、Advanced Configuration and Power Interface (ACPI) 名前空間からの新しいサポートが必要です。</p></td>
</tr>
<tr class="even">
<td><p><a href="device-power-management.md" data-raw-source="[Device power management](device-power-management.md)">デバイスの電源管理</a></p></td>
<td><p><a href="https://www.uefi.org/specifications" data-raw-source="[ACPI 5.0 specification](https://www.uefi.org/specifications)">ACPI 5.0 仕様</a>デバイスのデバイスの電源の情報を指定する名前空間のオブジェクトのセットを定義します。 たとえば、オブジェクトの 1 つのセットは、各サポートされているデバイスの電源状態のデバイスで必要な電源リソースを指定できます。 別のオブジェクト型では、ハードウェアのイベントに応答低電力状態から復帰するデバイスの機能を記述できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="acpi-defined-devices.md" data-raw-source="[ACPI-defined devices](acpi-defined-devices.md)">デバイスを ACPI 定義</a></p></td>
<td><p><a href="https://www.uefi.org/specifications" data-raw-source="[ACPI 5.0 specification](https://www.uefi.org/specifications)">ACPI 5.0 仕様</a>数を表し、一般的なプラットフォーム機能を制御するデバイスの種類を定義します。 たとえば、ACPI は、電源ボタンやスリープ ボタンの場合は、システムの評価指標を定義します。 SoC ベースのプラットフォームでは、Windows は、この記事で説明されている ACPI 定義されているデバイスをサポートする組み込みのドライバーを提供します。</p></td>
</tr>
<tr class="even">
<td><p><a href="other-acpi-namespace-objects.md" data-raw-source="[Other ACPI namespace objects](other-acpi-namespace-objects.md)">その他の ACPI 名前空間のオブジェクト</a></p></td>
<td><p>デバイスの特定のクラスがいくつか、それらのデバイスで、名前空間の下に表示する追加の Advanced Configuration and Power Interface (ACPI) 名前空間のオブジェクトの要件があります。 このセクションでは、SoC ベースのプラットフォームに必要なその他のオブジェクトが一覧表示します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="acpi-device-specific-methods.md" data-raw-source="[ACPI device-specific methods](acpi-device-specific-methods.md)">ACPI デバイス固有のメソッド</a></p></td>
<td><p>高度な機能とテクノロジ スタックを選択する拡張機能をサポートするには、は、Windows は、デバイスのデバイスに固有のメソッド (_DSM) を定義します。</p></td>
</tr>
</tbody>
</table>

 

 

 




