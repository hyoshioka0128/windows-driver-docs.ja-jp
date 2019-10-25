---
title: 色の管理を有効にする
description: 色の管理を有効にする
ms.assetid: 750d1e44-6d1c-4f18-94cb-20f1f846c0d1
keywords:
- 色の管理 WDK 印刷、有効化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c174a4a0d7dcdb50be304975a2e1202908330396
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838101"
---
# <a name="enabling-color-management"></a>色の管理を有効にする





色の管理は、アプリケーションまたはプリンタードライバーで有効にすることができます。 アプリケーションでは、次の2つの方法のいずれかによって、色の管理を有効にできます。

-   (Microsoft Windows SDK のドキュメントで説明されている) **Seticmmode**を呼び出して、での ICM\_を指定します。

    この方法では、システム制御の色の管理が有効になります。

-   **Createdc**を呼び出して印刷ジョブを作成するときに[**devmodew**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)構造体を指定し、DEVMODE 構造体の**DMICMMETHOD**で dmicmmethod\_SYSTEM、dmicmmethod\_ドライバー、または dmicmmethod\_デバイスを設定するレプリカ.

    このメソッドを使用すると、アプリケーションは、システムによって制御される、ドライバーによって制御される、またはデバイスで制御されるカラー管理を選択できます (指定したコントロールの種類がサポートされている場合)。

プリンタードライバーは、ドライバーの既定の DEVMODE 構造体**の dmicmmethod メンバーで**、dmicmmethod\_SYSTEM、dmicmmethod\_ドライバー、または dmicmmethod\_デバイスを設定することによって、カラー管理を有効にすることができます。 ( **Createdc**の DEVMODE 構造体を指定すると、アプリケーションは既定の設定をオーバーライドできます。 さらに、ドライバーは、ドライバーの[**DrvDocumentPropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentpropertysheets)関数の実行中に、ユーザーが色の管理を行うための選択肢を格納します。

 

 




