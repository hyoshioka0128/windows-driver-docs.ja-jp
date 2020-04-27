---
title: 'Acpi.sys: Windows ACPI ドライバー'
description: Windows ACPI ドライバー (Acpi.sys) は、Windows オペレーティング システムのインボックス コンポーネントです。
ms.assetid: 38ca54e0-defe-48b2-ab00-a5f688c2eb01
keywords:
- ACPI ドライバー WDK 電源管理
- 列挙子 WDK 電源管理
- PDO WDK 電源管理
- フィルター DO WDK 電源管理
- 物理デバイス オブジェクト WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: High
ms.openlocfilehash: 09062c0572ac672a66b4f39d6bd000898601cf56
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "74261407"
---
# <a name="acpisys-the-windows-acpi-driver"></a>Acpi.sys: Windows ACPI ドライバー


Windows ACPI ドライバー (Acpi.sys) は、Windows オペレーティング システムのインボックス コンポーネントです。 Acpi.sys の役割には、電源管理とプラグ アンド プレイ (PnP) デバイス列挙のサポートが含まれます。 [ACPI BIOS](acpi-bios.md) を搭載しているハードウェア プラットフォームでは、[HAL](windows-kernel-mode-hal-library.md) により、システム起動時に[デバイス ツリー](device-tree.md)のベースに Acpi.sys が読み込まれます。 Acpi.sys は、オペレーティング システムと ACPI BIOS の間のインターフェイスとして機能します。 Acpi.sys は、デバイス ツリー内の他のドライバーに対して透過的です。

特定のハードウェア プラットフォームで Acpi.sys によって実行されるその他のタスクには、COM ポートのリソースの再プログラミング、またはシステム ウェイクアップ用の USB コントローラーの有効化が含まれる場合があります。

**このトピックの内容**

