---
title: ConvertDevModeToPrintTicket 概要
description: ConvertDevModeToPrintTicket メソッドがプラグインがインストールされた印刷ドライバーごとに呼び出されます。
ms.assetid: 71387d8b-60ce-4deb-a20b-9d7b0b7be230
keywords:
- ConvertDevModeToPrintTicket
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6d07230ca976330dd9f45683661227bc767bf39
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374668"
---
# <a name="convertdevmodetoprintticket-overview"></a>ConvertDevModeToPrintTicket 概要


Unidrv と PScript5 の印刷ドライバーは、パブリックおよびプライベートの部分から要素を使用して印刷チケットを作成、 [ **DEVMODEW** ](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)ドライバーをサポートする構造体。 [ **IPrintOemPrintTicketProvider::ConvertDevModeToPrintTicket** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff553161(v=vs.85))各印刷ドライバーのプラグインがインストールされているメソッドが呼び出されます。

次の図は、ドライバーが ConvertDevModeToPrintTicket を呼び出すときに、IPrintOemPrintTicketProvider::ConvertDevModeToPrintTicket への呼び出しの順序を示します。

![convertdevmodetoprintticket 呼び出しシーケンス](images/ptpcdm2pt-uml.gif)

 

 




