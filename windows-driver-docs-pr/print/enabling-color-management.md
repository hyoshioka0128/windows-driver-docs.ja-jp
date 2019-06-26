---
title: 色の管理を有効にする
description: 色の管理を有効にする
ms.assetid: 750d1e44-6d1c-4f18-94cb-20f1f846c0d1
keywords:
- 色の管理 WDK の印刷を有効にします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67f27497980b3f5f3ddfdd8cf91e7ea5a3e5acdd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376948"
---
# <a name="enabling-color-management"></a>色の管理を有効にする





アプリケーションまたはプリンター ドライバーのいずれかによって、色の管理を有効にできます。 アプリケーションは、次の 2 つのメソッドのいずれかで、色の管理を有効にできます。

-   呼び出す**SetICMMode** (Microsoft Windows SDK のドキュメントで説明)、ICM を指定する\_ON です。

    このメソッドは、システムによって制御された色の管理を使用します。

-   指定する、 [ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)を呼び出すときに構造体**フォーマット**、印刷ジョブと DMICMMETHOD いずれかの設定を作成する\_システム、DMICMMETHOD\_ドライバー、または DMICMMETHOD\_DEVMODE 構造体のデバイス**dmICMMethod**メンバー。

    このメソッドは、システム管理の対象、ドライバーの制御、またはデバイス制御の色の管理 (指定したコントロールの種類がサポートされていると仮定した場合) を選択するアプリケーションを使用します。

プリンター ドライバーは、色の管理を有効に DMICMMETHOD いずれかを設定して\_システム、DMICMMETHOD\_ドライバー、または DMICMMETHOD\_内のデバイス、 **dmICMMethod**ドライバーの既定のメンバーDEVMODE 構造体。 (アプリケーションでは、用の構造を DEVMODE を指定する場合に既定の設定をオーバーライドする**フォーマット**します。 さらに、ドライバーがドライバーの実行中に色の管理のユーザーの選択を保存する責任を負います[ **DrvDocumentPropertySheets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdocumentpropertysheets)関数です)。

 

 




