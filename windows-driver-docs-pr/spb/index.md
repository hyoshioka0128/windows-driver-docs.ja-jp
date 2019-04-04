---
title: SPB (Simple Peripheral Bus) ドライバー設計ガイド
description: このセクションでは、SPB (simple peripheral bus) コントローラー デバイス用、または SPB に接続された周辺機器用のドライバーを記述する方法について説明します。
ms.assetid: 7E9F688B-F473-4343-A1E0-525273391935
ms.date: 04/20/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 4da857be0cb7a6d7775f4711a400275dfd2c0c58
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56465752"
---
# <a name="simple-peripheral-bus-spb-driver-design-guide"></a>SPB (Simple Peripheral Bus) ドライバー設計ガイド


このセクションでは、SPB ([simple peripheral bus](https://msdn.microsoft.com/library/windows/hardware/hh450903)) コントローラー デバイス用、または SPB に接続された周辺機器用のドライバーを記述する方法について説明します。 SPB カテゴリには、I²C や SPI などのバスが含まれています。 SPB コントローラー デバイスのハードウェア ベンダーにより、コントローラーのハードウェア機能を管理するための SPB コントローラー ドライバーが提供されます。 このドライバーは、類似したコントローラー デバイスのファミリをサポートしている可能性があります。 SPB に接続された周辺機器のハードウェア ベンダーにより、周辺機器のハードウェア機能を管理するための SPB 周辺機器ドライバーが提供されます。 このドライバーは、互換性のある SPB を提供するさまざまなハードウェア プラットフォーム間で、周辺機器デバイスのファミリをサポートしている可能性があります。

Windows 8 よりも前のバージョンの Windows の場合、オペレーティング システムでは、PC マザーボード上の SPB に接続されたデバイスから、プラットフォームのファームウェアを経由して間接的にのみ情報を取得していました。 Windows 8 以降、ハードウェア ベンダーは、自社の SPB コントローラーとその SPB に接続された周辺機器を直接制御し、これらのデバイスをオペレーティング システムとアプリケーションから使用できるようにするための Windows ドライバーを提供することができます。 詳細については、「[SPB コントローラー ドライバー](https://msdn.microsoft.com/library/windows/hardware/hh698220)」と「[SPB 周辺機器ドライバー](https://msdn.microsoft.com/library/windows/hardware/hh698225)」を参照してください。

SPB は、低速の周辺機器をマザーボードのチップセットと System on a Chip (SoC) モジュールに接続するためによく使用されます。 集積回路では、シリアル バスに接続する場合、クロック サイクルごとに複数ビットのデータを転送するパラレル バスよりも必要なピンの数が少なくなります。 通常、SPB は、データ転送速度よりも少ないピン数とシンプルな接続が重要な、コスト重視のアプリケーションで使用されます。 SPB は低速で動作し、電気的接続をほとんど必要としないため、バッテリ電源を節約する必要があるアプリケーションでよく使用されます。

たとえば、ノート PC の PC マザーボードでは、バッテリ レベルを監視する低速デバイスとの通信に I²C バスを使用する場合があります。 同様に、スマート フォンや他のモバイル機器の SoC モジュールは、I²C バスを使用して、加速度計、GPS デバイス、温度センサーなどのセンサー デバイスに接続する場合があります。

SPB はプラグ アンド プレイ バスではありません。 通常、周辺機器は SPB との接続が固定されていて、削除できません。 周辺機器を SPB のスロットから取り外すことができたとしても、通常そのスロットはこのデバイス専用です。 システム起動時に、ハードウェア プラットフォームの ACPI ファームウェアによって、SPB に接続された周辺機器がプラグ アンド プレイ マネージャー用に列挙され、各デバイスの専用ハードウェア リソースが指定されます。

これらのリソースには、SPB へのデバイスの接続を識別する接続 ID が含まれています。 接続 ID には、SPB コントローラーがデバイスへの接続を確立するために必要とする情報 (たとえば、バス アドレスやバスのクロック周波数) がカプセル化されています。 その他のハードウェア リソースに、ドライバーが ISR を接続する割り込みが含まれる場合があります。 ただし、デバイスのハードウェア リソースには、デバイス レジスター用のメモリは含まれていません。 SPB に接続された周辺機器は、メモリ マップされず、SPB を介してのみアクセスできます。 詳細については、「[SPB 接続周辺機器の接続 ID](https://msdn.microsoft.com/library/windows/hardware/hh698216)」を参照してください。

SPB では、周辺機器からプロセッサに割り込み要求を伝えるためのバス固有の手段は提供されません。 代わりに、SPB に接続された周辺機器は、SPB と SPB コントローラー両方の外側にある別のハードウェア パスを介して割り込みを通知します。 SPB に接続された周辺機器の割り込みサービス ルーチン (ISR) は、IRQL = PASSIVE\_LEVEL で実行される必要があります。これにより、SPB 経由でデバイスのハードウェア レジスターにシリアルにアクセスするために、I/O 要求を同期的に送信できます。 詳細については、「[SPB 接続周辺機器からの割り込み](https://msdn.microsoft.com/library/windows/hardware/hh698218)」を参照してください。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh698220" data-raw-source="[SPB controller drivers](https://msdn.microsoft.com/library/windows/hardware/hh698220)">SPB コントローラー ドライバー</a></p></td>
<td><p>SPB コントローラーは、SPB (<a href="https://msdn.microsoft.com/library/windows/hardware/hh450903" data-raw-source="[simple peripheral bus](https://msdn.microsoft.com/library/windows/hardware/hh450903)">simple peripheral bus</a>) を制御し、SPB に接続された周辺機器との間でデータを転送するデバイスです。 SPB コントローラーのハードウェア ベンダーにより、コントローラーのハードウェア機能を管理するための SPB コントローラー ドライバーが提供されます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh698225" data-raw-source="[SPB peripheral device drivers](https://msdn.microsoft.com/library/windows/hardware/hh698225)">SPB 周辺機器ドライバー</a></p></td>
<td><p>SPB 周辺機器デバイス ドライバーは、SPB (<a href="https://msdn.microsoft.com/library/windows/hardware/hh450903" data-raw-source="[simple peripheral bus](https://msdn.microsoft.com/library/windows/hardware/hh450903)">simple peripheral bus</a>) に接続された周辺機器を制御します。 このデバイスのハードウェア レジスターは、SPB を介してのみ利用できます。 デバイスに対して読み取りまたは書き込みを行うには、ドライバーから SPB コントローラーに I/O 要求を送信する必要があります。 このコントローラーのみが、デバイスとの間で SPB を経由したデータ転送を開始できます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn919874" data-raw-source="[Test with Multi Interface Test Tool (MITT)](https://msdn.microsoft.com/library/windows/hardware/dn919874)">Multi Interface Test Tool (MITT) によるテスト</a></p></td>
<td><p>Multi Interface Test Tool (MITT) は、UART、I2C、SPI、GPIO などの SPB (simple peripheral bus) についてハードウェアとソフトウェアを検証するためのテスト ツールです。 MITT には、FPGA 開発ボードが使用されており、ファームウェア、テスト バイナリ、ドライバーを含む、安価なテスト ソリューションを提供するソフトウェア パッケージが組み込まれています。</p></td>
</tr>
</tbody>
</table>

 

 

 




