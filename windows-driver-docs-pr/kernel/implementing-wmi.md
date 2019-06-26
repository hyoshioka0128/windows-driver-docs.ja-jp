---
title: WMI の実装
description: WMI の実装
ms.assetid: 5c2ed322-0fc9-4004-9a5f-f4d3c6a59fe9
keywords:
- WMI の WDK カーネル
- Windows Management Instrumentation の WDK カーネル
- WDK WMI 拡張機能
- 計測データ WDK WMI
- WDK の WMI のインストルメンテーション データ
- ユーザー モード WMI WDK
- WMI の WDK ユーザー モード
- Windows Management Instrumentation の WDK ユーザー モード
- カーネル モード ドライバー WDK、WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04acc37c917bf9cea64911c945d1599da081c227
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369802"
---
# <a name="implementing-wmi"></a>WMI の実装





このセクションでは、カーネル モードでは、Windows Management Instrumentation (WMI) の WDM 拡張機能について説明します。 カーネル モード ドライバーにこれらの拡張機能を追加すると、ドライバーは、WMI プロバイダーになります。 WMI プロバイダーでは、ユーザー モード アプリケーションなどの WMI コンシューマーに使用可能な測定値とインストルメンテーション データをようにします。

ユーザー モードの WMI API の詳細についてを参照してください[Windows Management Instrumentation](https://docs.microsoft.com/windows/desktop/WmiSdk/wmi-start-page) Windows SDK に含まれています。

KMDF ドライバーを実装する場合を参照してください[Framework ベースのドライバーでサポートしている WMI](https://docs.microsoft.com/windows-hardware/drivers/wdf/supporting-wmi-in-kmdf-drivers)します。

このセクションには、カーネル モードの WMI の詳細については、次の情報が含まれています。

[WMI の概要](introduction-to-wmi.md)

[WMI アーキテクチャ](wmi-architecture.md)

[WDM ドライバーの WMI の要件](wmi-requirements-for-wdm-drivers.md)

[WMI データとイベント ブロックの MOF 構文](mof-syntax-for-wmi-data-and-event-blocks.md)

[WMI データとイベント ブロックの設計](designing-wmi-data-and-event-blocks.md)

[WMI スキーマの公開](publishing-a-wmi-schema.md)

[WMI データ プロバイダーとして登録します。](registering-as-a-wmi-data-provider.md)

[WMI の要求の処理](handling-wmi-requests.md)

[WMI イベントの送信](sending-wmi-events.md)

[WMI プロパティ シート](wmi-property-sheets.md)

[Wmimofck.exe を使用します。](using-wmimofck-exe.md)

[WMI イベントのトレース](wmi-event-tracing.md)

[テストとドライバー サポートの WMI のトラブルシューティング](testing-and-troubleshooting-wmi-driver-support.md)

 

 




