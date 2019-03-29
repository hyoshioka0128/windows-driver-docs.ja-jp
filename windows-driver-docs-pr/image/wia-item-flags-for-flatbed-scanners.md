---
title: フラットベッド スキャナー用 WIA 項目のフラグ
description: フラットベッド スキャナー用 WIA 項目のフラグ
ms.assetid: bd070e41-47e9-4165-a250-e759b8a214aa
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 545f3523482fb0e54a45d8a21ca4b71ba278bcb3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572656"
---
# <a name="wia-item-flags-for-flatbed-scanners"></a>フラットベッド スキャナー用 WIA 項目のフラグ





このトピックでは、ルート項目とフラット ベッド スキャナーの項目のツリーの子項目の必須および省略可能な WIA 項目フラグを使用します。 WIA 項目のフラグとその定義の完全な一覧を参照してください。 [ **WIA\_IPA\_項目\_フラグ**](https://msdn.microsoft.com/library/windows/hardware/ff551585)します。

### <a name="required-wia-item-flags-for-flatbed-scanners"></a>WIA アイテムのフラット ベッド スキャナーのフラグが必要

次の WIA 項目のフラグをサポートするために、WIA フラット ベッド スキャナーの項目が必要です。

<a href="" id="wiaitemtypeprogrammabledatasource"></a>**WiaItemTypeProgrammableDataSource**  
WIA 項目は構成可能と一連の定義済み構成規則に基づく、 [ **WIA\_IPA\_項目\_カテゴリ**](https://msdn.microsoft.com/library/windows/hardware/ff551581)プロパティ。 フラット ベッド スキャナー部分は、プログラミング可能なために、このフラグが必要です。

<a href="" id="wiaitemtypetransfer"></a>**WiaItemTypeTransfer**  
WIA 項目は、データ転送に使用できます。 フラット ベッド スキャナーの項目をデータ転送に使用できるため、このフラグが必要です。

<a href="" id="wiaitemtypefile"></a>**WiaItemTypeFile**  
項目は、ファイルです。 このフラグが必要ですが、 **WiaItemTypeImage**フラグ。

<a href="" id="wiaitemtypeimage"></a>**WiaItemTypeImage**  
項目は、イメージです。 このフラグは設定されている項目でのみ有効です、 **WiaItemTypeFile**フラグを設定します。 このフラグは、フラット ベッド スキャナーのイメージ形式を報告するために必要な[ **WIA\_IPA\_形式**](https://msdn.microsoft.com/library/windows/hardware/ff551553)プロパティの値。 WIA フラット ベッド スキャナーのすべての項目が少なくとも 1 つのイメージ形式をサポートするために必要です。 WIA が WiaImgFmt 現在必要があります\_BMP と WiaImgFmt\_MEMORYBMP としてサポートされているイメージ形式。

### <a name="optional-wia-item-flags-for-flatbed-scanners"></a>WIA の省略可能な項目のフラット ベッド スキャナーのフラグを設定します。

WIA フラット ベッド スキャナーの項目は、次 WIA 項目フラグを必要に応じてサポートできます。

<a href="" id="wiaitemtypefolder"></a>**WiaItemTypeFolder**  
アイテムはフォルダーです。 フラット ベッド スキャナーの項目に子項目が含まれている場合は、このフラグを追加します。 (これらの項目は、1 つのフラット ベッドからプラテン上で選択した複数のリージョンを含めることができます)基本の項目にのみ、このフラグを使用する必要があります。 子項目*できません*このフラグがあります。

 

 




