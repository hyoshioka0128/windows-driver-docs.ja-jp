---
title: プリンターのプロパティ シート ページを作成する
description: プリンターのプロパティ シート ページを作成する
ms.assetid: b9b7aa52-39b7-4809-acdf-e72293da37e1
keywords:
- printer interface DLL WDK、プロパティシートページ
- プロパティシートページ WDK 印刷、作成
- プロパティシートページ WDK 印刷、プリンターインターフェイス DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2beb3b66e12e0da3f809a3a43678d33920afbf20
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837725"
---
# <a name="creating-property-sheet-pages-for-printers"></a>プリンターのプロパティ シート ページを作成する





プリンターインターフェイス Dll は、 [CPSUI](common-property-sheet-user-interface.md)と連携して、Windows 2000 以降のユーザーがプリンターや印刷ドキュメントに関連付けられた構成パラメーターを表示および変更するために使用するプロパティシートページを作成します。 各プリンターインターフェイス DLL は、プリンター固有のページを作成するための[**DrvDevicePropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicepropertysheets)関数と、ドキュメント固有のページを作成するための[**DrvDocumentPropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentpropertysheets)関数を提供する必要があります。

これらの関数の設計方法を理解するには、 [CPSUI](common-property-sheet-user-interface.md)について説明するセクションを参照することが重要です。 プロパティシートのページを表示するには、アプリケーション、印刷スプーラ、プリンターインターフェイス DLL、および CPSUI 間の対話が必要です。 実行フローの詳細については、「 [CPSUI とプリンタードライバーの使用](using-cpsui-with-printer-drivers.md)」を参照してください。

 

 




