---
title: I/O スタック位置
description: I/O スタック位置
ms.assetid: 62c8ee00-c7cb-4aa1-90ab-b8bedbd818ee
keywords:
- Irp WDK カーネル、i/o スタックの場所
- I/o スタックの場所 (WDK カーネル)
- スタックの場所 (WDK カーネル)
- 階層型ドライバー i/o スタックの場所 WDK カーネル
- Irp WDK カーネル、コンテンツ
- IO_STACK_LOCATION 構造体
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 35a645f822d9259f425ebce38b4bf4486cbf93c1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838649"
---
# <a name="io-stack-locations"></a>I/O スタック位置





I/o マネージャーは、設定されているすべての IRP の i/o スタックの場所を、階層化されたドライバーのチェーンにします。 各 i/o スタックの場所は、 [**IO\_スタック\_の場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)の構造で構成されます。

I/o マネージャーによって、各 IRP の i/o スタックの場所の配列が作成されます。この配列要素は、複数の階層化されたドライバーのチェーン内の各ドライバーに対応しています。 各ドライバーは、パケット内のスタックの場所の1つを所有し、 [**Iogetlocation entiの場所**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)を呼び出して、i/o 操作に関するドライバー固有の情報を取得します。

このようなチェーン内の各ドライバーは、 [**Iogetnextiシャー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetnextirpstacklocation)ドの場所を呼び出し、次に小さいドライバーの i/o スタックの場所を設定します。 上位レベルのドライバーの i/o スタックの場所は、操作に関するコンテキストを格納するためにも使用できます。これにより、ドライバーの[*Iocompletion*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)ルーチンはクリーンアップ操作を実行できます。

