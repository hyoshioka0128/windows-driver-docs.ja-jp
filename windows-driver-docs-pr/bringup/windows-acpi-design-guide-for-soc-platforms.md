---
title: SoC プラットフォーム向け Windows ACPI 設計ガイド
description: ACPI 5.0 では、接続されたスタンバイ電源モデルを実装する SoC ICs に基づいて、低電力のモバイルデバイスをサポートするための新機能を定義しています。
ms.assetid: 661BFB7E-D190-450D-A466-7D6AD0EAAAB0
ms.date: 05/26/2020
ms.localizationpriority: medium
ms.openlocfilehash: d48939d314a7293052cbcfaa9b61c4314e5e3163
ms.sourcegitcommit: 5273e44c5c6c1c87952d74e95e5473c32a916d10
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2020
ms.locfileid: "84122692"
---
# <a name="windows-acpi-design-guide-for-soc-platforms"></a>SoC プラットフォーム向け Windows ACPI 設計ガイド

Advanced Configuration and Power Interface Specification, Revision 5.0 ([ACPI 5.0 仕様](https://uefi.org/specifications)) では、システム オン チップ (SoC) IC をベースとし、コネクト スタンバイ電源モデルを実装する省電力のモバイル デバイスをサポートする新しい機能のセットが定義されています。 Windows 8 と Windows 8.1 以降、Windows では SoC ベースのプラットフォームの新しい ACPI 5.0 機能がサポートされています。

このセクションでは、ACPI 5.0 仕様の新機能をサポートする Windows Pc およびデバイスを実装するためのガイドラインを示します。 ファームウェア開発者やシステム設計者は、これらのガイドラインを使用して、プラットフォームで Windows が正しく動作することを確認できます。 Windows ファームウェアのすべての要件の一覧については、 [Windows 認定プログラム](https://docs.microsoft.com/previous-versions/windows/hardware/hck/jj124227(v=vs.85))のドキュメントを参照してください。

## <a name="in-this-section"></a>このセクションの内容

| トピック | 説明 |
| --- | --- |
| [ACPI 5.0 に対する Windows のサポートの概要](overview-of-windows-support-for-acpi-5-0.md) | [ACPI 5.0 仕様](https://uefi.org/specifications)では、windows 8 以降を実行する SoC ベースのモバイルプラットフォームのサポートが有効になりますが、以前のバージョンの windows で導入された多くの便利な機能は引き続きサポートされます。 この設計ガイドでは、SoC ベースのプラットフォームに特に適用される ACPI 5.0 の部分に実装を指示し、これらのプラットフォームで Windows を実行するために、ACPI で SoC 固有の機能を実装するためのベストプラクティスについて説明します。 |
| [ACPI システム記述テーブル](acpi-system-description-tables.md) | Advanced Configuration and Power Interface (ACPI) ハードウェア仕様の実装は、BIOS ベースのプラットフォームや、BIOS ベースの Windows Server システムでは必須ではありませんが、ACPI ソフトウェアの仕様の多くは必須です。 ACPI では、汎用的な拡張可能なテーブル渡しメカニズムに加え、プラットフォームをオペレーティングシステムに記述するための特定のテーブルが定義されています。 |
| [デバイス管理用の名前空間オブジェクト](device-management-namespace-objects.md) | [ACPI 5.0 仕様](https://uefi.org/specifications)では、デバイスの管理に使用できる名前空間オブジェクトの種類がいくつか定義されています。 たとえば、デバイス識別オブジェクトには、子デバイスのハードウェアの列挙をサポートしていない、I2C などのバスに接続するデバイスの識別情報が含まれています。 その他の種類の名前空間オブジェクトは、システムリソースを指定したり、デバイスの依存関係を記述したり、どのデバイスを無効にできるかを示したりすることができます。 |
| [汎用入出力 (GPIO)](general-purpose-i-o--gpio-.md) | SoC 統合回線では、汎用 i/o (GPIO) ピンが広く使用されています。 SoC ベースのプラットフォームの場合、Windows は GPIO ハードウェアの一般的な抽象化を定義します。この抽象化には、Advanced Configuration and Power Interface (ACPI) 名前空間のサポートが必要です。 |
| [シンプルな周辺機器バス (SPB)](simple-peripheral-bus--spb-.md) | SoC 統合回線では、プラットフォーム周辺機器に接続するために、シンプルで低ピンのカウントと低電力のシリアルの相互接続が広く使用されています。 I ² C、SPI、および Uart は例です。 SoC ベースのプラットフォームの場合、Windows ではシンプルな周辺機器バス (SPB) ハードウェアの一般的な抽象化が提供されます。この抽象化には、Advanced Configuration and Power Interface (ACPI) 名前空間の新しいサポートが必要です。 |
| [デバイス電源管理](device-power-management.md) | [ACPI 5.0 仕様](https://uefi.org/specifications)では、デバイスのデバイスの電源情報を指定する一連の名前空間オブジェクトを定義します。 たとえば、1つのオブジェクトセットで、サポートされている各デバイスの電源状態でデバイスが必要とする電源リソースを指定できます。 別のオブジェクトの種類では、ハードウェアイベントに応答して、デバイスが低電力状態から復帰する機能を記述できます。 |
| [ACPI で定義されたデバイス](acpi-defined-devices.md) | [ACPI 5.0 仕様](https://uefi.org/specifications)では、一般的なプラットフォーム機能を表すデバイスの種類をいくつか定義しています。 たとえば、ACPI は電源ボタン、スリープボタン、およびシステムインジケーターを定義します。 SoC ベースのプラットフォームの場合、Windows には、この記事で説明されている ACPI 定義デバイスをサポートする組み込みドライバーが用意されています。 |
| [その他の ACPI 名前空間オブジェクト](other-acpi-namespace-objects.md) | デバイスの特定のクラスについては、名前空間内のこれらのデバイスの下に、追加の高度な構成と電源インターフェイス (ACPI) の名前空間オブジェクトを表示するための要件があります。 このセクションでは、SoC ベースのプラットフォームに必要な追加のオブジェクトの一覧を示します。 |
| [ACPI デバイス固有のメソッド](acpi-device-specific-methods.md) | テクノロジスタックを選択するための機能と拡張機能の向上をサポートするために、Windows はデバイスのデバイス固有のメソッド (_DSM) を定義します。 |
