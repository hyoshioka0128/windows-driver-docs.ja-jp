---
title: I/O スタックの場所
description: I/O スタックの場所
ms.assetid: 62c8ee00-c7cb-4aa1-90ab-b8bedbd818ee
keywords:
- Irp WDK カーネルでは、I/O スタックの場所
- I/O スタックの場所の WDK カーネル
- スタックの場所の WDK カーネル
- ドライバー I/O スタックの場所の WDK カーネルを階層化
- Irp WDK カーネル、内容
- IO_STACK_LOCATION 構造体
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae09b1cddf0813a586a499b5f2c360011eeffc27
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553682"
---
# <a name="io-stack-locations"></a>I/O スタックの場所





I/O マネージャーを設定するすべての IRP の複数層のドライバーのチェーン内には、各ドライバー、I/O スタックの場所を示します。 各 I/O スタックの場所から成る、 [ **IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)構造体。

I/O マネージャーは、複数層のドライバーのチェーンでは、各ドライバーに対応する配列要素を使用して、各 IRP の I/O スタックの場所の配列を作成します。 各ドライバーでは、パケットと呼び出しスタックの場所の 1 つ所有している[ **IoGetCurrentIrpStackLocation** ](https://msdn.microsoft.com/library/windows/hardware/ff549174) I/O 操作に関するドライバー固有の情報を取得します。

このようなチェーン内の各ドライバーが通話を担当[ **IoGetNextIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549266)次の下位ドライバーの I/O スタックの場所を設定します。 I/O スタックの上位レベルのドライバーの場所が操作に関するコンテキストを格納することもできるように、ドライバーの[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチンは、そのクリーンアップ操作を実行できます。

[ドライバーでの処理の Irp](example-i-o-request---the-details.md#ddk-example-i-o-request---the-details-kg)図は、2 つのドライバー、ファイル システム ドライバーと大容量記憶装置ドライバーが表示されるため、元の IRP で I/O スタックの 2 つの場所を示します。 ドライバーに割り当てられた Irp、[ドライバーでの処理の Irp](example-i-o-request---the-details.md#ddk-example-i-o-request---the-details-kg)図では、作成した FSD は、スタックの場所はありません。 Irp を下位レベルのドライバーによって割り当てられる任意の高度なドライバーは新しい Irp する必要がありますが、I/O スタック場所の数も決定に従って、 **StackSize**次の下位ドライバーのデバイス オブジェクトの値。

次の図は、さらに詳しく IRP の内容を示しています。

![irp の i/o スタックの場所の内容を示す図](images/2irpios.png)

図に示すように各 IRP のドライバー固有の I/O スタック場所には、次の一般的な情報が含まれています。

- 主要な関数のコード (**IRP\_MJ\_* XXX * * *) を示す、基本的な操作、ドライバーを実行する必要があります

- Fsd に対して表示されるより高度な SCSI ドライバー、およびすべての PnP ドライバーによって処理される一部の主要な関数コードは、マイナー機能コード (**IRP\_MN\_* XXX * * *)、基本的な操作のどのサブケース ドライバーを示すを実行します。

- 開始場所、ドライバーがデータを転送先または元のバッファーの長さなどの操作に固有の引数のセット

- 要求された操作のターゲット (物理、論理、または仮想) デバイスを表す、デバイスのドライバーが作成したオブジェクトへのポインター

- ファイルを開く、デバイス、ディレクトリ、またはボリュームを表すファイル オブジェクトへのポインター

  ファイル システム ドライバーは Irp では、I/O スタックの場所からファイル オブジェクトにアクセスします。 その他のドライバーは、通常は、ファイル オブジェクトを無視します。

特定のドライバーを処理する IRP のメジャーおよびマイナーの関数コードのセットには、デバイス固有の種類を指定できます。 ただし、最下位レベルおよび中間のドライバー (ドライバーの PnP 関数とフィルターを含む) は、通常、次の一連の基本的な要求を処理します。

-   [**IRP\_MJ\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff550729) -あることを示す存在し、使用可能な I/O 操作のターゲット デバイス オブジェクトを開く

-   [**IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff550794) : デバイスからのデータ転送

-   [**IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff550819) — データをデバイスに転送します。

-   [**IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744) などを設定する (またはリセット)、デバイス、システム定義のデバイス固有の種類 I/O 制御コード (IOCTL) に従って

-   [**IRP\_MJ\_閉じます**](https://msdn.microsoft.com/library/windows/hardware/ff550720) — ターゲットのデバイス オブジェクトを閉じる

-   [**IRP\_MJ\_PNP**](https://msdn.microsoft.com/library/windows/hardware/ff550772) -デバイスのプラグ アンド プレイ操作を実行します。 **IRP\_MJ\_PNP** I/O マネージャーを通じて PnP マネージャーによって要求が送信されます。

-   [**IRP\_MJ\_POWER**](https://msdn.microsoft.com/library/windows/hardware/ff550784) -デバイスの電源操作を実行します。 **IRP\_MJ\_POWER** I/O マネージャーを通じて電源マネージャー要求を送信します。

ドライバーが処理するために必要な主要な IRP の関数コードの詳細については、[IRP の主な機能コード](https://msdn.microsoft.com/library/windows/hardware/ff550710)を参照してください。

一般に、I/O マネージャーは、ファイル システムが他のドライバーの大容量記憶装置上に構築されたために、少なくとも 2 つの大容量記憶装置デバイス ドライバーへの I/O スタックの場所で Irp を送信します。 I/O マネージャーは、Irp をその上層の他のドライバーがない任意のドライバーを 1 つのスタックの場所に送信します。

ただし、I/O マネージャーは、既存のドライバーのすべてのチェーンに、システムで新しいドライバーを追加するためのサポートを提供します。 たとえば、中間*ミラー ドライバー*対ドライバー、ファイル システム ドライバーとに示すように最下位レベルのドライバーなどの特定のディスク パーティションにデータ バックアップを挿入する可能性があります、[で Irp の処理ドライバーを階層化](example-i-o-request---the-details.md#ddk-example-i-o-request---the-details-kg)図。 この新しいドライバーは、デバイス スタックに自体をアタッチ、I/O マネージャーはファイル システム、ミラー、および最下位レベルのドライバーに送信するすべての Irp で I/O スタックの場所の数を調整します。 すべて IRP をファイル システムで、[ドライバーでの処理の Irp](example-i-o-request---the-details.md#ddk-example-i-o-request---the-details-kg)割り当ての図は、このような新しいミラー ドライバーのもう 1 つの I/O スタックの場所にも含まれます。

既存のチェーンに新しいドライバーを追加するためには、このサポートが Irp では、I/O スタックの場所へのアクセスを特定のドライバーに対して特定の制限を意味することに注意してください。

- 複数層のドライバーのチェーンの上位レベルのドライバーにのみアクセスできる安全にその独自と任意の IRP で、[次へ] の下位レベルのドライバーの I/O スタックの場所。 このようなドライバーは、Irp で次の下位レベルのドライバーを I/O スタックの場所を設定する必要があります。 ただし、このようなより高度なドライバーを設計するときは、ときに (またはかどうか)、既存のチェーンには、ドライバーのすぐ下に新しいドライバーが追加されます予測できません。

  そのため、前提にするべきこと、後で追加したドライバーは IRP の主な機能と同じコードを処理する (**IRP\_MJ\_* XXX * * *) 変位させられた下位レベルの次のドライバーと同様です。

- 複数層のドライバーのチェーンの最下位レベルのドライバーでは、のみ独自 I/O スタックの場所の IRP で安全にアクセスできます。 このようなドライバーを設計するときは、ときに (またはかどうか)、既存のチェーンには、デバイス ドライバーの上に新しいドライバーが追加されますを予測できません。

  最下位レベルのドライバーを設計すると想定しています、ドライバーは Irp 独自 I/O スタックの場所に、どのような特定の IRP の元のソースに渡される情報を使用してプロセスを続けることができますが、多くのドライバーは、上に階層化されているとします。

 

 




