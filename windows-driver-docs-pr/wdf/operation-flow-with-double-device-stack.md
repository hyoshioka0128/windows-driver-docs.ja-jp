---
title: ダブル デバイス スタックでの操作フロー
description: ダブル デバイス スタックでの操作フロー
ms.assetid: a717b9c0-b24a-4347-8b0a-254a17238b5f
keywords:
- 操作フロー WDK UMDF
- I/O 要求の WDK UMDF、操作フロー
- 要求の WDK UMDF、操作のフローの処理
- 二重デバイス スタック フロー WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04bfb9e87e2df17ffaa938e7c666e580d63179d3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375073"
---
# <a name="operation-flow-with-double-device-stack"></a>ダブル デバイス スタックでの操作フロー


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

次の図は、UMDF フィルターおよび二重デバイス スタックの機能のドライバーとの間に発生する操作の流れを示しています。

![umdf フィルター ドライバーおよび umdf function ドライバーの umdf i/o 呼び出しシーケンス](images/umdfflow2.gif)

**注**  の図に示すように、カーネル モードでアプリケーションによって開始されるすべての I/O がルーティングされます、 [、UMDF のアーキテクチャ](https://docs.microsoft.com/previous-versions/ff554461(v=vs.85))セクションで、上記の図にこのような状況が表示されない場合でも.

 

UMDF フィルターと関数のドライバーが呼び出すことも、 [ **IWDFIoRequest::GetCreateParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-getcreateparameters)メソッドの場合は、読み取り要求に関連付けられているファイルに関する情報が必要です。 UMDF フィルターと関数のドライバーが呼び出すことも、 [ **IWDFIoRequest::GetReadParameters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-getreadparameters)メソッドの詳細については、読み取り要求は必要がある場合。

UMDF ドライバーの機能の呼び出し、 [ **IWDFIoRequest::Complete** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-complete)または[ **IWDFIoRequest::CompleteWithInformation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-completewithinformation)メソッド読み取り操作が終了するフィルター ドライバーに通知します。 UMDF フィルター ドライバーがのメソッドを呼び出すことも、 [IWDFIoRequestCompletionParams](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiorequestcompletionparams)インターフェイスの詳細については、読み取り要求を完了する必要がある場合。 UMDF ドライバー呼び出しをフィルター処理**完了**または**CompleteWithInformation**読み取り操作が完了したシグナルは、アプリケーションは、読み取りデータへのアクセスにします。

 

 





