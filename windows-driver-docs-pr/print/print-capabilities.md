---
title: 印刷機能
description: 印刷機能
ms.assetid: 8ccbdab3-5be4-4ee1-9798-3b90e8b5b4d4
keywords:
- 印刷機能 WDK、印刷機能の詳細
- XML PrintCapabilities WDK の印刷
- PrintCapabilities ドキュメントを WDK の印刷
- IPrintTicketProvider
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e9ce7aa80bd5a3d552d751a0ee6df8991f63ec1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389481"
---
# <a name="print-capabilities"></a>印刷機能


印刷機能のテクノロジを使用すると、印刷ドライバーは、XML ドキュメント内の要素のセットとしてその機能を返すことができます。 印刷ドライバーの以前のバージョン、アプリケーションが呼び出されたときに、機能の情報が返される、 **DeviceCapabilities**または**調べるため**関数。 ただし、プリンターの機能と設定の固定セットに関する唯一の情報を返すし、1 つだけの機能または関数呼び出しごとの設定に関する情報を返すことができますので、これらの Microsoft Win32 関数は制限されています。

これに対し、XML PrintCapabilities ドキュメントが非常に優れた柔軟性は、新しいプリンターの機能をサポートするために設計されています。 PrintCapabilities 関数は、1 つの関数の呼び出しでも XML PrintCapabilities ドキュメント全体を返します。

このセクションでは、印刷機能の次の側面について説明します。

[印刷機能のアーキテクチャ](print-capabilities-architecture.md)

[印刷機能の Win32 API のサポート](win32-api-support-for-print-capabilities.md)

[印刷 Unidrv と PScript5 印刷ドライバーの機能](print-capabilities-in-unidrv-and-pscript5-print-drivers.md)

[プリンター ドライバー プラグインのサポート](print-driver-plug-in-support.md)

[モノリシック、GDI ベースのプリンター ドライバーでの印刷機能のサポート](print-capabilities-support-in-gdi-based--monolithic-print-drivers.md)

 

 




