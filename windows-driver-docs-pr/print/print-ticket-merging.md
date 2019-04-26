---
title: 印刷チケット結合
description: 印刷チケット結合
ms.assetid: 2d9cf4d3-5c73-4355-b5e0-effcfb7102cc
keywords:
- XPSDrv プリンター ドライバー WDK、モジュールを表示します。
- モジュール WDK XPSDrv、印刷チケットを表示します。
- 印刷チケット WDK、XPSDrv プリンター ドライバー
- 印刷チケット オブジェクトのマージ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e49acda9d9b06ac9a237061812545716df3e1f6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341896"
---
# <a name="print-ticket-merging"></a>印刷チケット結合


印刷ドライバーで処理 PrintTicket オブジェクトでは、関連付けられているドキュメントの一部に基づいた階層関係があります。 次の図は、XPS ドキュメント内のこれらの部分の関係を示しています。

![xps ドキュメント内のドキュメント パーツを示す図](images/ptpcxps1.gif)

印刷チケット レベルの階層では、別のスコープがあります。 印刷チケット情報を使用する印刷ドライバーのフィルター モジュールは、オブジェクトは、ドキュメント ストリームから読み取ら印刷チケットとそのスコープを維持する必要があります。 次の図は、これを実行して印刷ドライバーのフィルター モジュールで方法を示します。

![方法、さまざまな印刷チケットのレベルを示すダイアグラムが論理的にマージされます。 ](images/ptpcxps2.gif)

文書パーツは、フィルターによって読み取られる、印刷チケット オブジェクトは読み取りと、マージし検証され、フィルターがドキュメントの各部を処理する方法を構成するためのフィルターによってキャッシュします。 前の図は、さまざまな印刷チケット レベルが論理的にマージされる方法を示していて、次の擬似コードはこのマージを実装する方法を示しています。

```cpp
class Filter
{
 PrintTicket Saved_FDS_PT;
 PrintTicket Saved_FD_PT;

 ProcessFDS(pIFixedDocumentSequence)
    {
 Saved_FDS_PT = pIFixedDocumentSequence->GetPrintTicket();

        // continue processing the FixedDocumentSequence part
    }

 ProcessFD(pIFixedDocument)
    {
 Saved_FD_PT->Release();

        temp = pIFixedDocument->GetPrintTicket();

 Saved_FD_PT = PrintTicketMergeAndValidate(
 Saved_FDS_PT, temp);

        // continue processing the FixedDocument part
    }

 ProcessPage(IFixedPage)
    {
        temp = pIFixedPage->GetPrintTicket();

 PagePT = PrintTicketMergeAndValidate(Saved_FD_PT, temp);

        // continue processing the FixedPage part
    }

 PrintTicket PrintTicketMergeAndValidate(
 ParentPT,
 PartPT)
    {
        // Entries in the Part PrintTicket 
        // take precedence over the corresponding entries 
        // in the Parent PrintTicket
    }
};
```

 

 




