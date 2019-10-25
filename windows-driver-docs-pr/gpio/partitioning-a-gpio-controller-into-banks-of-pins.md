---
title: GPIO コントローラーのピンのバンクへのパーティション分割
description: ドライバー開発者は、オプションとして汎用 i/o (GPIO) コントローラーデバイスを2つ以上の GPIO pin のバンクに分割できます。
ms.assetid: D9425459-E052-48D8-A4F3-91387AE7059A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0901bbbc43aa34f99d6bb0d3cb699d548ca0c294
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824921"
---
# <a name="partitioning-a-gpio-controller-into-banks-of-pins"></a>GPIO コントローラーのピンのバンクへのパーティション分割


ドライバー開発者は、オプションとして汎用 i/o (GPIO) コントローラーデバイスを2つ以上の GPIO pin のバンクに分割できます。 たとえば、64 GPIO ピンを持つ GPIO controller デバイスは、GPIO コントローラードライバーによって、それぞれ 32 GPIO ピンを持つ2つの銀行として記述できます。 開発者は、単一のドライバーを使用して、GPIO コントローラーデバイスのすべての銀行を管理できます。このドライバーは通常、デバイス全体を表す1つのデバイスオブジェクトを使用します。 ただし、デバイスの一部またはすべての銀行は、デバイス内の他の銀行とは別に管理できます。

通常、GPIO コントローラードライバーは、次のいずれかの理由で、GPIO コントローラーを2つ以上の銀行にパーティション分割することを選択します。

-   銀行の GPIO ピンの電源状態は、他の銀行のピンとは別に管理できます。
-   GPIO コントローラーの pin の合計数が64を超えています。

GPIO framework 拡張機能 (GpioClx) がサポートする最大バンクサイズは64ピンです。 64個を超える pin を含む GPIO コントローラーデバイスは、ドライバーによって2つ以上のバンクにパーティション分割される必要があります。各バンクには64の pin が含まれていません。

GPIO コントローラーが銀行にどのようにパーティション分割されているかを判断するために、GpioClx は[*クライアント\_Querycontroller Basicinformation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)イベントコールバック関数を呼び出します。 この関数は、GPIO コントローラードライバーによって実装され、GPIO コントローラーの属性と機能を記述する[**クライアント\_コントローラー\_基本的な\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_client_controller_basic_information)の構造を提供します。 この構造体の2つのメンバー ( **Totalpinと Numberofpinsperbank**) によって、GPIO コントローラーのピンがどのように銀行に分割されるかを指定します。 **Totalpins**は、GPIO コントローラー内のピンの合計数を指定し、 **numberofpinsperbank**は銀行あたりの pin の数を指定します。 N がコントローラー内の銀行数である場合、銀行には 0 ~ N-1 の番号が付けられます。 最後の銀行 (銀行番号 N-1) を除くすべての値には、 **Numberofpinsperbank**メンバーで指定された pin の数が含まれている必要があります。 最後の銀行は、1つの**Numberofpinsperbank**から任意の数のピンを持つことができます。

GpioClx は、 **Totalpins**と**numberofpinsperbank**のメンバーの値から、GPIO コントローラー内の銀行の合計数を決定します。 GpioClx では、次の整数式を使用して、バンクの合計数を計算します。

( **Totalpin + numberofpinsperbank** – 1)、**一部の GPIO コントローラーデバイスでは**、デバイスのピンのバンクをオンにするか、同じデバイス内の他の銀行とは無関係に低電力状態に切り替えることができます。 このため、特定の銀行がアイドル状態になると、この銀行を省電力状態に切り替えて電力消費を減らすことができます。 このようなデバイスに対応するために、GpioClx は[コンポーネントレベルの電源管理](https://docs.microsoft.com/windows-hardware/drivers/kernel/component-level-power-management)をサポートしています。 GpioClx では、2つのコンポーネントレベルの電源状態 (F0) と F1 (低電力またはオフ) が定義されています。

GPIO ピンのバンクがコンポーネントレベルの電源管理をサポートしているかどうかを判断するために、GpioClx は[*クライアント\_Querysetコントローラー情報*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_set_controller_information)イベントコールバック関数を呼び出します。 この関数の*InputBuffer*パラメーターは、[**クライアント\_コントローラー\_クエリ\_\_情報\_入力**](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_client_controller_query_set_information_input)構造を設定するためのポインターです。 電源管理情報を要求するために、呼び出し元は、この構造体の**RequestType**メンバーを**QueryBankPowerInformation**に設定します。

GPIO bank でコンポーネントレベルの電源管理がサポートされている場合、GpioClx を使用すると、バンクがアイドル状態のときに F1 電源状態に移行できます。 銀行が F1 状態になる前に、GpioClx は[*クライアント\_SaveBankHardwareContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_save_bank_hardware_context)イベントコールバック関数を呼び出して、バンクのハードウェアコンテキスト (主、レジスタコンテンツ) を保存するようにドライバーに指示します。 その後、銀行が F0 状態になると、GpioClx は[*クライアント\_RestoreBankHardwareContext*](https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_restore_bank_hardware_context)イベントコールバック関数を呼び出して、以前に保存されたハードウェアコンテキストを復元するようにドライバーに指示します。

 

 




