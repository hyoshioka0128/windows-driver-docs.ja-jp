---
title: ConvertDevModeToPrintTicket の概要
description: ConvertDevModeToPrintTicket メソッドがプラグインがインストールされた印刷ドライバーごとに呼び出されます。
ms.assetid: 71387d8b-60ce-4deb-a20b-9d7b0b7be230
keywords:
- ConvertDevModeToPrintTicket
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e1575700126bd6e775f7519cc5f53dc1acabf2d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557738"
---
# <a name="convertdevmodetoprintticket-overview"></a>ConvertDevModeToPrintTicket の概要


Unidrv と PScript5 の印刷ドライバーは、パブリックおよびプライベートの部分から要素を使用して印刷チケットを作成、 [ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)ドライバーをサポートする構造体。 [ **IPrintOemPrintTicketProvider::ConvertDevModeToPrintTicket** ](https://msdn.microsoft.com/library/windows/hardware/ff553161)各印刷ドライバーのプラグインがインストールされているメソッドが呼び出されます。

次の図は、ドライバーが ConvertDevModeToPrintTicket を呼び出すときに、IPrintOemPrintTicketProvider::ConvertDevModeToPrintTicket への呼び出しの順序を示します。

![convertdevmodetoprintticket 呼び出しシーケンス](images/ptpcdm2pt-uml.gif)

 

 




