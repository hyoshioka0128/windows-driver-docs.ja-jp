---
title: KSPROPSETID \_ Pin
description: KSPROPSETID \_ Pin
ms.assetid: a74a9cb2-2809-4e03-95da-71eeb5f079e9
ms.date: 06/26/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5775c3a892fcc869794b20caa85d0801b6b0f5ab
ms.sourcegitcommit: 7a69c2e0abf91a57407b13a30faf24925f677970
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85829005"
---
# <a name="kspropsetid_pin"></a>KSPROPSETID \_ Pin


## <span id="ddk_kspropsetid_pin_ks"></span><span id="DDK_KSPROPSETID_PIN_KS"></span>


クライアントは、KSPROPSETID pin プロパティに設定されているプロパティを使用して、 \_ サポートされている各 Pin ファクトリに関する情報を KS フィルターに照会します。

[**Ksproperty \_ ピン \_ ctypes**](ksproperty-pin-ctypes.md)プロパティは、KS フィルターがサポートする PIN ファクトリの数を指定します。 このプロパティセットの他のすべてのプロパティは、個々の pin ファクトリに関する情報を指定します。 KS フィルターは、各 pin ファクトリを ID で識別します。これは0から、pin ファクトリの数から1を引いた数までの範囲です。 クライアントには、プロパティ要求を発行するときに使用する[**KSP の \_ ピン**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)構造内に、ピンファクトリ T が含まれています。

KSPROPSETID \_ Pin プロパティセットには次のものが含まれます。

[**KSK プロパティの \_ PIN \_ カテゴリ**](ksproperty-pin-category.md)

[**KSPROPERTY \_ ピン \_ CINSTANCES**](ksproperty-pin-cinstances.md)

[**KSK プロパティの \_ PIN \_ 通信**](ksproperty-pin-communication.md)

[**KSPROPERTY \_ PIN \_ CONSTRAINEDDATARANGES**](ksproperty-pin-constraineddataranges.md)

[**KSPROPERTY \_ ピン \_ CTYPES**](ksproperty-pin-ctypes.md)

[**KSK プロパティ \_ ピンデータ \_ フロー**](ksproperty-pin-dataflow.md)

[**KSK プロパティ \_ ピン \_ DATAINTERSECTION と**](ksproperty-pin-dataintersection.md)

[**KSPROPERTY \_ PIN \_ DATARANGES**](ksproperty-pin-dataranges.md)

[**KSK プロパティ \_ ピン \_ GLOBALCINSTANCES**](ksproperty-pin-globalcinstances.md)

[**KSK プロパティの \_ PIN \_ インターフェイス**](ksproperty-pin-interfaces.md)

[**KSK プロパティの \_ PIN \_ メディア**](ksproperty-pin-mediums.md)

[**KSPROPERTY \_ PIN \_ MODEDATAFORMATS**](ksproperty-pin-modedataformats.md)

[**KSK プロパティの \_ PIN \_ 名**](ksproperty-pin-name.md)

[**KSPROPERTY \_ PIN \_ NECESSARYINSTANCES**](ksproperty-pin-necessaryinstances.md)

[**KSPROPERTY \_ ピン \_ PHYSICALCONNECTION**](ksproperty-pin-physicalconnection.md)

[**KSPROPERTY \_ PIN \_ PROPOSEDATAFORMAT**](ksproperty-pin-proposedataformat.md)

[**KSPROPERTY \_ PIN \_ PROPOSEDATAFORMAT2**](ksproperty-pin-proposedataformat2.md)

 

 





