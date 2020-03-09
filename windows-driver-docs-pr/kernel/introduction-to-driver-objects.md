---
title: ドライバー オブジェクトの概要
description: ドライバー オブジェクトの概要
ms.assetid: 497ee2dc-671d-408e-b228-16dc24532375
keywords:
- ドライバーオブジェクト WDK カーネル
- 標準ドライバールーチン WDK カーネル、ドライバーオブジェクト
- ドライバールーチン WDK カーネル、ドライバーオブジェクト
- ルーチン WDK カーネル、ドライバーオブジェクト
- オブジェクト WDK ドライバーオブジェクト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5736566d6b407690ceea71b2d7d78a92cff7bc2c
ms.sourcegitcommit: e1cfed28850a8208ea27e7a6a336de88c48e9948
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/06/2020
ms.locfileid: "78402425"
---
# <a name="introduction-to-driver-objects"></a>ドライバー オブジェクトの概要


## <a href="" id="ddk-introduction-to-driver-objects-kg"></a>


I/o マネージャーは、インストールおよび読み込みが完了した各ドライバーの*ドライバーオブジェクト*を作成します。 ドライバーオブジェクトは、[**ドライバー\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)構造を使用して定義されます。

I/o マネージャーがドライバーの[**Driverentry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)ルーチンを呼び出すと、ドライバーのドライバーオブジェクトのアドレスが提供されます。 Driver オブジェクトには、ドライバーの標準ルーチンの多くに対するエントリポイントのストレージが含まれています。 ドライバーは、これらのエントリポイントを入力する役割を担います。

## <a href="" id="driver-object-illustration"></a>


次の図は、ドライバーオブジェクトを示しています。これは、最下位レベルのドライバーと上位レベルのドライバーが持つことができるシステム定義の標準ルーチンのセットです。

名前の横にアスタリスクが付いた各標準ルーチンは、i/o 要求パケット (IRP) を入力として受け取ります。 これらの各標準ルーチンは、i/o 要求のターゲットデバイスオブジェクトへのポインターも受け取ります。

![driver オブジェクトを示す図](images/24drvobj.png)

I/o マネージャーは、ドライバーオブジェクトの種類を定義し、ドライバーオブジェクトを使用して、読み込まれたドライバーのイメージに関する情報を登録および追跡します。 Driver オブジェクトのディスパッチエントリポイント ( **dddispatch * * * Xxx*から**Dddispatch * **Yyy*)*** は、irp の i/o スタックの場所で渡される主な関数コード (irp\_MJ\_Xxx * * *) に対応します。

I/o マネージャーは、各 IRP をドライバーが提供するディスパッチルーチンに最初にルーティングします。 一般に、最下位レベルのドライバーのディスパッチルーチンは、ドライバーの[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンに有効な引数を持つ各 IRP をキューに入れて (または成功させる)、i/o サポートルーチン ([**iostartpacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)) を呼び出します。 *StartIo*ルーチンは、特定のデバイスで要求された i/o 操作を開始します。 通常、上位レベルのドライバーには*StartIo*ルーチンがありませんが、できます。

 

 




