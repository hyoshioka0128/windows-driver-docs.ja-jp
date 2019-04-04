---
title: XPS プリンター ドライバー (XPSDrv)
description: XPSDrv、強化された、GDI ベース バージョン 3 プリンター ドライバーが Windows Vista より前に使用されました。
ms.assetid: 7567c514-3034-4db0-9622-31d14eb3772e
keywords:
- プリンター ドライバー WDK、XPSDrv プリンター ドライバー
- XPSDrv プリンター ドライバー WDK
- XPSDrv プリンター ドライバーに関する XPSDrv プリンター ドライバー WDK、
- 構成モジュール WDK XPSDrv
- WDK XPSDrv モジュールを表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1efd2c4dae9ebefc57be5d9ef17fc19047eb2c0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571152"
---
# <a name="xps-printer-driver-xpsdrv"></a>XPS プリンター ドライバー (XPSDrv)


XPS のプリンター ドライバー (XPSDrv) は、GDI ベースの強化されたバージョン 3 プリンタ ドライバを Windows Vista より前に使用されました。 (GDI に基づくもの) のような XPSDrv プリンター ドライバーは、次の 3 つの主要なコンポーネントで構成されます。

XPSDrv プリンター ドライバーの 3 つの主要なコンポーネントを次に示します。

-   [XPSDrv レンダー モジュール](xpsdrv-render-module.md)

-   [XPSDrv 構成モジュール](xpsdrv-configuration-module.md)

-   [XPSDrv インストール](xpsdrv-installation.md)

XPSDrv プリンター ドライバーの構成のモジュールの構成のモジュールと同じ機能を提供する、[プリンター インターフェイス DLL](printer-interface-dll.md)構成モジュールが、GDI ベースのドライバーでは、XPSDrv のサポートも、 [印刷チケットと印刷機能のテクノロジ](print-ticket-and-print-capabilities-technologies.md)します。

XPSDrv プリンター ドライバーのレンダリングのモジュールは必ずしも、GDI ベースのプリンター ドライバーの GDI ベースのレンダリング関数を使用しません。 代わりに、XPSDrv プリンター ドライバーのレンダリングのモジュールは、0 個以上のフィルターと各フィルターのアクションを記述した構成ファイルで構成されます。 XPSDrv プリンター ドライバーのレンダリングのモジュール内のフィルターでは、プリンターの印刷ジョブを正しく処理する印刷チケット テクノロジもサポートする必要があります。

XPSDrv ドライバーのインストールの詳細については、[XPSDrv インストール](xpsdrv-installation.md)を参照してください。

 

 




