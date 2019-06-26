---
title: GPIO コントローラーのピンのバンクへのパーティション分割
description: ドライバー開発者向けオプション、GPIO ピンの 2 つ以上の銀行に汎用入出力 (GPIO) コント ローラーのデバイス パーティションとしてことができます。
ms.assetid: D9425459-E052-48D8-A4F3-91387AE7059A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a53a07d0450326ffdb2fda08c6eaeeeeef73fc89
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363569"
---
# <a name="partitioning-a-gpio-controller-into-banks-of-pins"></a>GPIO コントローラーのピンのバンクへのパーティション分割


ドライバー開発者向けオプション、GPIO ピンの 2 つ以上の銀行に汎用入出力 (GPIO) コント ローラーのデバイス パーティションとしてことができます。 たとえば、32 の GPIO ピンを持つ 2 つの銀行としてするには、GPIO コント ローラー ドライバーが 64 の GPIO ピン GPIO コント ローラー デバイスを説明します。 開発者は、GPIO コント ローラー デバイスでは、銀行のすべてを管理する 1 つのドライバーを提供でき、通常、このドライバーはデバイス全体を表す 1 つのデバイス オブジェクトを使用します。 ただし、一部またはすべてのデバイスで銀行は、デバイスで、その他の銀行とは無関係に管理できます。

通常、2 つ以上の銀行に GPIO コント ローラーを次の理由の 1 つのパーティションに GPIO コント ローラーのドライバーが選択されます。

-   銀行の GPIO ピンの電源の状態は、他の銀行のピンとは無関係に管理できます。
-   GPIO コント ローラーのピンの合計数は 64 を超えています。

GPIO フレームワーク拡張機能 (GpioClx) をサポートする銀行の最大サイズは、64 ピンです。 含む 64 を超えるピン GPIO コント ローラー デバイスは、64 個のピンを含む 2 つ以上の銀行にドライバーによってパーティション分割する必要があります。

GpioClx を呼び出す銀行に GPIO コント ローラーを分割する方法を決定する、 [*クライアント\_QueryControllerBasicInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)イベント コールバック関数。 この関数は、GPIO コント ローラーのドライバーによって実装される、提供、 [**クライアント\_コント ローラー\_BASIC\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/ns-gpioclx-_client_controller_basic_information)記述する構造体属性と GPIO コント ローラーの機能です。 この構造体の 2 つのメンバー **TotalPins**と**NumberOfPinsPerBank**銀行に GPIO コント ローラーのピンがパーティション分割方法を指定します。 **TotalPins** GPIO コント ローラーのピンの合計数を指定し、 **NumberOfPinsPerBank**銀行あたりピンの数を指定します。 コント ローラーで、銀行の数を N には、N-1 を 0 から、銀行の番号します。 銀行 (つまりは銀行番号 N-1) 最後以外のすべてで指定されたピンの数を含める必要があります、 **NumberOfPinsPerBank**メンバー。 最後の銀行を 1 つからピンの任意の数を持つことができます**NumberOfPinsPerBank**します。

GpioClx の値から、GPIO コント ローラーで、銀行の合計数を決定する、 **TotalPins**と**NumberOfPinsPerBank**メンバー。 GpioClx では、次のような整数式を使用して、銀行の合計数を計算します。

(**TotalPins** + **NumberOfPinsPerBank** – 1)/ **NumberOfPinsPerBank** GPIO コント ローラーの一部のデバイスでのデバイスで pin の銀行をオンにできますか同じデバイスで、その他の銀行とは無関係に低電力状態に切り替えられます。 したがって、特定の銀行がアイドル状態のときは、この銀行は電力消費量を削減する低電力状態に切り替えることができます。 このようなデバイスに合わせて、GpioClx サポートしている[コンポーネント レベルの電源管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/component-level-power-management)します。 GpioClx (完全に) F0、f1 キーを 2 つのコンポーネント レベルの電源状態を定義します (低電力またはオフ)。

GPIO ピンの銀行がコンポーネント レベルの電源管理をサポートするかどうかを判断する GpioClx を呼び出し、 [*クライアント\_QuerySetControllerInformation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_query_set_controller_information)イベント コールバック関数。 *InputBuffer*この関数のパラメーターはへのポインターを[**クライアント\_コント ローラー\_クエリ\_設定\_情報\_入力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/ns-gpioclx-_client_controller_query_set_information_input)構造体。 電源管理情報、呼び出し元のセットを**RequestType**をこの構造体のメンバー **QueryBankPowerInformation**します。

GpioClx に GPIO 銀行では、コンポーネント レベルの電源管理をサポートする銀行がアイドル状態のときに F1 電源の状態への移行を使用できます。 GpioClx を呼び出す前に、銀行の F1 が状態、 [*クライアント\_SaveBankHardwareContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_save_bank_hardware_context)ハードウェア コンテキスト (主に、登録を保存するドライバーを通知するイベントのコールバック関数内容)、銀行の。 その後、銀行 F0 状態を入力すると、GpioClx 呼び出し、 [*クライアント\_RestoreBankHardwareContext* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/gpioclx/nc-gpioclx-gpio_client_restore_bank_hardware_context)以前に保存したハードウェアを復元するドライバーを通知するイベントのコールバック関数コンテキスト。

 

 




