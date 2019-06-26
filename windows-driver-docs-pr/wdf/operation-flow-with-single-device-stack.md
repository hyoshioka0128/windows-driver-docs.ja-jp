---
title: シングル デバイス スタックでの操作フロー
description: シングル デバイス スタックでの操作フロー
ms.assetid: b7e38844-2e00-48b8-9741-3bfc38869a6d
keywords:
- 1 つのデバイス スタック フロー WDK UMDF
- 操作フロー WDK UMDF
- I/O 要求の WDK UMDF、操作フロー
- 要求の WDK UMDF、操作のフローの処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be9e629f9a11b5ac09c684e6810209ac9f518431
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375056"
---
# <a name="operation-flow-with-single-device-stack"></a>シングル デバイス スタックでの操作フロー


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

次の図と UMDF 機能ドライバーを 1 つのデバイス スタック内の間に発生する操作の流れを示しています。

![ファイルの作成後、読み取り要求の呼び出しシーケンスを umdf](images/umdfflow.gif)

**注**  の図に示すように、カーネル モードでアプリケーションによって開始されるすべての I/O がルーティングされます、 [、UMDF のアーキテクチャ](https://docs.microsoft.com/previous-versions/ff554461(v=vs.85))セクションで、上記の図にこのような状況が表示されない場合でも.

 

UMDF ドライバーの呼び出し、 [ **IWDFIoRequest::GetCreateParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-getcreateparameters)メソッド、読み取り要求に関連付けられているファイルに関する情報が必要な場合のみです。 UMDF ドライバーの呼び出し、 [ **IWDFIoRequest::GetReadParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-getreadparameters)メソッドの詳細については、読み取り要求は必要な場合のみです。

UMDF ドライバーを呼び出すことができます、 [ **IWDFIoRequest::Complete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-complete)メソッドではなく、 [ **IWDFIoRequest::CompleteWithInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation)読み取り操作で転送されるバイト数を指定する場合、メソッドは必要ありません。 UMDF ドライバー呼び出し**完了**または**CompleteWithInformation**読み取り操作が完了したシグナルは、アプリケーションは、読み取りデータへのアクセスにします。

 

 





