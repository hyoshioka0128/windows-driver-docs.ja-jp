---
title: フレームワーク オブジェクトのメソッド
description: フレームワーク オブジェクトのメソッド
ms.assetid: f82275c5-15f9-43f5-91bb-b83446526c28
keywords:
- フレームワークオブジェクト WDK KMDF、メソッド
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c17fa1b066809e2b0a0ba866d8279804ecaab829
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845139"
---
# <a name="framework-object-methods"></a>フレームワーク オブジェクトのメソッド





各フレームワークオブジェクトは、一連のメソッド (functions) をエクスポートします。 各方法には、次の2つの目的があります。

-   オブジェクトに関連付けられているアクションを実行します。

    たとえば、 [**WdfIoQueueCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfio/nf-wdfio-wdfioqueuecreate)メソッドは、デバイスの i/o キューを作成します。

    通常、アクションを実行するメソッドは、 [NTSTATUS 値](https://docs.microsoft.com/windows-hardware/drivers/kernel/ntstatus-values)を返します。

-   オブジェクトに関連付けられている[プロパティ](framework-object-properties.md)を取得または変更します。

    たとえば、 [**Wdfrequestgetinformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestgetinformation)メソッドは、i/o 要求の完了ステータスに関する情報を返します。

    プロパティを取得するメソッドは通常、プロパティの値を返しますが、プロパティを変更するメソッドは通常、値を返しません。

各オブジェクトメソッドは、オブジェクトハンドルを入力として受け取ります。 ドライバーが無効なオブジェクトハンドルをオブジェクトメソッドに渡すと、システムのバグチェックが行われます。

 

 





