---
title: V4 プリンター ドライバー ユーザー インターフェイス
description: V4 印刷ドライバーでは、Windows デスクトップ UI と Microsoft Store アプリの UI の両方でカスタマイズをサポートします。
ms.assetid: DE45C0F3-3385-451D-AD29-94D28089E9C3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c774c757e963a48393d22a7b36421ea88d042a60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324837"
---
# <a name="v4-printer-driver-user-interfaces"></a>V4 プリンター ドライバー ユーザー インターフェイス


V4 印刷ドライバーでは、Windows デスクトップ UI と Microsoft Store アプリの UI の両方でカスタマイズをサポートします。

これらのエクスペリエンスの非常にさまざまな性質には、2 つのアプリケーションとしてこれらの Ui を実装する必要があります。 ただし、両方は、構成のモジュールによって提供される一般的な COM API に基づいて構築します。 プリンター拡張機能では、デスクトップで v4 プリンター ドライバーをサポートし、既存のすべてのアプリケーションを使用します。 プリンターの拡張機能は、プリンターの共有が強化されたポイント アンド プリント ドライバーを使用したシナリオでも動作します。 Windows 8 から Windows Vista からのすべてのオペレーティング システムのサポートが予定されています。

UWP デバイス アプリでは、Microsoft Store アプリの UI で v4 印刷ドライバーをサポートします。 UWP デバイス アプリの開発に関する詳細については、次を参照してください。[印刷デバイス アプリを UWP を開発](https://msdn.microsoft.com/library/windows/hardware/br259129.aspx)します。

次の図は、カスタマイズした Ui と印刷システムの間の通信アーキテクチャの高レベルな概要を示します。

![カスタムの ui と印刷システムの通信の概要](images/v4customuicomms.png)

次のトピックでは、ユーザー インターフェイスの v4 印刷ドライバーのサポートの詳細についてを説明します。

[V4 ドライバー UI のアーキテクチャ](v4-driver-ui-architecture.md)

[カスタマイズした UI のドライバー サポート](driver-support-for-customized-ui.md)

[ジョブの管理](job-management.md)

[デバイスのメンテナンス](device-maintenance.md)

[プリンターの拡張機能](printer-extensions.md)

[プリンター用の UWP デバイス アプリ](uwp-device-apps-for-printers.md)

## <a name="related-topics"></a>関連トピック
[V4 プリンター ドライバー](v4-printer-driver.md)  



