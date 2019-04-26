---
title: その他のプリンター インターフェイスの操作をカスタマイズする
description: その他のプリンター インターフェイスの操作をカスタマイズする
ms.assetid: ae59d2e7-9049-432d-b519-9e7c88af8d48
keywords:
- ユーザー インターフェイスにプラグイン WDK 印刷、カスタマイズ メソッド
- UI プラグインの WDK 印刷、カスタマイズ方法
- IPrintOemUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 916fdba3e1a22db48bc95200ed1c88804e15abb9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355676"
---
# <a name="customizing-other-printer-interface-operations"></a>その他のプリンター インターフェイスの操作をカスタマイズする





プラグインの UI は、必要に応じて次 IPrintOemUI メソッドのいずれかに実装できます。

[**IPrintOemUI::DeviceCapabilities**](https://msdn.microsoft.com/library/windows/hardware/ff554162)

[**IPrintOemUI::DevQueryPrintEx**](https://msdn.microsoft.com/library/windows/hardware/ff554172)

[**IPrintOemUI::PrinterEvent**](https://msdn.microsoft.com/library/windows/hardware/ff554182)

[**IPrintOemUI::UpgradePrinter**](https://msdn.microsoft.com/library/windows/hardware/ff554189)

メソッドは、同様に、ユーザー モードでエクスポートされた名前付きの関数に相当[プリンター インターフェイス DLL](printer-interface-dll.md) Unidrv と Pscript5 によって使用されます。 これらのカスタマイズの方法では、ドライバーのプリンター インターフェイス DLL で同等の関数は置き換えられません。 各ケースでプリンター インターフェイス DLL 関数が最初に呼び出されないし、ドライバーがプラグのカスタマイズ メソッドを呼び出します。

 

 