階層化された[ドライバーの処理の irp](example-i-o-request---the-details.md#ddk-example-i-o-request---the-details-kg)は、元の irp 内の2つの i/o スタックの場所を示しています。これは、ファイルシステムドライバーと大容量記憶装置ドライバーの2つのドライバーが表示されるためです。 階層化された[ドライバーの処理 irp](example-i-o-request---the-details.md#ddk-example-i-o-request---the-details-kg)で、ドライバーによって割り当てられる irp には、それを作成した FSD のスタック位置がありません。 下位レベルのドライバーに対して Irp を割り当てる上位レベルのドライバーでは、次に低いドライバーのデバイスオブジェクトの**StackSize**値に従って、新しい irp が持つ i/o スタックの場所の数も決定されます。

次の図は、IRP の内容の詳細を示しています。

![irp 内の i/o スタック位置の内容を示す図](images/2irpios.png)

図に示すように、IRP 内の各ドライバー固有の i/o スタックの場所には、次の一般的な情報が含まれています。

- 主要な関数コード (**IRP\_MJ\_* XXX * * *)。ドライバーが実行する基本操作を示します。

- FSDs、高レベルの SCSI ドライバー、およびすべての PnP ドライバーによって処理される主要な関数コードには、ドライバーが実行する必要がある基本的な操作の subcase を示すマイナー関数コード (**IRP\_\_* XXX * * *) があります。

- ドライバーがデータを転送する、またはその元となるバッファーの長さや開始位置など、一連の操作固有の引数。

- 要求された操作のターゲット (物理、論理、または仮想) デバイスを表す、ドライバーによって作成されたデバイスオブジェクトへのポインター

- 開いているファイル、デバイス、ディレクトリ、またはボリュームを表すファイルオブジェクトへのポインター。

  ファイルシステムドライバーは、Irp 内の i/o スタックの場所を介してファイルオブジェクトにアクセスします。 その他のドライバーは、通常、ファイルオブジェクトを無視します。

特定のドライバーが処理する IRP メジャーおよびマイナー関数コードのセットは、デバイスタイプに固有のものにすることができます。 ただし、最下位レベルのドライバーと中間ドライバー (PnP 関数とフィルタードライバーを含む) は、通常、次の基本的な要求セットを処理します。

-   [**IRP\_MJ\_作成**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create) —ターゲットデバイスオブジェクトを開きます。これは、そのオブジェクトが存在し、i/o 操作に使用できることを示します。

-   [**IRP\_MJ\_読み取り**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read) —デバイスからのデータの転送

-   [**IRP\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write) —デバイスへのデータの転送

-   [**IRP\_MJ\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control) -システム定義のデバイスタイプ固有の i/o 制御コード (IOCTL) に従ってデバイスを設定 (またはリセット) します。

-   [**IRP\_MJ\_閉じる**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-close) —ターゲットデバイスオブジェクトを閉じる

-   [**IRP\_MJ\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-pnp) —デバイスでプラグアンドプレイ操作を実行します。 **IRP\_MJ\_pnp**要求は、i/o マネージャーによって pnp マネージャーによって送信されます。

-   [**IRP\_MJ\_電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power) -デバイスで電源操作を実行します。 **IRP\_MJ\_の電源**要求は、i/o マネージャーによって電源マネージャーによって送信されます。

ドライバーが処理するために必要な主要な IRP 関数コードの詳細については、「 [Irp Major 関数コード](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-major-function-codes)」を参照してください。

通常、i/o マネージャーは、大容量記憶装置用の他のドライバーよりもファイルシステムが階層化されているため、2つ以上の i/o スタック位置を持つ Irp を大容量記憶装置デバイスドライバーに送信します。 I/o マネージャーは、1つのスタック位置を持つ Irp を、その上に他のドライバーが含まれていないすべてのドライバーに送信します。

ただし、i/o マネージャーは、システム内の既存のドライバーのチェーンに新しいドライバーを追加するためのサポートを提供します。 たとえば、特定のディスクパーティションのデータをバックアップする中間*ミラードライバー*は、ファイルシステムドライバーや、階層化された[ドライバーの処理 irp](example-i-o-request---the-details.md#ddk-example-i-o-request---the-details-kg)に示されている最下位レベルのドライバーなど、1組のドライバーの間に挿入される場合があります。 この新しいドライバーがデバイススタックに接続すると、i/o マネージャーは、ファイルシステム、ミラー、および下位レベルのドライバーに送信されるすべての Irp 内の i/o スタックの場所の数を調整します。 階層化された[ドライバー内の処理 irp](example-i-o-request---the-details.md#ddk-example-i-o-request---the-details-kg)内のファイルシステムによって割り当てられたすべての irp にも、このような新しいミラードライバー用の別の i/o スタックの場所が含まれています。

既存のチェーンに新しいドライバーを追加する場合は、Irp 内の i/o スタックの場所に対する特定のドライバーのアクセスに特定の制限があることに注意してください。

- 階層化されたドライバーのチェーンにある上位レベルのドライバーは、任意の IRP 内の独自の下位レベルのドライバーの i/o スタックの場所のみに安全にアクセスできます。 このようなドライバーでは、Irp で次の下位レベルのドライバーの i/o スタックの場所を設定する必要があります。 ただし、このような上位レベルのドライバーを設計する場合、ドライバーのすぐ下にある既存のチェーンに新しいドライバーを追加するかどうかを予測することはできません。

  そのため、それ以降に追加されたドライバーでは、次の下位レベルのドライバーが実行したときと同じ IRP メジャー関数コード (**irp\_MJ\_* XXX * * * *) が処理されることを前提としています。

- 階層化されたドライバーのチェーン内の最下位レベルのドライバーは、任意の IRP 内の専用の i/o スタックの場所に安全にアクセスできます。 このようなドライバーを設計する場合、デバイスドライバーの上にある既存のチェーンに新しいドライバーが追加されるタイミング (またはその有無) を予測することはできません。

  最下位レベルのドライバーを設計する際には、ドライバーが独自の i/o スタックの場所で渡される情報を使用して、Irp の処理を継続できると想定しています。これは、特定の IRP の生成元がどのようなものであっても、その上に多くのドライバーが含まれています。

 

 




