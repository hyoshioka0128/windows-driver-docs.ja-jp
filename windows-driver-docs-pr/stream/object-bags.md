---
title: オブジェクト バッグ
description: オブジェクト バッグ
ms.assetid: b7ee5756-1c79-4ead-9999-d13be9a0d3d9
keywords:
- AVStream オブジェクトバッグ WDK
- オブジェクトバッグ WDK AVStream
- オブジェクト WDK AVStream
- メモリ管理 (WDK AVStream)
- AVStream WDK 用に動的に割り当てられたデータを共有する
- 動的に割り当てられたデータ WDK AVStream
- AVStream 記述子 WDK
- 記述子 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 334f5da09ea3f1cb7b9c26a2245dfc64aebdc3ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823567"
---
# <a name="object-bags"></a>オブジェクト バッグ





AVStream は、ミニドライバーに表示される各 AVStream オブジェクトのオブジェクトバッグと呼ばれるコンストラクトを管理します。 オブジェクトバッグは、特定のオブジェクトに関連付けられた動的に割り当てられたメモリを保持するための汎用コンテナーです。

次の構造体には KSOBJECT\_BAG 型のメンバーがあります。これは PVOID: [**Ksdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice)、 [**ksfilterfactory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilterfactory)、 [**Ksdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter)、および[**kspin**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_kspin)と同等です。

オブジェクトバッグの用途は次のとおりです。

-   メモリ管理。

    ミニドライバーでは、メモリ管理にオブジェクトバッグを使用して、クリーンアップ作業を減らすことができます。 これを行うには、ミニドライバーが最初に[**Exallocatepoolwithtag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)を呼び出して動的メモリを割り当て、特定のオブジェクトに関連付ける必要があります。 次に、ミニドライバーは、 [**Ksk Additemtoobjectbag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksadditemtoobjectbag)を呼び出して、割り当てられたメモリをオブジェクトバッグに追加します。

    ミニドライバーが**Ksk Additemtoobjectbag**を呼び出すと、avstream は既定のクリーンアップ関数 (通常は[**exfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)) をオブジェクトと関連付けます。 また、ミニドライバーには、ミニドライバーによって提供されるクリーンアップルーチンへのポインターを、 **Ksadditemtoobjectbag**の*Free*パラメーターに含めることができます。 オブジェクトが閉じられると、AVStream はオブジェクトバッグからすべての項目を削除し、関連付けられたクリーンアップルーチンを呼び出します。

-   複数の AVStream オブジェクト間で動的に割り当てられたデータを共有します。

    ミニドライバーは、複数のオブジェクトバッグに特定の項目を配置することで、動的に割り当てられたデータを複数の AVStream オブジェクト間で共有できます。 この場合、AVStream は、オブジェクトバッグに含まれなくなるまで、指定された項目を解放しません。 オブジェクトバッグに含めることができる項目の数に関する制限は、使用可能なメモリだけです。

-   記述子を使用して編集できる構造を決定します。

    ミニドライバーが記述子または記述子サブ構造体を動的に割り当てる場合、ミニドライバーは該当するオブジェクトバッグに記述子を配置します。 次に、 [ **\_KsEdit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-_ksedit)関数は、この情報を使用して、特定の構造体を編集できるかどうかを判断します。

所有オブジェクトが削除されると、AVStream はオブジェクトバッグから項目を自動的に削除します。

ミニドライバーは、 [**KsRemoveItemFromObjectBag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksremoveitemfromobjectbag)または[**ksdiscard**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksdiscard)を呼び出すことによって、オブジェクトバッグから個々の項目を削除できます。

 

 




