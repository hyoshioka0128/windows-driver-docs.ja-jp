---
title: SD カードのドライバー スタック
description: SD カードのドライバー スタック
ms.assetid: 196739bb-530f-4a60-98a0-ece0b4c5ef34
keywords:
- SD WDK バス, ドライバースタック
- ドライバースタック WDK SD バス
- スタック WDK SD bus
- デバイススタック WDK SD バス
- SDIO WDK バス
- デジタル i/o WDK バスをセキュリティで保護する
- ホストコントローラー WDK SD バス
- ハードウェア WDK SD バス
- ソフトウェア WDK SD bus
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 437f76be200944e7677987dbe216d7d1f9299554
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824732"
---
# <a name="sd-card-driver-stack"></a>SD カードのドライバー スタック


セキュアデジタル (SD) カードテクノロジは、移植可能な小さなメモリカードで開始されましたが、セキュリティで保護されたデジタル i/o (SDIO) 仕様がリリースされたため、セキュアデジタルアソシエーション (SDA) は SD テクノロジの定義を拡大して、Bluetooth デバイス、ビデオカメラ、ワイヤレス LAN デバイス、Global Positioning System (GPS) レシーバーなどのカード機能。 このドキュメントでは、オペレーティングシステムが SD テクノロジのカード関数拡張機能をサポートするしくみについて説明します。

多くの初期 SD 記憶装置のカードリーダーは、USB バスに接続するように設計されています。 Windows は、次の図に示すように、USB 大容量記憶装置ドライバー (*usbstor.sys*) とネイティブストレージクラスドライバー (*disk.sys*) を使用してこれらのデバイスを管理します。

![初期の sd ストレージデバイスのデバイススタックを示す図](images/sdio-usb.png)

USB バスに接続するメモリカード用に Windows によって作成されるデバイススタックの詳細については、「 [Usb 大容量記憶装置のデバイスオブジェクトの例](https://docs.microsoft.com/windows-hardware/drivers/storage/device-object-example-for-a-usb-mass-storage-device)」を参照してください。

まず、オペレーティング システムにより、PCI バスに直接接続する SD ホスト コントローラーのサポートが提供されます。 システムは SD ホストコントローラーを列挙すると、ネイティブ SD bus ドライバー (*sdbus .sys*) を読み込みます。 ユーザーが SD メモリカードを挿入すると、Windows はネイティブ SD storage クラスドライバー (*sffdisk .sys*) と記憶域ミニポートドライバー (*sffp\_SD*) をバスドライバーの上に読み込みます。 GPS やワイヤレス LAN など、機能の異なる SD カードが挿入された場合は、そのデバイス用にベンダーから提供されているドライバーが読み込まれます。

SD スタック内のすべてのデバイスドライバーは、ネイティブまたはベンダーから提供されているかどうかにかかわらず、静的 SD バスライブラリ (*sdbus .lib*) でルーチンを呼び出すことによって、sd バスドライバーと通信する必要があります。 SD ドライバーは、コンパイル時にこのライブラリにリンクする必要があります。 次の図は、SD コントローラーと付随カードを列挙するときにシステムによって作成される SD ドライバースタックを示しています。

![sd ソフトウェアとハードウェアコンポーネントの関係を示す図](images/sdiostack.png)

SD デバイスドライバーは、ホストコントローラーレジスタセットに直接アクセスできません。また、ホストコントローラーのパススルーコマンドを i/o 要求パケット (Irp) に埋め込むこともできません。 SD デバイスドライバーは、SD bus ライブラリルーチンを呼び出して、ホストコントローラーにコマンドを発行します。その後、ライブラリによって、ホストコントローラーに適した SD コマンドが生成されます。

SD デバイスドライバーは、標準の PnP と電源 Irp を処理する必要がありますが、ポート、メモリ、割り込みベクターなどのハードウェアリソースを要求したり管理したりすることはありません。 そのため、\_IRP を処理するときに、SD デバイスドライバーが\_デバイスの要求を[**開始\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)て、ハードウェアリソースをマップする必要はありません。 ただし、SD デバイスドライバーが、\_デバイスの要求を[**停止\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)を受信した場合、すべての i/o 操作を停止する必要があります。 さらに、ドライバーは、 [**IRP\_の\_クエリ\_\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)要求の削除に応答して、SD バスドライバーへのインターフェイスを閉じる必要があります。

ハードウェアの割り込みが発生すると、SD bus ライブラリは割り込みをインターセプトし、さらに割り込みを解除し、ハードウェアの割り込みが発生したことを示すコールバックルーチンによって SD デバイスドライバーに通知します。 ハードウェア割り込みの SD デバイスドライバーに通知するためにバスドライバーが使用するコールバックルーチンの説明については、「 [**PSDBUS\_callback\_ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddsd/nc-ntddsd-sdbus_callback_routine)」を参照してください。 SD ドライバーのスタックとライブラリがハードウェアの割り込みを管理する方法に関する一般的な説明については、「[セキュアデジタル (sd) ハードウェア割り込みの処理](https://docs.microsoft.com/windows-hardware/drivers/sd/handling-sd-card-interrupts)」を参照してください。

Windows Driver Kit (WDK) に用意されている ntddsd ヘッダーファイルは、SD bus ライブラリによって公開されるルーチンのプロトタイプを宣言し*ます*。

 

 




