---
title: Acpi.sys The Windows ACPI Driver
description: ACPI の Windows ドライバー、Acpi.sys は、Windows オペレーティング システムの受信トレイ コンポーネントです。
ms.assetid: 38ca54e0-defe-48b2-ab00-a5f688c2eb01
keywords:
- ACPI ドライバー WDK の電源管理
- WDK の列挙子の電源管理
- Pdo WDK の電源管理
- フィルター DOs WDK 電源管理
- 物理デバイス オブジェクトの WDK 電源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9ea8501e889fe6ec44dd805b67a983fc8f9f82a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363450"
---
# <a name="acpisys-the-windows-acpi-driver"></a>Acpi.sys: Windows ACPI ドライバー


ACPI の Windows ドライバー、Acpi.sys は、Windows オペレーティング システムの受信トレイ コンポーネントです。 Acpi.sys の責任では、電源管理のサポートを含めるし、プラグ アンド プレイ (PnP) デバイスの列挙。 持つハードウェア プラットフォームで、 [ACPI BIOS](acpi-bios.md)、 [HAL](windows-kernel-mode-hal-library.md) Acpi.sys のベース システムの起動時に読み込まれると、[デバイス ツリー](device-tree.md)します。 Acpi.sys は、オペレーティング システムと ACPI BIOS 間のインターフェイスとして機能します。 Acpi.sys は、デバイス ツリーの他のドライバーに対して透過的です。

COM ポートのリソースを再プログラミングまたはシステムのウェイク アップの USB コント ローラーを有効にすると、特定のハードウェア プラットフォームで Acpi.sys によって実行されるその他のタスクが含まれます。

**このトピックの「**

