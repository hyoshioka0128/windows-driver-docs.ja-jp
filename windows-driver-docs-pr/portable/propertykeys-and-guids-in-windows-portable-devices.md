---
Description: Windows ポータブル デバイスの PROPERTYKEY と GUID
title: Windows ポータブル デバイスの PROPERTYKEY と GUID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba408fa498b0e543d8de61c16571e77d86ee9c69
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376230"
---
# <a name="propertykeys-and-guids-in-windows-portable-devices"></a>Windows ポータブル デバイスの PROPERTYKEY と GUID


プロパティまたはコマンドがで識別される、 **PROPERTYKEY**構造体。 A **PROPERTYKEY** 2 つの部分の構造から成る: GUID (、 *fmtid*メンバー) と、DWORD (、 *pid*メンバー)。 GUID の一部を使用して、プロパティ、カテゴリを指定またはコマンドが属する (つまり、関連のプロパティは、同じカテゴリに属すると関連するコマンドが同じカテゴリに属している。 したがって、は同じ*fmtid*)。 DWORD の一部が、プロパティまたはコマンドの ID を示し、個々 のプロパティまたはプロパティまたはコマンドのカテゴリ内のコマンドを区別するために使用 (つまり、 *pid*プロパティまたは同じカテゴリ内のコマンドの値になります異なる)。

このドキュメントのリファレンス セクションでは、WPD によって定義されたすべての PROPERTYKEY 値について説明します。 これらの値は、コマンド、プロパティ、およびリソースに対応します。 カスタム PROPERTYKEY 値を作成する場合は、新しい GUID カテゴリを定義する必要があります。WPD GUID 値またはことのリスクの既存および将来の WPD 指定 PROPERTYKEYs と競合してを再利用しないでください。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**WPD\_コンテンツ\_型\_機能\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff597845)

[**オブジェクトの要件**](requirements-for-objects.md)

[**オブジェクトの形式の Guid**](https://msdn.microsoft.com/library/windows/hardware/ff597651)

[**リソースの要件**](https://msdn.microsoft.com/library/windows/hardware/ff597663)

[**コマンド**](https://msdn.microsoft.com/library/windows/hardware/ff597554)

[**プロパティと属性**](https://msdn.microsoft.com/library/windows/hardware/ff597900)

[**WPD ドライバーの概要**](wpd-drivers-overview.md)

 

 





