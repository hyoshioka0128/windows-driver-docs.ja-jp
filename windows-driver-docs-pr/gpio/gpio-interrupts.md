---
title: GPIO 割り込み
description: 一部の汎用 I/O (GPIO) コントローラー デバイスでは、割り込み要求の入力として機能するよう GPIO ピンを構成できます。
ms.assetid: 0F56AD4C-E0BF-49F1-AB67-0107D08DEF9F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c941b80ed808b022524dbe5c0fff36a88411e3e8
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393112"
---
# <a name="gpio-interrupts"></a>GPIO 割り込み


一部の汎用 I/O (GPIO) コントローラー デバイスでは、割り込み要求の入力として機能するよう GPIO ピンを構成できます。 これらの割り込み要求の入力は、GPIO ピンに物理的に接続されている周辺機器によって駆動されます。 これらの GPIO コントローラー用のドライバーにより、個々の GPIO ピンで割り込み要求の有効化、無効化、マスク、マスク解除、およびクリアを実行できます。

GPIO 割り込みのサポートは、省略可能です。 GPIO フレームワーク拡張機能 (GpioClx) では、GPIO 割り込みをサポートするために GPIO コント ローラーは必要ありません。

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
<td><p>GPIO 割り込み処理が 2 段階のプロセスでは本質的にします。 GPIO フレームワーク拡張機能 (GpioClx) 割り込みサービス ルーチン (ISR) を実行するとの汎用的な I/O (GPIO) コントローラからの割り込みと呼ばれる、<em>プライマリ割り込み</em>します。 この ISR では、グローバル システムの割り込み (GSI) に割り込む GPIO ピンをマップし、ハードウェア アブストラクション レイヤー (HAL) にこの GSI を渡します。 HAL を生成、<em>セカンダリ割り込み</em>を通じてこの GSI GPIO ピンに論理的に接続されている 2 つ目の ISR を実行します。 このプロセスはダイアグラムに示した<a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-driver-support-overview#gpio-block-diagram" data-raw-source="[GPIO Driver Support Overview](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-driver-support-overview#gpio-block-diagram)">GPIO ドライバー サポートの概要</a>します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-based-interrupt-resources" data-raw-source="[GPIO-Based Interrupt Resources](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-based-interrupt-resources)">割り込みの GPIO ベースのリソース</a></p></td>
<td><p>割り込みを汎用入出力 (GPIO) ピンとして抽象 Windows GPIO 割り込みを取得する送信周辺機器のデバイス用のドライバーでは、リソースを中断します。 <a href="https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers" data-raw-source="[Kernel-mode driver framework](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)">カーネル モード ドライバー フレームワーク</a>(KMDF) ドライバーを通じてこれらのリソースが表示される、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware" data-raw-source="[&lt;em&gt;EvtDevicePrepareHardware&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)"> <em>EvtDevicePrepareHardware</em> </a>イベント コールバック関数。 </p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/passive-level-isrs" data-raw-source="[Passive-Level ISRs](https://docs.microsoft.com/windows-hardware/drivers/gpio/passive-level-isrs)">パッシブ レベル isr を特定します。</a></p></td>
<td><p>Windows 8、カーネル モード ドライバー フレームワーク (KMDF) とユーザー モード ドライバー フレームワーク (UMDF) ドライバーを開始できます、オプションとして、登録、割り込みサービス ルーチン (Isr) パッシブ レベルで実行します。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/interrupt-related-callbacks" data-raw-source="[Interrupt-Related Callbacks](https://docs.microsoft.com/windows-hardware/drivers/gpio/interrupt-related-callbacks)">割り込みに関連するコールバック</a></p></td>
<td><p>オプションとして、汎用入出力 (GPIO) コント ローラーのドライバーは、GPIO 割り込みのサポートを提供できます。 GPIO 割り込みをサポートするためには、GPIO コント ローラーのドライバーは、これらの割り込みを管理するコールバック関数のセットを実装します。 ドライバーには、GPIO フレームワークの拡張機能 (GpioClx) のクライアントとして自身を登録するときに、ドライバーが提供する登録パケット内のこれらのコールバック関数へのポインターが含まれています。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/interrupt-synchronization-for-gpio-controller-drivers" data-raw-source="[Interrupt Synchronization for GPIO Controller Drivers](https://docs.microsoft.com/windows-hardware/drivers/gpio/interrupt-synchronization-for-gpio-controller-drivers)">GPIO コント ローラーのドライバーの同期を中断します。</a></p></td>
<td><p>GPIO コント ローラー ドライバーが呼び出すことができます、 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_acquireinterruptlock" data-raw-source="[&lt;strong&gt;GPIO_CLX_AcquireInterruptLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_acquireinterruptlock)"> <strong>GPIO_CLX_AcquireInterruptLock</strong> </a>と<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_releaseinterruptlock" data-raw-source="[&lt;strong&gt;GPIO_CLX_ReleaseInterruptLock&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nf-gpioclx-gpio_clx_releaseinterruptlock)"> <strong>GPIO_CLX_ReleaseInterruptLock</strong> </a>メソッド取得および GPIO フレームワーク拡張機能 (GpioClx) によって内部的に実装される割り込みロックを解放します。 IRQL で実行されるドライバー コード = PASSIVE_LEVEL GpioClx で割り込みサービス ルーチン (ISR) に同期するこれらのメソッドを呼び出すことができます。 GpioClx 専用に GPIO コント ローラーのピンの各銀行に別の割り込みロックします。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/enabling-and-disabling-shared-gpio-interrupts" data-raw-source="[Enabling and Disabling Shared GPIO Interrupts](https://docs.microsoft.com/windows-hardware/drivers/gpio/enabling-and-disabling-shared-gpio-interrupts)">共有 GPIO 割り込みを有効化と無効化</a></p></td>
<td><p>場合によっては、2 つ以上の周辺機器からの割り込み要求行が同じ物理汎用入出力 (GPIO) ピンに接続します。 共有の割り込みの行の GPIO ピンは通常、割り込みのトリガーされたレベルの構成します。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-interrupt-masks" data-raw-source="[GPIO Interrupt Masks](https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-interrupt-masks)">GPIO 割り込みマスク</a></p></td>
<td><p>割り込み入力はマスクやほかにマスク解除が有効と無効にできるように構成されている汎用の I/O (GPIO) ピンです。</p></td>
</tr>
</tbody>
</table>

 

 

 




