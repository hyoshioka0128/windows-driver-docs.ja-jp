---
title: ConvertPrintTicketToDevMode 概要
description: アプリケーションの印刷チケットの渡されたから IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode メソッドの使用状況をについて説明します。
ms.assetid: dd77d79e-e274-47c3-9bfd-95054bc9f23d
keywords:
- ConvertPrintTicketToDevMode
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d3b3ce6e3e4fa0ac7392810fb31ef7e5942f9ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579192"
---
# <a name="convertprinttickettodevmode-overview"></a>ConvertPrintTicketToDevMode 概要


Unidrv と PScript5 印刷ドライバーをパブリックおよびプライベートな部分の入力、 [ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)から渡されたアプリケーションの印刷チケット情報を使用してサポートされる構造体ConvertPrintTicketToDevMode を呼び出します。 [ **IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode** ](https://msdn.microsoft.com/library/windows/hardware/ff553167)各印刷ドライバーのプラグインがインストールされているメソッドが呼び出されます。

次の図への呼び出しの順序**IPrintOemPrintTicketProvider::ConvertPrintTicketToDevMode**ドライバーを呼び出すと**ConvertPrintTicketToDevMode**します。

![呼び出しシーケンス convertprinttickettodevmode を示す図](images/ptpcpt2dm-uml.gif)





