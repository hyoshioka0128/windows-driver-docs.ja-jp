---
title: シングル デバイス スタックでの操作フロー
description: シングル デバイス スタックでの操作フロー
ms.assetid: b7e38844-2e00-48b8-9741-3bfc38869a6d
keywords:
- 単一デバイススタックフロー WDK UMDF
- 操作フロー WDK UMDF
- I/o 要求 WDK UMDF、操作フロー
- 要求の処理 WDK UMDF、操作フロー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cff476c6177d879e00438a1e57e6196e03cd47f
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210876"
---
# <a name="operation-flow-with-single-device-stack"></a>シングル デバイス スタックでの操作フロー


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

次の図は、1つのデバイススタックで、UMDF 機能ドライバーとの間で発生する操作のフローを示しています。

![create file の後に読み取り要求を行うための umdf 呼び出しシーケンス](images/umdfflow.gif)

アプリケーションによって開始されるすべての i/o は、前の図にはこのような状況が示されていませんが、「UMDF」セクション[のアーキテクチャ](https://docs.microsoft.com/previous-versions/ff554461(v=vs.85))の図に示すように、カーネルモード経由でルーティングさ**れる   ます**。

 

UMDF ドライバーは、読み取り要求に関連付けられているファイルに関する情報が必要な場合にのみ、 [**IWDFIoRequest:: GetCreateParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getcreateparameters)メソッドを呼び出します。 UMDF ドライバーは、読み取り要求に関する詳細情報が必要な場合にのみ、 [**IWDFIoRequest:: GetReadParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-getreadparameters)メソッドを呼び出します。

UMDF ドライバーは、読み取り操作で転送されるバイト数を指定する必要がない場合に、 [**IWDFIoRequest:: CompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation)メソッドではなく[**IWDFIoRequest:: Complete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-complete)メソッドを呼び出すことができます。 UMDF ドライバーは、**完了**または**completewithinformation**を呼び出して、読み取り操作が完了したことを通知します。その後、アプリケーションは読み取りデータにアクセスできます。

 

 





