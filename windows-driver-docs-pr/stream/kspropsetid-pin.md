---
title: KSPROPSETID\_暗証番号 (pin)
description: KSPROPSETID\_暗証番号 (pin)
ms.assetid: a74a9cb2-2809-4e03-95da-71eeb5f079e9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd70aee31074338f1bccb30cc316d39a89175b67
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384650"
---
# <a name="kspropsetidpin"></a>KSPROPSETID\_暗証番号 (pin)


## <span id="ddk_kspropsetid_pin_ks"></span><span id="DDK_KSPROPSETID_PIN_KS"></span>


クライアントが、KSPROPSETID でプロパティを使用して\_暗証番号 (pin) のプロパティでサポートされる各ピン ファクトリについては、KS フィルターのクエリに設定します。

[ **KSPROPERTY\_PIN\_CTYPES** ](ksproperty-pin-ctypes.md)プロパティの数の pin ファクトリ、KS サポートをフィルター処理を指定します。 このプロパティ セット内の他のすべてのプロパティは、ピン留めする個々 の出荷時の情報を指定します。 KS フィルターは、暗証番号 (pin) ファクトリから 1 を引いた数の 0 から、ID によって各ピン留めするファクトリを識別します。 クライアントには内では、ピン留めするファクトリ T にはが含まれています、 [ **KSP\_PIN** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksp_pin)プロパティ要求を発行時に使用する構造体。

KSPROPSETID\_暗証番号 (pin) プロパティ セットが含まれます。

[**KSPROPERTY\_PIN\_カテゴリ**](ksproperty-pin-category.md)

[**KSPROPERTY\_PIN\_CINSTANCES**](ksproperty-pin-cinstances.md)

[**KSPROPERTY\_PIN\_通信**](ksproperty-pin-communication.md)

[**KSPROPERTY\_PIN\_CONSTRAINEDDATARANGES**](ksproperty-pin-constraineddataranges.md)

[**KSPROPERTY\_PIN\_CTYPES**](ksproperty-pin-ctypes.md)

[**KSPROPERTY\_PIN\_データ フロー**](ksproperty-pin-dataflow.md)

[**KSPROPERTY\_PIN\_DATAINTERSECTION**](ksproperty-pin-dataintersection.md)

[**KSPROPERTY\_PIN\_DATARANGES**](ksproperty-pin-dataranges.md)

[**KSPROPERTY\_PIN\_GLOBALCINSTANCES**](ksproperty-pin-globalcinstances.md)

[**KSPROPERTY\_PIN\_インターフェイス**](ksproperty-pin-interfaces.md)

[**KSPROPERTY\_PIN\_メディア**](ksproperty-pin-mediums.md)

[**KSPROPERTY\_PIN\_名**](ksproperty-pin-name.md)

[**KSPROPERTY\_PIN\_NECESSARYINSTANCES**](ksproperty-pin-necessaryinstances.md)

[**KSPROPERTY\_PIN\_PHYSICALCONNECTION**](ksproperty-pin-physicalconnection.md)

[**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT**](ksproperty-pin-proposedataformat.md)

[**KSPROPERTY\_PIN\_PROPOSEDATAFORMAT2**](ksproperty-pin-proposedataformat2.md)

 

 