-   [ACPI デバイス](#acpi-devices)
-   [ACPI 制御メソッド](#acpi-control-methods)
-   [ACPI の仕様](#acpi-specification)
-   [ACPI のデバッグ](#acpi-debugging)

## <a name="acpi-devices"></a>ACPI デバイス


ハードウェア プラットフォーム ベンダーは、プラットフォームのハードウェア トポロジを記述するために、ACPI BIOS 内の ACPI 名前空間の階層を指定します。 詳細については、「[ACPI 名前空間の階層](https://docs.microsoft.com/windows-hardware/drivers/bringup/acpi-namespace-hierarchy)」を参照してください。

ACPI 名前空間の階層で記述されている各デバイスについて、Windows ACPI ドライバーである Acpi.sys は、フィルター デバイス オブジェクト (フィルター DO) または物理デバイス オブジェクト (PDO) を作成します。 デバイスがシステム ボードに統合されている場合は、Acpi.sys により、ACPI バス フィルターを表すフィルター デバイス オブジェクトが作成され、バス ドライバー (PDO) のすぐ上のデバイス スタックに接続されます。 ACPI 名前空間で記述されているがシステム ボード上にはないその他のデバイスについては、Acpi.sys によって PDO が作成されます。 Acpi.sys は、これらのデバイス オブジェクトを使用して、デバイス スタックに電源管理機能と PnP 機能を提供します。 詳細については、「[ACPI デバイスのデバイス スタック](https://docs.microsoft.com/windows-hardware/drivers/acpi/device-stacks-for-an-acpi-device)」をご覧ください。

Acpi.sys によってデバイス オブジェクトが作成されるデバイスは、[ACPI デバイス](https://docs.microsoft.com/windows-hardware/drivers/acpi/supporting-acpi-devices)と呼ばれます。 ACPI デバイスのセットは、ハードウェア プラットフォームによって異なり、ACPI BIOS およびマザーボードの構成に依存します。 Acpi.sys が ACPI バス フィルターを読み込むのは、ACPI 名前空間で記述されており、ハードウェア プラットフォームに永続的に接続されたデバイスに対してのみであることに注意してください (通常、このデバイスは、コア シリコンに統合されているか、システム ボードにはんだ付けされています)。 すべてのマザーボード デバイスが ACPI バス フィルターを持つわけではありません。

すべての ACPI 機能は、上位レベルのドライバーに対して透過的です。 これらのドライバーでは、特定のデバイス スタックに ACPI フィルターが存在するか、存在しないかについて想定する必要はありません。

Acpi.sys および ACPI BIOS は、ACPI デバイスの基本的な機能をサポートします。 デバイス ベンダーでは、ACPI デバイスの機能を強化するために WDM 機能ドライバーを提供できます。 詳細については、「[ACPI デバイス機能ドライバーの操作](https://docs.microsoft.com/windows-hardware/drivers/acpi/operation-of-an-acpi-device-function-driver)」をご覧ください。

ACPI デバイスは、ACPI BIOS の[システム記述テーブル](https://docs.microsoft.com/windows-hardware/drivers/bringup/acpi-system-description-tables)の定義ブロックで指定されます。 デバイスの定義ブロックは、デバイス データへのアクセスに使用されるデバイス メモリの連続したブロックである操作領域を指定します。 操作領域のデータを変更するのは、Acpi.sys のみです。 デバイスの機能ドライバーは、操作領域内のデータを読み取ることができますが、データを変更してはなりません。 [操作領域ハンドラー](https://docs.microsoft.com/windows-hardware/drivers/acpi/implementing-an-operation-region-handler)が呼び出されると、操作領域内のバイトが Acpi.sys のデータ バッファーとの間で転送されます。 機能ドライバーおよび Acpi.sys の結合された操作はデバイスに固有であり、ハードウェア ベンダーによって ACPI BIOS で定義されます。 一般に、機能ドライバーと Acpi.sys では、操作領域内の特定の領域にアクセスしてデバイス固有の操作を実行し、情報を取得します。 詳細については、「[操作領域をサポートする](https://docs.microsoft.com/windows-hardware/drivers/acpi/supporting-an-operation-region)」をご覧ください。

## <a name="acpi-control-methods"></a>ACPI 制御メソッド


ACPI 制御メソッドは、ACPI デバイスの照会と構成を行うための単純な操作を宣言して定義するソフトウェア オブジェクトです。 制御メソッドは ACPI BIOS に格納され、ACPI 機械語 (AML) と呼ばれるバイト コード形式でエンコードされています。 デバイスの制御メソッドは、システム ファームウェアからメモリ内のデバイスの ACPI 名前空間に読み込まれ、Windows ACPI ドライバー (Acpi.sys) によって解釈されます。

制御メソッドを呼び出すには、ACPI デバイスのカーネル モード ドライバーで [**IRP\_MJ\_DEVICE\_CONTROL**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control) 要求を開始します。これは Acpi.sys によって処理されます。 ACPI で列挙されたデバイスに読み込まれたドライバーに対して、Acpi.sys は常にドライバー スタック内に物理デバイス オブジェクト (PDO) を実装します。 詳細については、「[ACPI 制御メソッドを評価する](https://docs.microsoft.com/windows-hardware/drivers/acpi/evaluating-acpi-control-methods)」をご覧ください。

## <a name="acpi-specification"></a>ACPI の仕様


最新の *Advanced Configuration and Power Interface の仕様*については、Unified Extensible Firmware Interface フォーラムの Web サイトから入手できる [ACPI 5.0 仕様](https://uefi.org/specifications)をご覧ください。 ACPI 仕様のリビジョン 5.0 では、システム オン チップ (SoC) IC をベースとし、[コネクト スタンバイ](https://docs.microsoft.com/windows-hardware/design/device-experiences/modern-standby)電源モデルを実装する省電力のモバイル PC をサポートする機能のセットが導入されています。 Windows 8 および Windows 8.1 以降では、Windows ACPI ドライバー Acpi.sys により、ACPI 5.0 仕様の新機能がサポートされています。 詳細については、「[SoC プラットフォーム向け Windows ACPI 設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/bringup/windows-acpi-design-guide-for-soc-platforms)」をご覧ください。

## <a name="acpi-debugging"></a>ACPI のデバッグ


システム インテグレーターおよび ACPI デバイス ドライバーの開発者は、Microsoft [AMLI デバッガー](https://docs.microsoft.com/windows-hardware/drivers/debugger/introduction-to-the-amli-debugger)を使用して AML コードをデバッグできます。 AML はインタープリター言語であるため、AML のデバッグには特別なソフトウェア ツールが必要です。

AMLI デバッガーの詳細については、「[ACPI のデバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/acpi-debugging)」を参照してください。

ACPI ソース言語 (ASL) を AML にコンパイルする方法については、「[Microsoft ASL コンパイラ](https://docs.microsoft.com/windows-hardware/drivers/bringup/microsoft-asl-compiler)」をご覧ください。

 

 




