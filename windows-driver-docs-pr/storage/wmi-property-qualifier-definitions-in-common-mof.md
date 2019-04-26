---
title: Common.mof 内の WMI プロパティ修飾子の定義
description: Common.mof 内の WMI プロパティ修飾子の定義
ms.assetid: 24a95c4b-f4f4-4042-9a06-069685ac0260
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: be76d11b49c3093fb8df9cc3c27c5ae6d011676d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357220"
---
# <a name="wmi-property-qualifier-definitions-in-commonmof"></a>Common.mof 内の WMI プロパティ修飾子の定義


## <span id="ddk_wmi_property_qualifier_definitions_in_common_mof_kr"></span><span id="DDK_WMI_PROPERTY_QUALIFIER_DEFINITIONS_IN_COMMON_MOF_KR"></span>


*Common.mof*ファイルは、次の WMI プロパティ修飾子を定義します。

[ISCSI\_AUTH\_型\_修飾子](iscsi-auth-types-qualifiers.md)

[ISCSI\_状態\_修飾子](iscsi-status-qualifiers.md)

[セキュリティ\_フラグ\_修飾子](security-flag-qualifiers.md)

WMI クラス定義内のデータ フィールドに、上記の修飾子のいずれかを適用する場合は、対応する構造体のメンバーに修飾子の定義に示される整数値のいずれかを割り当てることができますを示します。

そのため、WMI プロパティ修飾子では、修飾子は、一連の整数値を表すために列挙体が似ています。 WMI ツールのスイートで列挙型の宣言を生成しませんが、 *Iscsidef.h*で修飾子に対応する*Common.mof*、シンボリック定数の定義のセットをそのも生成しません修飾子の値に対応しています。

WMI プロパティ修飾子の概要については、次を参照してください。 [WMI プロパティ修飾子](https://msdn.microsoft.com/library/windows/hardware/ff566365)します。

 

 





