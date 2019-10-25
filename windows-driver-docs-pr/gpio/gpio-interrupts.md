---
title: GPIO 割り込み
description: 一部の汎用 I/O (GPIO) コントローラー デバイスでは、割り込み要求の入力として機能するよう GPIO ピンを構成できます。
ms.assetid: 0F56AD4C-E0BF-49F1-AB67-0107D08DEF9F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 713eb6162dde55c265aacb868c0a7e11c2c3b97a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824970"
---
# <a name="gpio-interrupts"></a>GPIO 割り込み


一部の汎用 I/O (GPIO) コントローラー デバイスでは、割り込み要求の入力として機能するよう GPIO ピンを構成できます。 これらの割り込み要求の入力は、GPIO ピンに物理的に接続されている周辺機器によって駆動されます。 これらの GPIO コントローラー用のドライバーにより、個々の GPIO ピンで割り込み要求の有効化、無効化、マスク、マスク解除、およびクリアを実行できます。

GPIO 割り込みのサポートはオプションです。 Gpio framework 拡張機能 (GpioClx) では、gpio 割り込みをサポートするために GPIO コントローラーは必要ありません。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/primary-and-secondary-interrupts" data-raw-source="[Primary and Secondary Interrupts](https://docs.microsoft.com/windows-hardware/drivers/gpio/primary-and-secondary-interrupts)">プライマリとセカンダリの割り込み</a></p></td>
<td><p>GPIO 割り込み処理は本質的に2段階のプロセスです。 汎用 i/o (GPIO) コントローラーからの割り込みにより、GPIO framework extension (GpioClx) interrupt service ルーチン (ISR) が実行されるようになりましたが、<em>プライマリ割り込み</em>と呼ばれています。 この ISR は、割り込みを行う GPIO pin をグローバルシステム割り込み (GSI) にマップし、この GSI をハードウェアアブストラクションレイヤー (HAL) に渡します。 HAL は、この GSI を介して、GPIO ピンに論理的に接続されている2つ目の ISR を実行するための2次<em>割り込み</em>を生成します。 このプロセスは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-driver-support-overview#gpio-block-diagram" data-raw-source="[GPIO Driver Support Overview](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-driver-support-overview#gpio-block-diagram)">「GPIO ドライバーサポートの概要</a>」の図に示されています。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-based-interrupt-resources" data-raw-source="[GPIO-Based Interrupt Resources](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-based-interrupt-resources)">GPIO ベースの割り込みリソース</a></p></td>
<td><p>汎用 i/o (GPIO) ピンに割り込みを送信する周辺機器のドライバーは、抽象的な Windows 割り込みリソースとして GPIO 割り込みを取得します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers" data-raw-source="[Kernel-mode driver framework](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)">カーネルモードドライバーフレームワーク</a>(kmdf) ドライバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)"><em>Evtdevicepreparehardware</em></a>イベントコールバック関数を介してこれらのリソースを受け取ります。 </p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/passive-level-isrs" data-raw-source="[Passive-Level ISRs](https://docs.microsoft.com/windows-hardware/drivers/gpio/passive-level-isrs)">パッシブレベルの Isr</a></p></td>
<td><p>Windows 8 以降では、カーネルモードドライバーフレームワーク (KMDF) とユーザーモードドライバーフレームワーク (UMDF) ドライバーを使用して、パッシブレベルで実行するように割り込みサービスルーチン (Isr) を登録することができます。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/interrupt-related-callbacks" data-raw-source="[Interrupt-Related Callbacks](https://docs.microsoft.com/windows-hardware/drivers/gpio/interrupt-related-callbacks)">割り込み関連のコールバック</a></p></td>
<td><p>オプションとして、汎用 i/o (GPIO) コントローラーのドライバーは、GPIO 割り込みをサポートすることができます。 Gpio 割り込みをサポートするために、GPIO コントローラードライバーは、これらの割り込みを管理するためのコールバック関数のセットを実装します。 ドライバーには、そのドライバーが GPIO framework extension (GpioClx) のクライアントとして登録するときに提供される、登録パケット内のこれらのコールバック関数へのポインターが含まれています。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/interrupt-synchronization-for-gpio-controller-drivers" data-raw-source="[Interrupt Synchronization for GPIO Controller Drivers](https://docs.microsoft.com/windows-hardware/drivers/gpio/interrupt-synchronization-for-gpio-controller-drivers)">GPIO コントローラードライバーの割り込み同期</a></p></td>
<td><p>GPIO controller ドライバーは、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_acquireinterruptlock" data-raw-source="[&lt;strong&gt;GPIO_CLX_AcquireInterruptLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_acquireinterruptlock)"><strong>GPIO_CLX_AcquireInterruptLock</strong></a>メソッドと<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_releaseinterruptlock" data-raw-source="[&lt;strong&gt;GPIO_CLX_ReleaseInterruptLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_releaseinterruptlock)"><strong>GPIO_CLX_ReleaseInterruptLock</strong></a>メソッドを呼び出して、gpio フレームワーク拡張機能 (gpioclx) によって内部的に実装されている割り込みロックを取得し、解放します。 IRQL = PASSIVE_LEVEL で実行されるドライバーコードは、これらのメソッドを呼び出して、GpioClx の割り込みサービスルーチン (ISR) に同期できます。 GpioClx は、GPIO コントローラー内の各ピンのバンクに個別の割り込みロックを専用にします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/enabling-and-disabling-shared-gpio-interrupts" data-raw-source="[Enabling and Disabling Shared GPIO Interrupts](https://docs.microsoft.com/windows-hardware/drivers/gpio/enabling-and-disabling-shared-gpio-interrupts)">共有 GPIO 割り込みの有効化と無効化</a></p></td>
<td><p>場合によっては、2つ以上の周辺機器からの割り込み要求行が、同じ物理汎用 i/o (GPIO) ピンに接続することがあります。 共有割り込み線の GPIO ピンは、通常、レベルでトリガーされる割り込み用に構成されます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-interrupt-masks" data-raw-source="[GPIO Interrupt Masks](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-interrupt-masks)">GPIO 割り込みマスク</a></p></td>
<td><p>割り込み入力として構成されている汎用 i/o (GPIO) の pin は、有効または無効にするだけでなく、マスクとマスク解除が可能です。</p></td>
</tr>
</tbody>
</table>

 

 

 




