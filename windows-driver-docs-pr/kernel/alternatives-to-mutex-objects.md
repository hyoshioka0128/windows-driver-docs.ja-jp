---
title: ミュー テックス オブジェクトの代替
description: ミュー テックス オブジェクトの代替
ms.assetid: c3b78155-426a-449d-8678-5666a7a12cbd
keywords:
- カーネルディスパッチャーオブジェクト WDK、mutex オブジェクト
- ディスパッチャーオブジェクト WDK カーネル、ミューテックスオブジェクト
- mutex オブジェクト WDK カーネル
- 高速ミューテックス WDK カーネル
- 保護された mutex WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e25361ff8615c98d56f45727cd65e081fa39fa06
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837214"
---
# <a name="alternatives-to-mutex-objects"></a>ミュー テックス オブジェクトの代替


高速ミューテックスと保護されたミューテックスは、mutex オブジェクトの代わりとして使用できます。 高速ミューテックスまたは保護されたミューテックスは、mutex オブジェクトよりも迅速に取得および解放できますが、次の制限があります。

-   ドライバーは、 [**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)または[**KeWaitForMultipleObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)ルーチンを使用して、高速または保護されたミューテックスを待機することはできません。 したがって、高速または保護されたミューテックスとディスパッチャーオブジェクトを同時に待機することはできません。

-   ドライバーは、高速または保護されたミューテックスを再帰的に取得することはできません。 ドライバーが既に取得した高速または保護されたミューテックスを取得しようとすると、ドライバーがデッドロックします。 ただし、ミューテックスオブジェクトは再帰的に取得できます。

高速ミューテックスと保護されたミューテックスの詳細については、「[高速ミューテックスと保護](fast-mutexes-and-guarded-mutexes.md)されたミューテックス」を参照してください。

 

 




