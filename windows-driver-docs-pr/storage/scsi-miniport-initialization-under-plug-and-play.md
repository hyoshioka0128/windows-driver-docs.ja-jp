---
title: プラグ アンド プレイでの SCSI ミニポートの初期化
description: プラグ アンド プレイでの SCSI ミニポートの初期化
ms.assetid: bf2f9809-8271-4f0f-a2c4-25127fe9c4aa
keywords:
- SCSI ミニポートドライバー WDK 記憶域、PnP
- PnP WDK SCSI
- WDK SCSI のプラグアンドプレイ
- SCSI ミニポートドライバーの初期化
- SCSI ミニポートドライバー WDK ストレージ、初期化
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 675994d06427a396439c3cbc4eff403ec711b00d
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252452"
---
# <a name="scsi-miniport-initialization-under-plug-and-play"></a>プラグ アンド プレイでの SCSI ミニポートの初期化

Windows 2000 以降では、レガシミニポートドライバーは、Microsoft Windows NT 4.0 の場合とまったく同じ方法で初期化されます。 レガシミニポートドライバーが[**ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)を呼び出すと、ポートドライバーはミニポートドライバーを呼び出して、その HBA を特定し、初期化します。 これは、検出された HBA ごとに1回 (HBA が列挙可能なバス上にある場合)、またはミニポートドライバーによって他のデバイスが検出できないことが報告されるまで繰り返します。 次に、コントロールはミニポートドライバーの[**Driverentry**](driverentry-of-scsi-miniport-driver.md)ルーチンに戻ります。このルーチンでは、別の種類の HBA (たとえば、別のインターフェイスまたは別のベンダーと製品 ID) に対して、ミニポートドライバーが**ScsiPortInitialize**を再度呼び出すことができます。 すべての初期化呼び出しはミニポートドライバーの**Driverentry**ルーチンのコンテキスト内で行われ、 **ScsiPortInitialize**が呼び出された順序で作成されます。 レガシドライバーの初期化は、システムの起動時と、それ以外の時間に発生します。

プラグアンドプレイでは、初期化の順序を維持することはできません。 プラグアンドプレイに対して有効になっているミニポートドライバーが**ScsiPortInitialize**を呼び出すと、ポートドライバーは、後で参照できるように初期化データを格納し、STATUS_SUCCESS を返します。 これは、ミニポートドライバーの**PnPInterface**レジストリキーに記載されているインターフェイスの種類ごとに実行されます。このキーに記載されて*いない*インターフェイスは、すぐに初期化されます。

その後、プラグアンドプレイ manager がミニポートドライバーの HBA を検出すると、ポートドライバーに通知します。 ポートドライバーは、必要なシステムリソース (ミニポートドライバーのデバイス拡張機能用のメモリなど) を割り当て、ミニポートドライバーを呼び出して HBA を検出し、初期化します。 これは通常、システムの起動時に発生しますが、システムがドッキング操作を検出した場合や、CardBus などの HBA がシステムにホットプラグされた場合にも発生する可能性があります。

プラグアンドプレイ manager によってデバイスが報告されると、そのデバイス*とデバイスだけ*に対して、バスリソース (i/o ポート、メモリアドレス、割り込みなど) が既に割り当てられています。 これらのリソースはミニポートドライバーに提供され、これらのリソースを使用するか、デバイスが見つからなかったことを報告する必要があります。 特に、ミニポートドライバーは、デバイスを検索するために指定されたポートまたはメモリの場所にアクセスしようとすることはできません。

プラグアンドプレイドライバーとして起動されたミニポートドライバーは、非列挙型バス上のデバイスを検出するように求められることがあります。 これには、ポートの HBA を検出するために、ミニポートドライバーがバス上でコマンドを発行する必要がある ISA などのバスが含まれます。 このような検出中に見つかったデバイスはレジストリに記録され、次回システムを起動したときにプラグアンドプレイデバイスとして初期化されます。

プラグアンドプレイの詳細については、「[プラグアンドプレイ](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)」を参照してください。
