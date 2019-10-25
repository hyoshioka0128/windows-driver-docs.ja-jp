---
title: 操作領域ハンドラーを登録/登録解除する
description: 操作領域ハンドラーを登録/登録解除する
ms.assetid: de40488d-7935-431c-b1f4-87f8aff1125b
keywords:
- ACPI デバイス WDK、操作リージョン
- 操作リージョン WDK ACPI
- 関数ドライバー WDK ACPI、操作リージョン
- WDM 関数ドライバー WDK ACPI、操作リージョン
- 登録 (操作領域ハンドラーを)
- 操作領域ハンドラーの登録解除
ms.date: 01/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: 781fad9aa446b1a6cbb5e2b42d8e2726686139db
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831470"
---
# <a name="registering-and-deregistering-an-operation-region-handler"></a>操作領域ハンドラーを登録/登録解除する


ACPI デバイス関数ドライバーは、 [**Registeropregionhandler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/oprghdlr/nf-oprghdlr-registeropregionhandler)を呼び出し、次の情報を提供することによって、操作領域ハンドラーを登録します。

-   操作領域を定義する ACPI デバイスを表す物理デバイスオブジェクト (PDO)。

-   アクセスの種類。*未加工*または*加工できます。*

    詳細については、「[操作領域へのアクセス](accessing-an-operation-region.md)」を参照してください。

-   領域の領域の種類。

    ベンダーは、0x80 から0xFF までのベンダー定義の値を指定する必要があります。 (0x80 未満の値は ACPI 仕様によって定義され、内部使用のために予約されています)。

-   ドライバーの操作領域ハンドラーへのポインター。

    ACPI ドライバーは、ドライバーの操作領域ハンドラーを呼び出すことによって、操作領域にアクセスします。

-   *操作領域コンテキスト*へのポインター。

    操作領域コンテキストはデバイス固有であり、関数ドライバーによってのみ使用されます。 ACPI ドライバーは、操作領域ハンドラーを呼び出すと、操作領域コンテキストをハンドラーに渡します。 通常は、機能デバイスオブジェクト (FDO) のデバイス拡張機能です。

**Registeropregionhandler**は、ドライバーがハンドラーを解除したときにのみ、関数ドライバーが操作領域ハンドラーを一意に識別するために使用する操作領域オブジェクトを返します。

通常、ドライバーは、\_IRP に応答して FDO を開始した後に、ドライバーのプラグアンドプレイディスパッチルーチンに操作領域ハンドラーを登録します。これにより、 [ **\_デバイス要求の開始\_開始**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)されます。 ドライバーは、ハンドラーの操作領域コンテキストを割り当てると、ハンドラーを登録する必要があります。 ドライバーがベンダー定義のデバイスインターフェイスを作成する場合、ドライバーは、ハンドラーを登録した後にデバイスインターフェイスを有効にする必要があります。

ACPI デバイス関数ドライバーは、 [**DeRegisterOpRegionHandler**](https://docs.microsoft.com/windows-hardware/drivers/ddi/oprghdlr/nf-oprghdlr-deregisteropregionhandler)を呼び出し、次の情報を指定することによって、操作領域ハンドラーを解除します。

-   操作領域を定義する ACPI デバイスを表す PDO。

-   ドライバーが操作領域ハンドラーを登録したときに ACPI ドライバーによって返された操作領域オブジェクト。 このオブジェクトは、操作領域ハンドラーを一意に識別します。

通常、ドライバーは、 [ **\_\_\_IRP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)に応答して FDO を停止する前に、ドライバーのプラグアンドプレイディスパッチルーチン内の操作領域ハンドラーを解除します。 ハンドラーの操作領域コンテキストを解放する前に、ドライバーがハンドラーを登録解除する必要があります。 ドライバーがベンダー定義のデバイスインターフェイスを作成する場合、ドライバーは、ハンドラーを解除する前にデバイスインターフェイスを無効にする必要があります。

 




