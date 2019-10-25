---
title: データ バッファーにアクセスする方法
description: データ バッファーにアクセスする方法
ms.assetid: f95a0aec-65f9-44c9-8ae5-11bb4d832752
keywords:
- I/o WDK カーネル、データバッファー
- データバッファー WDK i/o
- WDK i/o をバッファーする
- バッファー WDK i/o、アクセス
- データバッファー WDK i/o、アクセス
- データ転送 WDK カーネル、データバッファーアクセス
- データの転送 WDK カーネル、データバッファーアクセス
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a32e63f8c8ca2c37e2080053c13675444d8481d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827867"
---
# <a name="methods-for-accessing-data-buffers"></a>データ バッファーにアクセスする方法


ドライバースタックの主要な役割の1つは、ユーザーモードアプリケーションとシステムデバイス間でデータを転送することです。 オペレーティングシステムには、データバッファーにアクセスするための次の3つの方法が用意されています。

<a href="" id="buffered-i-o"></a>*バッファーされる i/o*  
オペレーティングシステムによって、アプリケーションのバッファーと同じサイズの非ページシステムバッファーが作成されます。 書き込み操作の場合、i/o マネージャーは、ドライバースタックを呼び出す前に、ユーザーデータをシステムバッファーにコピーします。 読み取り操作の場合、i/o マネージャーは、要求された操作がドライバースタックによって完了した後に、システムバッファーからアプリケーションのバッファーにデータをコピーします。

詳細については、「[バッファー i/o の使用](using-buffered-i-o.md)」を参照してください。

<a href="" id="direct-i-o"></a>*ダイレクト i/o*  
オペレーティングシステムは、メモリ内のアプリケーションのバッファーをロックします。 次に、ロックされたメモリページを識別するメモリ記述子リスト (MDL) を作成し、その MDL をドライバースタックに渡します。 ドライバーは、MDL を介してロックされたページにアクセスします。

詳細については、「 [Direct i/o の使用](using-direct-i-o.md)」を参照してください。

<a href="" id="neither-buffered-nor-direct-i-o"></a>*バッファーも直接 i/o でもありません*  
オペレーティングシステムは、アプリケーションバッファーの仮想開始アドレスとサイズをドライバースタックに渡します。 バッファーには、アプリケーションのスレッドコンテキストで実行されるドライバーからのみアクセスできます。

詳細については、「[バッファーと直接 i/o の両方を使用する](using-neither-buffered-nor-direct-i-o.md)」を参照してください。

[**Irp\_MJ\_READ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-read)および[**irp\_MJ\_書き込み**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-write)要求の場合、ドライバーは各[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)構造のフラグを使用して i/o の方法を指定します。 詳細については、「[デバイスオブジェクトの初期化](initializing-a-device-object.md)」を参照してください。

[**Irp\_MJ\_デバイス\_control**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)および[**irp\_MJ\_内部\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)要求の場合、I/O メソッドは各 IOCTL に含まれる*transfertype*値によって決まります。数値. 詳細については、「 [I/o 制御コードの定義](defining-i-o-control-codes.md)」を参照してください。

ドライバースタック内のすべてのドライバーは、要求ごとに同じバッファーアクセスメソッドを使用する必要があります。ただし、最上位レベルのドライバー (下位のドライバーで使用されるメソッドに関係なく、"どちらの" メソッドも使用できます) は例外です。

 

 




