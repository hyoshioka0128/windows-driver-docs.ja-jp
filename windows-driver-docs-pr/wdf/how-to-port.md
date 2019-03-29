---
title: 移植の手順
description: 移植の手順
ms.assetid: D8B7E534-7CFC-45EC-93E9-4B046598D82B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9600d83828d16d36e3773a7e4e0d5120c5d531f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577727"
---
# <a name="steps-in-porting"></a>移植の手順


によって、ドライバーの種類の移植は、次の手順を実行するがあります。

1.  [DriverEntry ルーチンをポート](porting-driver-entry.md)WDFDRIVER オブジェクトを作成するコードを追加します。
2.  [AddDevice ルーチンをポート](porting-adddevice-to-evtdriverdeviceadd.md)を[ *EvtDriverDeviceAdd* ](https://msdn.microsoft.com/library/windows/hardware/ff541693)コールバック、WDFDEVICE オブジェクトを作成するコードを追加します。
3.  サポートを追加[割り込み](porting-interrupt-functionality.md)ドライバーは、割り込み処理をサポートしている場合。

この時点で実行できます、残りの手順増分し、任意の順序でのテストと追加するたびにデバッグします。 たとえば、I/O キューを実装して、プラグ アンド プレイを電源管理フレームワークの既定値を使用して開始できます。 基本的な I/O のサポートをデバッグした後より広範なプラグ アンド プレイと電源管理の要求のサポートを追加できます。 残りの手順は次のとおりです。

-   サポートを追加[プラグ アンド プレイし、電源管理](porting-pnp-and-power-management-functionality.md)します。
-   追加[I/O サポート](porting-i-o-handling.md)します。
-   サポートを追加[DMA](porting-dma.md)デバイス DMA を実行する場合は、<sup> 。†</sup>
-   [WMI コードを移植](porting-wmi-code.md).<sup>†</sup>
-   コードを移植[KMDF ドライバーの代わりに、framework が処理しない要求を処理する](requests-that-kmdf-does-not-support.md).<sup>†</sup>
-   [改訂、INF](installation-procedure.md)ドライバーをインストールします。

† この機能は、カーネル モード ドライバー フレームワーク (KMDF) ドライバーをできるだけです。

ただし、前述のように、すべての種類のドライバー (PDO、FDO、およびフィルター操作を行います) にこのセクションの情報が適用されます。 ただし、KMDF にバス ドライバー (PDO) を移植する場合は、デバイスの列挙型のコードを移植する必要がもあります。 デバイスを列挙する方法の詳細については、次を参照してください。[バス上のデバイスを列挙する](enumerating-the-devices-on-a-bus.md)します。

さまざまな WDF オブジェクト、メソッド、およびイベントのコールバック関数は、共通の WDM オブジェクトおよび関数にマップする方法を説明するリファレンス情報は、次を参照してください。 [KMDF の概要と対応する WDM](summary-of-kmdf-and-wdm-equivalents.md)します。

 

 





