---
title: KSPROPSETID\_Pin
description: KSPROPSETID\_Pin
ms.assetid: a74a9cb2-2809-4e03-95da-71eeb5f079e9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ead0a61a66c47591e757b97d57010aedc869f706
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845626"
---
# <a name="kspropsetid_pin"></a>KSPROPSETID\_Pin


## <span id="ddk_kspropsetid_pin_ks"></span><span id="DDK_KSPROPSETID_PIN_KS"></span>


クライアントは、KSPROPSETID\_Pin プロパティセット内のプロパティを使用して、サポートされている各 pin ファクトリに関する情報を KS フィルターに照会します。

[**Ksk プロパティ\_ピン留め\_CTYPES**](ksproperty-pin-ctypes.md)プロパティは、KS フィルターがサポートする pin ファクトリの数を指定します。 このプロパティセットの他のすべてのプロパティは、個々の pin ファクトリに関する情報を指定します。 KS フィルターは、各 pin ファクトリを ID で識別します。これは0から、pin ファクトリの数から1を引いた数までの範囲です。 クライアントには、プロパティ要求を発行するときに使用する[**KSP\_ピン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)構造内にピンファクトリ T が含まれています。

KSK PROPSETID\_ピンのプロパティセットには次のものが含まれます。

[**KSK プロパティ\_ピン\_カテゴリ**](ksproperty-pin-category.md)

[**KSK プロパティ\_ピン\_CINSTANCES**](ksproperty-pin-cinstances.md)

[**KSK プロパティ\_PIN\_通信**](ksproperty-pin-communication.md)

[**KSK プロパティ\_PIN\_CONSTRAINEDDATARANGES**](ksproperty-pin-constraineddataranges.md)

[**KSK プロパティ\_ピン\_CTYPES**](ksproperty-pin-ctypes.md)

[**KSK プロパティ\_ピン留め\_データフロー**](ksproperty-pin-dataflow.md)

[**KSK プロパティ\_ピン\_DATAINTERSECTION 集合**](ksproperty-pin-dataintersection.md)

[**KSK プロパティ\_PIN\_DATARANGES**](ksproperty-pin-dataranges.md)

[**KSK プロパティ\_\_GLOBALCINSTANCES にピン留めする**](ksproperty-pin-globalcinstances.md)

[**KSK プロパティ\_ピン留め\_インターフェイス**](ksproperty-pin-interfaces.md)

[**KSK プロパティ\_ピン\_メディア**](ksproperty-pin-mediums.md)

[**KSK プロパティ\_PIN\_名**](ksproperty-pin-name.md)

[**KSK プロパティ\_PIN\_NECESSARYINSTANCES**](ksproperty-pin-necessaryinstances.md)

[**KSK プロパティ\_固定\_PHYSICALCONNECTION**](ksproperty-pin-physicalconnection.md)

[**KSK プロパティ\_PIN\_PROPOSEDATAFORMAT**](ksproperty-pin-proposedataformat.md)

[**KSK プロパティ\_PIN\_PROPOSEDATAFORMAT2**](ksproperty-pin-proposedataformat2.md)

 

 





