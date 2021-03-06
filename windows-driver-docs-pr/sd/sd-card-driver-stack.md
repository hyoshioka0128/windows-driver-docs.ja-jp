---
title: SD カードのドライバー スタック
description: SD カードのドライバー スタック
ms.assetid: 196739bb-530f-4a60-98a0-ece0b4c5ef34
keywords:
- SD WDK バス ドライバー スタック
- ドライバー スタックの WDK SD バス
- スタックの WDK SD バス
- デバイス履歴の WDK SD バス
- SDIO WDK バス
- セキュリティで保護されたデジタル I/O WDK バス
- ホスト コント ローラーの WDK SD バス
- ハードウェア WDK SD バス
- ソフトウェア バスの WDK SD
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de4452bf7f8a8a6a6f0291557f1f22485d2bb2be
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384509"
---
# <a name="sd-card-driver-stack"></a>SD カードのドライバー スタック


移植可能で、小さいメモリ カードでは、セキュリティで保護されたデジタル (SD) カードのテクノロジから始まりましたが、セキュリティで保護されたデジタルの関連付け (SDA) には Secure Digital I/O (SDIO) 仕様のリリースでは、さまざまなを含める SD テクノロジの定義が拡大されましたBluetooth デバイス、ビデオ_カメラ、ワイヤレス LAN のデバイスとグローバル配置 System (GPS) 受信機などのカード関数。 このドキュメントでは、オペレーティング システムが SD テクノロジにカード関数の拡張機能をサポートする方法について説明します。

多くの早期 SD 記憶装置のカード リーダーは、USB バスに接続するために設計されました。 Windows USB 大容量記憶装置ドライバーを使用したこれらのデバイスを管理する (*usbstor.sys*) とネイティブ ストレージ クラス ドライバー (*disk.sys*)、次の図に示すようにします。

![初期の sd 記憶域デバイスに対するデバイス スタックを示す図](images/sdio-usb.png)

Windows がメモリ カード、USB バスに接続するために作成するデバイス スタックの詳細については、次を参照してください。 [USB 大容量記憶装置のデバイス オブジェクトの例](https://docs.microsoft.com/windows-hardware/drivers/storage/device-object-example-for-a-usb-mass-storage-device)します。

まず、オペレーティング システムにより、PCI バスに直接接続する SD ホスト コントローラーのサポートが提供されます。 システムでは、SD のホスト コント ローラーを列挙するネイティブ SD バス ドライバーが読み込まれます (*sdbus.sys*)。 SD メモリ カードを挿入すると、Windows はネイティブ SD 記憶域クラス ドライバーを読み込みます (*sffdisk.sys*) と記憶域ミニポート ドライバー (*sffp\_sd.sys*) バス ドライバーの上にします。 GPS やワイヤレス LAN など、機能の異なる SD カードが挿入された場合は、そのデバイス用にベンダーから提供されているドライバーが読み込まれます。

SD スタック内のすべてのデバイス ドライバー ネイティブまたはベンダーから提供されたかどうか通信する必要がある SD バス ドライバー SD バスのスタティック ライブラリでルーチンを呼び出すことによって (*sdbus.lib*)。 SD ドライバーは、コンパイルするときに、このライブラリにリンクする必要があります。 次の図は、列挙 SD のコント ローラーとカードに付随するときに、システムが作成した SD ドライバー スタックを示します。

![sd のハードウェアとソフトウェアのコンポーネント間の関係を示す図](images/sdiostack.png)

SD デバイス ドライバーは、ホスト コント ローラーのレジスタ セットに直接アクセスできません。 また I/O 要求パケット (Irp) でホスト コント ローラーにパススルー コマンドを埋め込むことができます。 SD デバイス ドライバーは、SD バス ライブラリのルーチンを呼び出すことによって、ホスト コント ローラーにコマンドを発行し、ライブラリ ホスト コント ローラーに対する適切な SD コマンドが生成されます。

SD デバイス ドライバーが標準の PnP と電力の Irp を処理する必要がありますが、要求またはポート、メモリなどのハードウェア リソースを管理したりしないでベクトルの割り込み。 その結果、SD デバイス ドライバーは、処理するときに、すべてのハードウェア リソースをマップする必要はありません、 [ **IRP\_MN\_開始\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-start-device)要求。 ただし、SD のデバイス ドライバーを受け取ると、 [ **IRP\_MN\_停止\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-stop-device)要求と、すべての I/O 操作を停止する必要があります。 さらに、ドライバーは SD バス ドライバーへの応答には、そのインターフェイスを閉じる必要があります、 [ **IRP\_MN\_クエリ\_削除\_デバイス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-remove-device)要求。

ハードウェアの割り込みが発生したときに SD バス ライブラリは、割り込みをインターセプト、さらに割り込み、マスクし、ハードウェアの割り込みが発生するコールバック ルーチンを使用して SD デバイス ドライバーを通知します。 バス ドライバーを使用して、SD のデバイス ドライバーのハードウェアの割り込みを通知するコールバック ルーチンの説明は、次を参照してください。 [ **PSDBUS\_コールバック\_ルーチン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddsd/nc-ntddsd-sdbus_callback_routine)します。 SD ドライバー スタックとライブラリがハードウェア割り込みを管理する方法の一般情報については、次を参照してください。[処理セキュア デジタル (SD) ハードウェアの割り込み](https://docs.microsoft.com/windows-hardware/drivers/sd/handling-sd-card-interrupts)します。

*Ntddsd.h*ヘッダー ファイルは、Windows Driver Kit (WDK) で指定すると、SD のバス ライブラリによって公開されるルーチンのプロトタイプを宣言します。

 

 




