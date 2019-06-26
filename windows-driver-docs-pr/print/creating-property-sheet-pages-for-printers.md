---
title: プリンターのプロパティ シート ページを作成する
description: プリンターのプロパティ シート ページを作成する
ms.assetid: b9b7aa52-39b7-4809-acdf-e72293da37e1
keywords:
- プリンター インターフェイス DLL の WDK、プロパティ シートのページ
- WDK のプロパティ シート ページが印刷を作成します。
- WDK プロパティ シートのページを印刷するプリンター インターフェイス DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 085c50d5d3335cc718f4d5737ddc59f728741f19
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372442"
---
# <a name="creating-property-sheet-pages-for-printers"></a>プリンターのプロパティ シート ページを作成する





組み合わせて、プリンター インターフェイス Dll [CPSUI](common-property-sheet-user-interface.md)は Windows 2000 のユーザーがプロパティ シートのページを作成し、後で表示およびプリンターに関連付けられている構成パラメーターを変更するために使用および印刷ドキュメント。 各プリンター インターフェイスの DLL を指定する必要があります、 [ **DrvDevicePropertySheets** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdevicepropertysheets)プリンター固有のページを作成する関数と[ **DrvDocumentPropertySheets**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvdocumentpropertysheets)ドキュメント固有のページを作成する関数。

これらの関数の設計方法を理解するのには説明するセクションを読み取る必要が[CPSUI](common-property-sheet-user-interface.md)します。 プロパティ シートのページを表示するには、アプリケーション、印刷スプーラー、プリンター インターフェイス DLL、および CPSUI 間の相互作用する必要があります。 実行の流れについては、「[プリンター ドライバーを使用して CPSUI](using-cpsui-with-printer-drivers.md)します。

 

 




