---
title: Acpi Windows ACPI ドライバー
description: Windows ACPI ドライバー (Acpi) は、Windows オペレーティングシステムの受信トレイコンポーネントです。
ms.assetid: 38ca54e0-defe-48b2-ab00-a5f688c2eb01
keywords:
- ACPI ドライバー WDK 電源管理
- 列挙子 WDK 電源管理
- PDOs WDK の電源管理
- DOs WDK 電源管理のフィルター処理
- 物理デバイスオブジェクト WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: High
ms.openlocfilehash: f43a17c54033fd82a2f21596013571fcf658a4d0
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007637"
---
# <a name="acpisys-the-windows-acpi-driver"></a>Acpi.sys: Windows ACPI ドライバー


Windows ACPI ドライバー (Acpi) は、Windows オペレーティングシステムの受信トレイコンポーネントです。 Acpi の役割には、電源管理とプラグアンドプレイ (PnP) デバイス列挙のサポートが含まれます。 [ACPI BIOS](acpi-bios.md)が搭載されているハードウェアプラットフォームでは、 [HAL](windows-kernel-mode-hal-library.md)によって、システムの起動時に[デバイスツリー](device-tree.md)のベースで acpi が読み込まれます。 Acpi は、オペレーティングシステムと ACPI BIOS の間のインターフェイスとして機能します。 Acpi は、デバイスツリー内の他のドライバーに対して透過的です。

特定のハードウェアプラットフォームで Acpi によって実行されるその他のタスクには、COM ポートのリソースの reprogramming、またはシステムウェイクアップ用の USB コントローラーの有効化が含まれる場合があります。

**このトピックの内容**

