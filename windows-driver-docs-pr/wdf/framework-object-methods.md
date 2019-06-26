---
title: フレームワーク オブジェクトのメソッド
description: フレームワーク オブジェクトのメソッド
ms.assetid: f82275c5-15f9-43f5-91bb-b83446526c28
keywords:
- framework オブジェクト WDK KMDF、メソッド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dd19a2818854f2bd820c59e480463d651881283
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384459"
---
# <a name="framework-object-methods"></a>フレームワーク オブジェクトのメソッド





Framework の各オブジェクトは、一連のメソッド (関数) をエクスポートします。 各メソッドは、2 つの目的の 1 つがあります。

-   オブジェクトに関連付けられているアクションを実行します。

    たとえば、 [ **WdfIoQueueCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfio/nf-wdfio-wdfioqueuecreate)メソッドがデバイスの I/O キューを作成します。

    通常、アクションを実行するメソッドを返す、 [NTSTATUS 値](https://docs.microsoft.com/windows-hardware/drivers/kernel/ntstatus-values)します。

-   これを取得または変更、[プロパティ](framework-object-properties.md)オブジェクトに関連付けられています。

    たとえば、 [ **WdfRequestGetInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfrequest/nf-wdfrequest-wdfrequestgetinformation)メソッドは、I/O 要求の完了ステータスに関する情報を返します。

    通常のプロパティを取得メソッドは、通常、プロパティを変更するメソッドは、値を返しません。 中に、プロパティの値を返します。

各オブジェクトのメソッドは、オブジェクト ハンドルを入力として受け取ります。 オブジェクトのメソッドに、ドライバーが、無効なオブジェクトのハンドルを渡すと、システムのバグ チェックが発生します。

 

 





