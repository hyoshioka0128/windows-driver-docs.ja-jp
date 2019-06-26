---
Description: Windows ポータブル デバイスの PROPERTYKEY と GUID
title: Windows ポータブル デバイスの PROPERTYKEY と GUID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78552a703e83665dfb29b7b54a81a7b773ac04d6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387181"
---
# <a name="propertykeys-and-guids-in-windows-portable-devices"></a>Windows ポータブル デバイスの PROPERTYKEY と GUID


プロパティまたはコマンドがで識別される、 **PROPERTYKEY**構造体。 A **PROPERTYKEY** 2 つの部分の構造から成る: GUID (、 *fmtid*メンバー) と、DWORD (、 *pid*メンバー)。 GUID の一部を使用して、プロパティ、カテゴリを指定またはコマンドが属する (つまり、関連のプロパティは、同じカテゴリに属すると関連するコマンドが同じカテゴリに属している。 したがって、は同じ*fmtid*)。 DWORD の一部が、プロパティまたはコマンドの ID を示し、個々 のプロパティまたはプロパティまたはコマンドのカテゴリ内のコマンドを区別するために使用 (つまり、 *pid*プロパティまたは同じカテゴリ内のコマンドの値になります異なる)。

このドキュメントのリファレンス セクションでは、WPD によって定義されたすべての PROPERTYKEY 値について説明します。 これらの値は、コマンド、プロパティ、およびリソースに対応します。 カスタム PROPERTYKEY 値を作成する場合は、新しい GUID カテゴリを定義する必要があります。WPD GUID 値またはことのリスクの既存および将来の WPD 指定 PROPERTYKEYs と競合してを再利用しないでください。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**WPD\_コンテンツ\_型\_機能\_オブジェクト**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597845(v=vs.85))

[**オブジェクトの要件**](requirements-for-objects.md)

[**オブジェクトの形式の Guid**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597651(v=vs.85))

[**リソースの要件**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597663(v=vs.85))

[**コマンド**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597554(v=vs.85))

[**プロパティと属性**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff597900(v=vs.85))

[**WPD ドライバーの概要**](wpd-drivers-overview.md)

 

 