-   [ACPI デバイス](#acpi-devices)
-   [ACPI の制御メソッド](#acpi-control-methods)
-   [ACPI の仕様](#acpi-specification)
-   [ACPI のデバッグ](#acpi-debugging)

## <a name="acpi-devices"></a>ACPI デバイス


ハードウェア プラットフォーム ベンダーは、プラットフォームのハードウェア トポロジを記述する ACPI BIOS で ACPI 名前空間の階層を指定します。 詳細については、次を参照してください。 [ACPI Namespace 階層](https://docs.microsoft.com/windows-hardware/drivers/bringup/acpi-namespace-hierarchy)します。

各デバイスを ACPI 名前空間の階層で説明されているは、ACPI の Windows ドライバー、Acpi.sys は、フィルター デバイス オブジェクト (フィルター操作を行います) または物理デバイス オブジェクト (PDO) のいずれかを作成します。 デバイスがマザーボードに内蔵されている場合、Acpi.sys は、ACPI bus フィルターを表すフィルター デバイス オブジェクトを作成し、バス ドライバー (PDO) のすぐ上のデバイス スタックに結び付けます。 システム ボードではなく、ACPI 名前空間で説明されている他のデバイスには、Acpi.sys は PDO を作成します。 Acpi.sys は、これらのデバイス オブジェクトを使用して、電源管理と PnP デバイス スタックの機能を提供します。 詳細については、次を参照してください。[デバイス スタック、デバイスを ACPI の](https://docs.microsoft.com/windows-hardware/drivers/acpi/device-stacks-for-an-acpi-device)します。

Acpi.sys がデバイス オブジェクトを作成する対象のデバイスと呼ばれる、 [ACPI デバイス](https://docs.microsoft.com/windows-hardware/drivers/acpi/supporting-acpi-devices)します。 ACPI のデバイスのセットでは、1 つのハードウェア プラットフォームによって異なるため、次へと、ACPI BIOS およびマザーボードの構成によって異なります。 Acpi.sys ACPI 名前空間では説明されているハードウェア プラットフォームに完全に接続されているデバイスに対してのみ、ACPI bus フィルターが読み込まれることに注意してください (通常、このデバイスはシリコンのコアに統合またはシステム ボードをはんだ付け)。 マザーボードのすべてのデバイスでは、ACPI のバス フィルターがあります。

すべての ACPI 機能は、上位レベルのドライバーに対して透過的です。 これらのドライバーする必要がありますいないに関して推測 ACPI フィルターの有無の特定のデバイス スタックで。

Acpi.sys と ACPI BIOS は、ACPI デバイスの基本的な機能をサポートします。 ACPI デバイスの機能強化のため、デバイス ベンダーは WDM 関数のドライバーを指定できます。 詳細については、次を参照してください。 [ACPI デバイス関数ドライバーの動作](https://docs.microsoft.com/windows-hardware/drivers/acpi/operation-of-an-acpi-device-function-driver)します。

定義のブロックで、デバイスを ACPI が指定された、[システム説明テーブル](https://docs.microsoft.com/windows-hardware/drivers/bringup/acpi-system-description-tables)ACPI BIOS でします。 デバイスの定義ブロックには、デバイスのデータにアクセスするために使用するデバイスのメモリの連続したブロック操作リージョンが、特に指定します。 Acpi.sys だけでは、操作、リージョン内のデータを変更します。 デバイスの関数のドライバーでは、操作、リージョン内のデータを読み取ることができますが、データを変更する必要があります。 呼び出されると、[操作リージョン ハンドラー](https://docs.microsoft.com/windows-hardware/drivers/acpi/implementing-an-operation-region-handler) Acpi.sys におけるデータ バッファーを送受信する操作領域内のバイト数を転送します。 関数のドライバーと Acpi.sys の結合操作デバイスに固有であり、ACPI BIOS でハードウェアの製造元によって定義されます。 一般に、関数のドライバーと Acpi.sys デバイスに固有の操作を実行し、情報を取得する操作領域で特定の領域にアクセスします。 詳細については、次を参照してください。[サポート、営業地域](https://docs.microsoft.com/windows-hardware/drivers/acpi/supporting-an-operation-region)します。

## <a name="acpi-control-methods"></a>ACPI の制御メソッド


ACPI 制御メソッドは、ソフトウェア オブジェクトを宣言および定義クエリを実行して ACPI のデバイスを構成する単純な操作です。 制御メソッドは、ACPI BIOS では保存され、ACPI 機械語 (AML) と呼ばれるバイト コード形式でエンコードされます。 デバイスの制御メソッドは、メモリ内のデバイスの ACPI 名前空間にシステム ファームウェアから読み込まれ、Acpi.sys、ACPI の Windows ドライバーによって解釈されます。

コントロールのメソッドを呼び出すには、ACPI デバイスの場合、カーネル モード ドライバーを開始する、 [ **IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)要求は、Acpi.sys によって処理されます。 デバイスを ACPI 列挙で読み込まれるドライバーについて Acpi.sys は常にドライバー スタックで物理デバイス オブジェクト (PDO) を実装します。 詳細については、次を参照してください。 [ACPI 制御メソッドを評価する](https://docs.microsoft.com/windows-hardware/drivers/acpi/evaluating-acpi-control-methods)します。

## <a name="acpi-specification"></a>ACPI の仕様


最新の*Advanced Configuration and Power Interface Specification*を参照してください、 [ACPI 5.0 仕様](https://uefi.org/specifications)拡張ファームウェア インターフェイス フォーラムの統合された web サイトから入手できます。 ACPI 仕様のリビジョン 5.0 には、省電力、モバイル Pc チップ (SoC) 統合の回線でシステムに基づくし、実装をサポートする機能のセットが導入されて、[コネクト スタンバイ](https://docs.microsoft.com/windows-hardware/design/device-experiences/modern-standby)電源モデル。 ACPI の Windows ドライバーを Windows 8 と Windows 8.1 では、以降、Acpi.sys は、ACPI 5.0 仕様での新機能をサポートします。 詳細については、次を参照してください。 [SoC プラットフォーム用の Windows ACPI 設計ガイド](https://docs.microsoft.com/windows-hardware/drivers/bringup/windows-acpi-design-guide-for-soc-platforms)します。

## <a name="acpi-debugging"></a>ACPI のデバッグ


システム インテグレーター、デバイス ドライバー開発者向けの ACPI は、Microsoft を使用できます[AMLI デバッガー](https://docs.microsoft.com/windows-hardware/drivers/debugger/introduction-to-the-amli-debugger) AML コードをデバッグします。 AML はインタープリター言語であるため AML デバッグ、特別なソフトウェア ツールが必要です。 チェックされているバージョン Windows ACPI ドライバー、Acpi.sys にはには、AML デバッグをサポートするためにデバッガーのコンポーネントが含まれます。 AMLI デバッガーの詳細については、次を参照してください。 [ACPI デバッグ](https://docs.microsoft.com/windows-hardware/drivers/debugger/acpi-debugging)します。 Windows のチェック ビルドをダウンロードする方法については、次を参照してください。[をチェック ビルドの Windows をダウンロード](https://docs.microsoft.com/windows-hardware/drivers/devtest/obtaining-the-checked-build)します。 AML ACPI ソース言語 (ASL) にコンパイルする方法の詳細については、次を参照してください。 [Microsoft ASL コンパイラ](https://docs.microsoft.com/windows-hardware/drivers/bringup/microsoft-asl-compiler)します。

 

 




