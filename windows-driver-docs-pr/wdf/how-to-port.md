---
title: 移植の手順
description: 移植の手順
ms.assetid: D8B7E534-7CFC-45EC-93E9-4B046598D82B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8912af4f0d2ee87b7460ec0f582cc68486b3857f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845213"
---
# <a name="steps-in-porting"></a>移植の手順


ドライバーの種類に応じて、移植には次の手順を実行する必要があります。

1.  [DriverEntry ルーチンを移植](porting-driver-entry.md)し、WDFDRIVER オブジェクトを作成するためのコードを追加します。
2.  [AddDevice ルーチン](porting-adddevice-to-evtdriverdeviceadd.md)を[*Evtdriverdeviceadd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)コールバックに移植し、wdfdevice オブジェクトを作成するためのコードを追加します。
3.  ドライバーで割り込み処理がサポートされている場合は、[割り込み](porting-interrupt-functionality.md)のサポートを追加します。

この時点で、残りのステップを段階的に実行できます。また、各追加後に、任意の順序、テスト、デバッグを行うことができます。 たとえば、まず、i/o キューを実装し、プラグアンドプレイと電源管理のフレームワークの既定値を使用します。 基本的な i/o サポートをデバッグした後、さらに多くのプラグアンドプレイおよび電源管理要求のサポートを追加できます。 残りの手順は次のとおりです。

-   [プラグアンドプレイと電源管理](porting-pnp-and-power-management-functionality.md)のサポートを追加します。
-   [I/o サポート](porting-i-o-handling.md)を追加します。
-   デバイスが DMA を実行する場合は、 [dma](porting-dma.md)のサポートを追加します。<sup>†</sup>
-   [ポート WMI コード](porting-wmi-code.md)。<sup>†</sup>
-   [KMDF ドライバーの代わりにフレームワークが処理しない要求を処理](requests-that-kmdf-does-not-support.md)するためのポートコード。<sup>†</sup>
-   ドライバーをインストールする[INF を修正](installation-procedure.md)します。

†この機能は、カーネルモードドライバーフレームワーク (KMDF) ドライバーでのみ使用できます。

ただし、前述のように、このセクションの情報はすべての種類のドライバー (PDO、FDO、および filter DO) に適用されます。 ただし、バスドライバー (PDO) を KMDF に移植する場合は、デバイスの列挙コードも移植する必要があります。 デバイスの列挙の詳細については、「[バス上のデバイスの列挙](enumerating-the-devices-on-a-bus.md)」を参照してください。

さまざまな WDF オブジェクト、メソッド、およびイベントコールバック関数を共通の WDM オブジェクトおよび関数にマップする方法については、「 [KMDF と wdm の概要](summary-of-kmdf-and-wdm-equivalents.md)」を参照してください。

 

 





