---
title: 印刷チケットと機能 - Unidrv/Pscript5
description: チケットの印刷し、印刷 Unidrv/Pscript5 プラグインによって実装される機能のプロバイダー インターフェイス
ms.assetid: 00dcbbde-e4e4-4fcc-b69f-9c91051e0e29
keywords:
- Unidrv WDK の印刷
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e6da5595ecae2d97e87cc899815ce9f6e73f31e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551975"
---
# <a name="print-ticket-and-print-capabilities-provider-interface-implemented-by-unidrvpscript5-plug-ins"></a>チケットの印刷し、印刷 Unidrv/Pscript5 プラグインによって実装される機能のプロバイダー インターフェイス


[Microsoft ユニバーサル プリンター ドライバー](microsoft-universal-printer-driver.md) (Unidrv) と[Microsoft PostScript プリンター ドライバー](microsoft-postscript-printer-driver.md) (Pscript5) Windows Vista 上のプリンター ドライバーの中核となる印刷チケットを実装するためにプラグインするための手段を提供します。サポート。 Unidrv と Pscript5 両方サポートため 1 つのドライバーの複数のプラグインを読み込み、各プラグインは独自のプロバイダーの実装を提供できます。 ドライバーのベンダーはの各 OEM プラグインのプロバイダーの実装が正しく動作する、他のことを確認します。 すべてのプリンター ドライバーでプラグインは、プロバイダー インターフェイスをサポートする必要があります。 ただし、core ドライバーによってサポートされている印刷チケットのスキーマのバージョンには、コア ドライバーとそのすべての利用可能なプラグインのプロバイダーでサポートされているバージョンのサブセットです。 プラグインのプロバイダーへの呼び出しは、アプリケーションによって主導別、ために、スレッド セーフ方式でプラグインのプロバイダーを実装する必要があります。

 




