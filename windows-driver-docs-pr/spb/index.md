---
title: Simple Peripheral Bus (SPB) ドライバー設計ガイド
description: このセクションでは、SPB (simple peripheral bus) コントローラー デバイス用、または SPB に接続された周辺機器用のドライバーを記述する方法について説明します。
ms.assetid: 7E9F688B-F473-4343-A1E0-525273391935
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
author: EliotSeattle
ms.openlocfilehash: 0efa5dae2495ee47b777d509950207f7ffe06c06
ms.sourcegitcommit: 988d100e4d3b218a59fdac034d39a1816d145c85
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/24/2020
ms.locfileid: "68473557"
---
# <a name="simple-peripheral-bus-spb-driver-design-guide"></a>Simple Peripheral Bus (SPB) ドライバー設計ガイド

このセクションでは、SPB ([simple peripheral bus](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))) コントローラー デバイス用、または SPB に接続された周辺機器用のドライバーを記述する方法について説明します。 SPB カテゴリには、I²C や SPI などのバスが含まれています。 SPB コントローラー デバイスのハードウェア ベンダーにより、コントローラーのハードウェア機能を管理するための SPB コントローラー ドライバーが提供されます。 このドライバーは、類似したコントローラー デバイスのファミリをサポートしている可能性があります。 SPB に接続された周辺機器のハードウェア ベンダーにより、周辺機器のハードウェア機能を管理するための SPB 周辺機器ドライバーが提供されます。 このドライバーは、互換性のある SPB を提供するさまざまなハードウェア プラットフォーム間で、周辺機器デバイスのファミリをサポートしている可能性があります。

Windows 8 よりも前のバージョンの Windows の場合、オペレーティング システムでは、PC マザーボード上の SPB に接続されたデバイスから、プラットフォームのファームウェアを経由して間接的にのみ情報を取得していました。 Windows 8 以降、ハードウェア ベンダーは、自社の SPB コントローラーとその SPB に接続された周辺機器を直接制御し、これらのデバイスをオペレーティング システムとアプリケーションから使用できるようにするための Windows ドライバーを提供することができます。 詳細については、「[SPB コントローラー ドライバー](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-controller-drivers)」と「[SPB 周辺機器ドライバー](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-peripheral-device-drivers)」を参照してください。

SPB は、低速の周辺機器をマザーボードのチップセットと System on a Chip (SoC) モジュールに接続するためによく使用されます。 集積回路では、シリアル バスに接続する場合、クロック サイクルごとに複数ビットのデータを転送するパラレル バスよりも必要なピンの数が少なくなります。 通常、SPB は、データ転送速度よりも少ないピン数とシンプルな接続が重要な、コスト重視のアプリケーションで使用されます。 SPB は低速で動作し、電気的接続をほとんど必要としないため、バッテリ電源を節約する必要があるアプリケーションでよく使用されます。

たとえば、ノート PC の PC マザーボードでは、バッテリ レベルを監視する低速デバイスとの通信に I²C バスを使用する場合があります。 同様に、スマート フォンや他のモバイル機器の SoC モジュールは、I²C バスを使用して、加速度計、GPS デバイス、温度センサーなどのセンサー デバイスに接続する場合があります。

SPB はプラグ アンド プレイ バスではありません。 通常、周辺機器は SPB との接続が固定されていて、削除できません。 周辺機器を SPB のスロットから取り外すことができたとしても、通常そのスロットはこのデバイス専用です。 システム起動時に、ハードウェア プラットフォームの ACPI ファームウェアによって、SPB に接続された周辺機器がプラグ アンド プレイ マネージャー用に列挙され、各デバイスの専用ハードウェア リソースが指定されます。

これらのリソースには、SPB へのデバイスの接続を識別する接続 ID が含まれています。 接続 ID には、SPB コントローラーがデバイスへの接続を確立するために必要とする情報 (たとえば、バス アドレスやバスのクロック周波数) がカプセル化されています。 その他のハードウェア リソースに、ドライバーが ISR を接続する割り込みが含まれる場合があります。 ただし、デバイスのハードウェア リソースには、デバイス レジスター用のメモリは含まれていません。 SPB に接続された周辺機器は、メモリ マップされず、SPB を介してのみアクセスできます。 詳細については、「[SPB 接続周辺機器の接続 ID](https://docs.microsoft.com/windows-hardware/drivers/spb/connection-ids-for-spb-connected-peripheral-devices)」を参照してください。

SPB では、周辺機器からプロセッサに割り込み要求を伝えるためのバス固有の手段は提供されません。 代わりに、SPB に接続された周辺機器は、SPB と SPB コントローラー両方の外側にある別のハードウェア パスを介して割り込みを通知します。 SPB に接続された周辺機器の割り込みサービス ルーチン (ISR) は、IRQL = PASSIVE\_LEVEL で実行される必要があります。これにより、SPB 経由でデバイスのハードウェア レジスターにシリアルにアクセスするために、I/O 要求を同期的に送信できます。 詳細については、「[SPB 接続周辺機器からの割り込み](https://docs.microsoft.com/windows-hardware/drivers/spb/interrupts-from-spb-connected-peripheral-devices)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容

|トピック|説明|
|----|----|
|[SPB コントローラー ドライバー](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-controller-drivers)|SPB コントローラーは、SPB ([simple peripheral bus](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))) を制御し、SPB に接続された周辺機器との間でデータを転送するデバイスです。 SPB コントローラーのハードウェア ベンダーにより、コントローラーのハードウェア機能を管理するための SPB コントローラー ドライバーが提供されます。|
|[SPB 周辺機器ドライバー](https://docs.microsoft.com/windows-hardware/drivers/spb/spb-peripheral-device-drivers)|SPB 周辺機器デバイス ドライバーは、SPB ([simple peripheral bus](https://docs.microsoft.com/previous-versions/hh450903(v=vs.85))) に接続された周辺機器を制御します。 このデバイスのハードウェア レジスターは、SPB を介してのみ利用できます。 デバイスに対して読み取りまたは書き込みを行うには、ドライバーから SPB コントローラーに I/O 要求を送信する必要があります。 このコントローラーのみが、デバイスとの間で SPB を経由したデータ転送を開始できます。|
|[Multi Interface Test Tool (MITT) によるテスト](https://docs.microsoft.com/windows-hardware/drivers/spb/testing-with-multi-interface-test-tool--mitt-)|Multi Interface Test Tool (MITT) は、UART、I2C、SPI、GPIO などの SPB (simple peripheral bus) についてハードウェアとソフトウェアを検証するためのテスト ツールです。 MITT には、FPGA 開発ボードが使用されており、ファームウェア、テスト バイナリ、ドライバーを含む、安価なテスト ソリューションを提供するソフトウェア パッケージが組み込まれています。|
