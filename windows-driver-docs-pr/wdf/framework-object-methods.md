---
title: フレームワーク オブジェクトのメソッド
description: フレームワーク オブジェクトのメソッド
ms.assetid: f82275c5-15f9-43f5-91bb-b83446526c28
keywords:
- framework オブジェクト WDK KMDF、メソッド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a9954c646788651ed1045fa64c60193adf82c53
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370978"
---
# <a name="framework-object-methods"></a>フレームワーク オブジェクトのメソッド





Framework の各オブジェクトは、一連のメソッド (関数) をエクスポートします。 各メソッドは、2 つの目的の 1 つがあります。

-   オブジェクトに関連付けられているアクションを実行します。

    たとえば、 [ **WdfIoQueueCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff547401)メソッドがデバイスの I/O キューを作成します。

    通常、アクションを実行するメソッドを返す、 [NTSTATUS 値](https://msdn.microsoft.com/library/windows/hardware/ff557697)します。

-   これを取得または変更、[プロパティ](framework-object-properties.md)オブジェクトに関連付けられています。

    たとえば、 [ **WdfRequestGetInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff549965)メソッドは、I/O 要求の完了ステータスに関する情報を返します。

    通常のプロパティを取得メソッドは、通常、プロパティを変更するメソッドは、値を返しません。 中に、プロパティの値を返します。

各オブジェクトのメソッドは、オブジェクト ハンドルを入力として受け取ります。 オブジェクトのメソッドに、ドライバーが、無効なオブジェクトのハンドルを渡すと、システムのバグ チェックが発生します。

 

 





