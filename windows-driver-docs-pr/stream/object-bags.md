---
title: オブジェクト バッグ
description: オブジェクト バッグ
ms.assetid: b7ee5756-1c79-4ead-9999-d13be9a0d3d9
keywords:
- AVStream オブジェクト バッグ WDK
- WDK AVStream バッグをオブジェクトします。
- WDK AVStream オブジェクト
- WDK AVStream のメモリ管理
- AVStream WDK のデータを共有を動的に割り当てられています。
- 動的に割り当てられたデータ WDK AVStream
- AVStream 記述子 WDK
- WDK AVStream 記述子
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7d35628bd23d5f87dc3db0fc9dcbc799a9c035d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377515"
---
# <a name="object-bags"></a>オブジェクト バッグ





AVStream は、ミニドライバーに表示される AVStream オブジェクトごとに、オブジェクトのバッグと呼ばれる構造を管理します。 オブジェクト、バッグは、割り当てられている特定のオブジェクトに関連付けられているメモリを動的に保持するための汎用コンテナーです。

次の構造が KSOBJECT 型のメンバーを持つ\_バッグは、これは PVOID に相当します。[**KSDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksdevice)、 [ **KSFILTERFACTORY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilterfactory)、 [ **KSFILTER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter)、および[ **KSPIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin)します。

オブジェクトのバッグの用途は次のとおりです。

-   メモリ管理します。

    ミニドライバーは、メモリ管理オブジェクトのバッグを使用して、クリーンアップ作業を削減できます。 これを行うために、ミニドライバーは呼び出す必要がありますまず[ **exallocatepoolwithtag に**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)を動的メモリを割り当てたり、特定のオブジェクトに関連付けます。 ミニドライバーし、割り当てられたメモリをバッグに追加のオブジェクトを呼び出して[ **KsAddItemToObjectBag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksadditemtoobjectbag)します。

    ミニドライバーを呼び出すと**KsAddItemToObjectBag**、AVStream に既定のクリーンアップ関数が関連付けられます (通常[ **ExFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool)) オブジェクトを使用します。 または、ミニドライバーは内のミニドライバーのクリーンアップ ルーチンへのポインターを含めることができます、 *Free*パラメーターの**KsAddItemToObjectBag**します。 オブジェクトが閉じられたときに AVStream オブジェクト バッグからのすべての項目を削除し、関連するクリーンアップ ルーチンを呼び出します。

-   動的に共有には、いくつかの AVStream オブジェクト間でデータが割り当てられます。

    ミニドライバーは、1 つ以上のオブジェクトのバッグで特定の項目を配置することで AVStream のいくつかのオブジェクト間で動的に割り当てられたデータを共有できます。 この場合は、任意のオブジェクトのバッグで不要になったに含まれるまで、AVStream は特定の項目を解放できません。 唯一の制限できる、オブジェクトのバッグに含まれる項目の数には、使用可能なメモリです。

-   どの構造体は、記述子で編集できるかを決定します。

    記述子または記述子のサブ構造体、ミニドライバーを動的に割り当てます、ミニドライバーは、関連するオブジェクトのバッグで記述子を配置します。 [  **\_KsEdit** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-_ksedit)関数が、この情報を使用して特定の構造を編集できるかどうかを判断します。

AVStream を使用、オブジェクトのバッグから所有するオブジェクトが削除された場合の項目が自動的に削除します。

ミニドライバーは呼び出すことによって、オブジェクトのバッグから個々 の項目を削除することができます[ **KsRemoveItemFromObjectBag** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksremoveitemfromobjectbag)または[ **KsDiscard**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksdiscard)します。

 

 




