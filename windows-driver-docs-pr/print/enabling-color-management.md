---
title: 色の管理を有効にする
description: 色の管理を有効にする
ms.assetid: 750d1e44-6d1c-4f18-94cb-20f1f846c0d1
keywords:
- 色の管理 WDK の印刷を有効にします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 017426533047c12c555cd7ad5d92c4850eba10e8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378619"
---
# <a name="enabling-color-management"></a>色の管理を有効にする





アプリケーションまたはプリンター ドライバーのいずれかによって、色の管理を有効にできます。 アプリケーションは、次の 2 つのメソッドのいずれかで、色の管理を有効にできます。

-   呼び出す**SetICMMode** (Microsoft Windows SDK のドキュメントで説明)、ICM を指定する\_ON です。

    このメソッドは、システムによって制御された色の管理を使用します。

-   指定する、 [ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)を呼び出すときに構造体**フォーマット**、印刷ジョブと DMICMMETHOD いずれかの設定を作成する\_システム、DMICMMETHOD\_ドライバー、または DMICMMETHOD\_DEVMODE 構造体のデバイス**dmICMMethod**メンバー。

    このメソッドは、システム管理の対象、ドライバーの制御、またはデバイス制御の色の管理 (指定したコントロールの種類がサポートされていると仮定した場合) を選択するアプリケーションを使用します。

プリンター ドライバーは、色の管理を有効に DMICMMETHOD いずれかを設定して\_システム、DMICMMETHOD\_ドライバー、または DMICMMETHOD\_内のデバイス、 **dmICMMethod**ドライバーの既定のメンバーDEVMODE 構造体。 (アプリケーションでは、用の構造を DEVMODE を指定する場合に既定の設定をオーバーライドする**フォーマット**します。 さらに、ドライバーがドライバーの実行中に色の管理のユーザーの選択を保存する責任を負います[ **DrvDocumentPropertySheets** ](https://msdn.microsoft.com/library/windows/hardware/ff548548)関数です)。

 

 




