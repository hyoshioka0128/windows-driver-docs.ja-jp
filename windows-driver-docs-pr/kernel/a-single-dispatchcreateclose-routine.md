---
title: 単一の DispatchCreateClose ルーチン
description: 単一の DispatchCreateClose ルーチン
ms.assetid: 6127d696-2409-49fc-9cbd-ba1b13c0c672
keywords:
- ディスパッチルーチン WDK カーネル、DispatchCreateClose ルーチン
- DispatchCreateClose ルーチン
- IRP_MJ_CREATE i/o 関数のコード
- IRP_MJ_CLOSE i/o 関数のコード
- ディスパッチルーチン WDK カーネルを作成する
- ディスパッチルーチン WDK カーネルを閉じる
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cfc660f7559867878be33d568b2e87dbc8763f5b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837333"
---
# <a name="a-single-dispatchcreateclose-routine"></a>単一の DispatchCreateClose ルーチン





多くのドライバー (特に、階層化されたドライバーのチェーンにある下位レベルのドライバー) では、*作成*要求の受信時に存在する必要があるだけで、*クローズ*要求の受信を確認するだけで済みます。

たとえば、 [**Iogetdeviceobjectpointer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer)を呼び出す1つ以上の密接に結合されたクラスドライバーを持つデバイスコントローラーのポートドライバーは、最小限の[*DispatchCreateClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンを持つ場合があります。 このルーチンは、次のように IRP を完了するだけではありません。

```cpp
    :    : 
{ 
    Irp->IoStatus.Status = STATUS_SUCCESS; 
 Irp->IoStatus.Information = 0; 
    IoCompleteRequest(Irp, IO_NO_INCREMENT); 
 return STATUS_SUCCESS; 
}
```

この最小*DispatchCreateClose*ルーチンは、i/o 状態ブロックの**情報**メンバーをゼロに設定します。これは、create 要求でファイルオブジェクトが開かれていることを示します。クローズ要求の場合、**情報**は意味を持ちません。 ルーチンは、 **status**メンバーを STATUS\_SUCCESS に設定し、また、ドライバーが i/o 要求を受け入れる準備ができていることを示すこのステータス値も返します。

この最小限の*DispatchCreateClose*ルーチンは、irp の発信者の優先度を上げることなく (IO\_\_の増分)、irp の開始者の優先順位を上げることなく、create irp を完了します。要求を完了するための。

*DispatchCreateClose*ルーチンが行う作業量は、ドライバーのデバイスまたは基になるデバイスの性質、およびドライバーの一部に依存します。 ドライバーが作成要求と終了要求に対してまったく異なる操作を実行する場合は、[個別の DispatchCreate および DispatchClose ルーチン](separate-dispatchcreate-and-dispatchclose-routines.md)でこれらの要求を処理する必要があります。

論理デバイスまたは物理デバイスを表すファイルオブジェクトを開くための create 要求を処理するには、最上位レベルのドライバーで次の操作を実行する必要があります。

1.  [**Iogetlocation entiを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)呼び出して、IRP 内の i/o スタックの場所へのポインターを取得します。

2.  **FileObject**を確認します。ファイル名の Unicode 文字列の**長さが 0**の場合は、i/o スタックの場所にある**filename**を使用して IRP を完了し、状態\_SUCCESS にします。それ以外の場合は、状態\_無効\_パラメーターを指定して IRP を完了します。

上記の手順に従うと、デバイスで擬似ファイルを開こうとしても、後で問題が発生する可能性があります。 たとえば、存在しない \\\\デバイス\\parallel0\\を開こうとすると、そのようなことを防ぐことができます。

 

 




