---
title: Hbaapi.mof 内の WMI クラス修飾子の定義
description: Hbaapi.mof 内の WMI クラス修飾子の定義
ms.assetid: 9db543f1-f6ad-4735-8ba0-21476aa229ba
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 8c4ddf93ac8f53357fdc09180e9b8f3b9aae8b2d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386793"
---
# <a name="wmi-class-qualifier-definitions-in-hbaapimof"></a>Hbaapi.mof 内の WMI クラス修飾子の定義


## <span id="ddk_wmi_class_qualifier_definitions_in_hbaapi_mof_kr"></span><span id="DDK_WMI_CLASS_QUALIFIER_DEFINITIONS_IN_HBAAPI_MOF_KR"></span>


によって定義された WMI クラスの修飾子、 *Hbaapi.mof*ファイルは、次のとおり。

[イベント\_型\_修飾子](event-types-qualifiers.md)

[HBA\_バインド\_型](hba-bind-type.md)

[HBA\_状態](hba-status.md)

で指定した修飾子の定義に示される整数値が事前に定義したフィールド割り当てることができる、一連のいずれかを示します、WMIクラス定義内のデータフィールドに適用されるこのセクションに記載されている修飾子のいずれかの*Hbaapi.mof*します。 ここで説明した各 WMI クラスの修飾子に列挙子がような一連の整数の値を表しますが、WMI ツール スイートでは、列挙子の宣言では生成されませんしたがって*Hbapiwmi.h*で修飾子に対応します。*Hbaapi.mof*修飾子の値に対応するシンボリック定数の定義のセットが生成されることもできます。

含めることで、ただし、 *Hbaapi.h*ドライバーまたはアプリケーションが定義されている WMI クラスの修飾子に関連付けられている各値に対して、覚えやすい名前を指定するために定義されているシンボリック定数のセットを使用できます*Hbaapi.mof*します。

WMI クラスの修飾子の概要については、次を参照してください。 [WMI クラスの修飾子](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-class-qualifiers)します。

 

 





