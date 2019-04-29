---
title: 仮想サブユニット デバイス識別子
description: 仮想サブユニット デバイス識別子
ms.assetid: c2018560-f9f4-4aaa-b2b2-8ac5195b892f
keywords:
- AV/C WDK、識別子
- WDK AV/C 識別子
- デバイス Id の WDK AV/C
- Avc.sys 関数ドライバー WDK、識別子
- 仮想のサブユニット デバイス識別子 WDK AV/C
- サブユニット サポート WDK AV/C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 096f7a783712dbb85d52f6edb7d4bc8042c1d487
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329956"
---
# <a name="virtual-subunit-device-identifiers"></a>仮想サブユニット デバイス識別子


デバイス識別子の形式に似ています (ID) のフィールドの[ピアのサブユニット](peer-subunit-device-identifiers.md)、形式を*Avc.sys* で説明する形式に基づいて、仮想のサブユニットデバイス識別子の文字列を生成するために使用[AV/C デバイス Id](av-c-device-identifiers.md)、次に示します。

-   ハードウェア id

<a href="" id="vavc-vendor-model-subunittype-subunitid"></a>**VAVC\\*ベンダー*&*モデル*&*SubunitType*& * SubunitID***  
このハードウェア識別子では、最も完全ながサブユニット識別子 (アンパサンド区切りの最後の部分、デバイスの識別子) は通常、関係のないため、めったにありません、INF ファイルに指定これです。

-   互換性のある識別子

<a href="" id="vavc-subunittype-subunitid"></a>**VAVC\\*SubunitType*& * SubunitID***  
中に*Avc.sys*この種類は行わないピアのサブユニットの互換性のある識別子は、仮想のサブユニットのこの種の互換性のある識別子を提供には。

<a href="" id="vavc-subunittype"></a>**VAVC\\* SubunitType***  
中に*Avc.sys*この種類は行わないピアのサブユニットの互換性のある識別子は、仮想のサブユニットのこの種の互換性のある識別子を提供には。

<a href="" id="vavc-generic"></a>**VAVC\\GENERIC**  
「汎用」単位ドライバーには、INF ファイルでのこのエントリが含まれています。

 

 