-   [ACPI デバイス](#acpi-devices)
-   [ACPI 制御メソッド](#acpi-control-methods)
-   [ACPI 仕様](#acpi-specification)
-   [ACPI デバッグ](#acpi-debugging)

## <a name="acpi-devices"></a>ACPI デバイス


ハードウェアプラットフォームベンダーは、プラットフォームのハードウェアトポロジを説明するために、acpi BIOS で ACPI 名前空間の階層を指定します。 詳細については、「 [ACPI 名前空間の階層](https://docs.microsoft.com/windows-hardware/drivers/bringup/acpi-namespace-hierarchy)」を参照してください。

ACPI 名前空間階層で説明されている各デバイスについて、Windows ACPI ドライバーである Acpi は、フィルターデバイスオブジェクト (フィルター DO) または物理デバイスオブジェクト (PDO) を作成します。 デバイスがシステムボードに統合されている場合、Acpi は、ACPI バスフィルターを表すフィルターデバイスオブジェクトを作成し、バスドライバー (PDO) のすぐ上のデバイススタックに接続します。 ACPI 名前空間で説明されているがシステムボードではないその他のデバイスについては、Acpi によって PDO が作成されます。 Acpi は、これらのデバイスオブジェクトを使用して、デバイススタックに電源管理機能と PnP 機能を提供します。 詳細については、「[デバイススタック (ACPI デバイス](https://docs.microsoft.com/windows-hardware/drivers/acpi/device-stacks-for-an-acpi-device))」を参照してください。

Acpi によってデバイスオブジェクトが作成されるデバイスは、 [acpi デバイス](https://docs.microsoft.com/windows-hardware/drivers/acpi/supporting-acpi-devices)と呼ばれます。 ACPI デバイスのセットは、ハードウェアプラットフォームによって次のように異なり、ACPI BIOS およびマザーボードの構成によって異なります。 Acpi は、acpi 名前空間で説明されているデバイスに対してのみ ACPI バスフィルターを読み込むことに注意してください (通常、このデバイスは、システムボードのコアシリコンまたははんだに統合されています)。 すべてのマザーボードデバイスに ACPI バスフィルターが適用されているわけではありません。

すべての ACPI 機能は、上位レベルのドライバーに対して透過的です。 これらのドライバーは、特定のデバイススタックに ACPI フィルターが存在するかどうかを想定していない必要があります。

Acpi および ACPI BIOS は、ACPI デバイスの基本的な機能をサポートしています。 デバイスベンダーは、ACPI デバイスの機能を強化するために、WDM 関数ドライバーを提供できます。 詳細については、「 [ACPI デバイス関数ドライバーの操作](https://docs.microsoft.com/windows-hardware/drivers/acpi/operation-of-an-acpi-device-function-driver)」を参照してください。

Acpi デバイスは、ACPI BIOS の[システム記述テーブル](https://docs.microsoft.com/windows-hardware/drivers/bringup/acpi-system-description-tables)の定義ブロックによって指定されます。 デバイスの定義ブロックは、特に、デバイスデータへのアクセスに使用されるデバイスメモリの連続したブロックである操作領域を指定します。 操作領域のデータは、Acpi のみによって変更されます。 デバイスの関数ドライバーは、操作領域内のデータを読み取ることができますが、データを変更することはできません。 [操作領域ハンドラー](https://docs.microsoft.com/windows-hardware/drivers/acpi/implementing-an-operation-region-handler)が呼び出されると、操作領域のバイトを、Acpi のデータバッファーとの間で転送します。 関数ドライバーと Acpi の組み合わせ操作はデバイス固有であり、ハードウェアベンダーによって ACPI BIOS で定義されます。 一般に、関数ドライバーと Acpi は、操作領域内の特定の領域にアクセスして、デバイス固有の操作を実行し、情報を取得します。 詳細については、「[操作領域のサポート](https://docs.microsoft.com/windows-hardware/drivers/acpi/supporting-an-operation-region)」を参照してください。

## <a name="acpi-control-methods"></a>ACPI 制御メソッド


ACPI 制御方式は、ACPI デバイスのクエリと構成を行うための単純な操作を宣言して定義するソフトウェアオブジェクトです。 コントロールメソッドは ACPI BIOS に格納され、ACPI コンピューター言語 (AML) と呼ばれるバイトコード形式でエンコードされます。 デバイスの制御メソッドは、システムファームウェアからメモリ内のデバイスの ACPI 名前空間に読み込まれ、Windows ACPI ドライバー (Acpi) によって解釈されます。

制御メソッドを呼び出すために、ACPI デバイスのカーネルモードドライバーは、 [**IRP @ no__t-2MJ @ no__t-3DEVICE @ no__t-4control**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)要求を開始します。この要求は、acpi によって処理されます。 ACPI で列挙されたデバイスに読み込まれたドライバーの場合、Acpi は常にドライバースタックに物理デバイスオブジェクト (PDO) を実装します。 詳細については、「 [ACPI 制御メソッドの評価](https://docs.microsoft.com/windows-hardware/drivers/acpi/evaluating-acpi-control-methods)」を参照してください。

## <a name="acpi-specification"></a>ACPI 仕様


最新の*高度な構成と電源インターフェイスの仕様*については、Unified Extensible Firmware Interface フォーラム web サイトから入手できる[ACPI 5.0 仕様](https://uefi.org/specifications)を参照してください。 ACPI 仕様のリビジョン5.0 では、低電力のモバイル Pc をサポートするための一連の機能が導入されています。この Pc は、チップ (SoC) 統合回線上のシステムに基づいており、[コネクトスタンバイ](https://docs.microsoft.com/windows-hardware/design/device-experiences/modern-standby)電源モデルを実装しています。 Windows 8 と Windows 8.1 以降では、acpi 5.0 仕様の新機能がサポートされています。 詳細については、「 [WINDOWS ACPI 設計ガイド (SoC プラットフォーム用](https://docs.microsoft.com/windows-hardware/drivers/bringup/windows-acpi-design-guide-for-soc-platforms))」を参照してください。

## <a name="acpi-debugging"></a>ACPI デバッグ


システムインテグレーターと ACPI デバイスドライバーの開発者は、Microsoft [Amli デバッガー](https://docs.microsoft.com/windows-hardware/drivers/debugger/introduction-to-the-amli-debugger)を使用して AML コードをデバッグできます。 AML は解釈された言語であるため、AML のデバッグには特別なソフトウェアツールが必要です。 チェックを行うバージョンの Windows ACPI ドライバーである Acpi には、AML デバッグをサポートするためのデバッガーコンポーネントが含まれています。 AMLI デバッガーの詳細については、「 [ACPI デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/acpi-debugging)」を参照してください。 Windows のチェックされたビルドをダウンロードする方法の詳細については、「 [windows のチェック済みビルドのダウンロード](https://docs.microsoft.com/windows-hardware/drivers/devtest/obtaining-the-checked-build)」を参照してください。 ACPI ソース言語 (ASL) を AML にコンパイルする方法については、「 [MICROSOFT ASL Compiler](https://docs.microsoft.com/windows-hardware/drivers/bringup/microsoft-asl-compiler)」を参照してください。

 

 




