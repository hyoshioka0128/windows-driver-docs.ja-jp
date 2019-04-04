---
title: バッファー付き I/O の使用
description: バッファー付き I/O の使用
ms.assetid: 69291156-babb-465a-9e80-1766f075768b
keywords:
- バッファー内の I/O の WDK カーネル
- WDK の I/O バッファーのバッファー I/O
- データ バッファー WDK の I/O バッファー内の I/O
- WDK の I/O バッファーの非ページ システム
- I/O 制御コード WDK カーネル、バッファー内の I/O
- I/O WDK カーネルでは、バッファー内の I/O
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 391f688f6c200ee9f922cd68388c81beeab0d181
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570269"
---
# <a name="using-buffered-io"></a>バッファー付き I/O の使用





対話型または低速のデバイスでは、または通常は、時に、比較的少量のデータを転送するサービスを提供するドライバーを使用する必要があります、 [I/O バッファー](methods-for-accessing-data-buffers.md)転送メソッド。 全体的な物理を向上するバッファー内の I/O を小さな、対話型の転送を使用してメモリ使用量、メモリ マネージャーが、各転送の完全な物理ページをロックダウンする必要がないため、としてを要求するドライバーに対してダイレクト I/O。 一般に、ビデオ、キーボード、マウス、シリアル ポート、および並列のドライバーがバッファー内の I/O を要求します。

I/O マネージャーは、I/O 操作がバッファー内の I/O を次のように使用しているかを決定します。

-   [ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff550794)と[ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff550819)操作を要求します。\_バッファーに格納された\_IO が設定されている、**フラグ**のメンバー、 [**デバイス\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff543147)構造体。 詳細については、[デバイス オブジェクトを初期化して](initializing-a-device-object.md)を参照してください。

-   [ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)と[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)要求、IOCTL コードの値には、メソッドが含まれています。\_としてバッファリングされている、 *TransferType* IOCTL 値の値。 詳細については、[I/O 制御コードを定義する](defining-i-o-control-codes.md)を参照してください。

次の図は、I/O マネージャーの設定方法を示しています、 **IRP\_MJ\_読み取り**バッファリングされる I/O を使用する転送操作の要求。

![ユーザー バッファーのバッファー内の i/o を示す図](images/3mdlbffr.png)

図は、ドライバーの使用方法の概要を示しています、 **SystemBuffer** IRP がドライバーに入れて、デバイス オブジェクトの読み取りの要求のデータを転送するポインター**フラグ**か\_バッファー\_IO:

1.  ユーザー スペースの仮想アドレスのいくつかの範囲は、現在のスレッドのバッファーを表し、ページ ベースの物理アドレス (前の図では濃い網掛け) の範囲内でそのバッファーの内容をどこかに保存する可能性があります。

2.  I/O マネージャー サービスの現在のスレッドの読み取り要求、対象のスレッドに渡しますユーザー領域の範囲、バッファーを表す仮想アドレス。

3.  I/O マネージャーは、ユーザーが指定したバッファーのアクセシビリティと呼び出しを確認します[ **exallocatepoolwithtag に**](https://msdn.microsoft.com/library/windows/hardware/ff544520)非ページ システム領域バッファーを作成する (**SystemBuffer**)、。ユーザーが指定したバッファーのサイズ。

4.  I/O マネージャーは、新しく割り当てられたへのアクセスを提供します。 **SystemBuffer**で IRP がドライバーに送信します。

    場合は、図では、書き込み要求を表示、I/O マネージャーがデータ ユーザー バッファーからバッファーにコピー システム IRP がドライバーに送信する前にします。

5.  前の図に示すように、読み取り要求には、ドライバーは、システム容量のバッファーに、デバイスからデータを読み取ります。 このバッファーのメモリが非ページと、ドライバーが初めてロックすることがなく、バッファーを安全にアクセスできます。 読み取り要求が満たされたときに、ドライバーが呼び出す[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343) IRP にします。

6.  元のスレッドが再びアクティブとは、I/O マネージャーは、ユーザー バッファーにシステムのバッファーから読み取りでデータをコピーします。 呼び出しも[ **ExFreePool** ](https://msdn.microsoft.com/library/windows/hardware/ff544590)システム バッファーを解放します。

I/O マネージャーがドライバーのシステム領域バッファーを作成した後は、要求元のユーザー モード スレッドをスワップ アウトと可能性がある別のプロセスに属するスレッドによって、別のスレッドで物理メモリを再利用することができます。 ただし、IRP で指定したシステム領域仮想アドレスの範囲が有効なドライバー呼び出されるまで[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343) IRP にします。

大量のデータを同時に転送、具体的には、複数の転送を行うドライバーをドライバーが、バッファー内の I/O を使用しないようにします。 システムを実行すると非ページ プールは断片化するため、I/O マネージャーは、このようなドライバーの Irp で送信する、連続した大規模なシステム領域バッファーを割り当てることができません。

通常、ドライバーを使用してバッファー内の I/O 一部の種類の Irp でなど[ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)も使用している場合でも、要求[ダイレクト I/O](methods-for-accessing-data-buffers.md)します。 通常、ダイレクト I/O を使用するドライバーだけでこれを行う[ **IRP\_MJ\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff550794)と[ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff550819)を要求して、場合によってドライバー定義[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)ことを要求大量のデータ転送が必要です。

すべて**IRP\_MJ\_デバイス\_コントロール**と**IRP\_MJ\_内部\_デバイス\_コントロール**要求には、I/O 制御コードが含まれます。 I/O 制御コードは、バッファー内の I/O を使用して、IRP をサポートする必要が示されている場合、I/O マネージャーは、ユーザー アプリケーションの入力を表し、出力バッファーに 1 つのシステムのバッファーを使用します。 ドライバー サポート、そのような I/O 制御コードする必要がありますバッファーから入力データを読み取る (ある場合) を指定し、出力データ (該当する場合)、入力データを上書きすることで。 詳細については、[I/O 制御コードを定義する](defining-i-o-control-codes.md)を参照してください。

 

 




