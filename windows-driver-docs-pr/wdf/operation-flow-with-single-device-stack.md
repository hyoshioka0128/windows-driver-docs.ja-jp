---
title: スタックの 1 つのデバイスでの操作フロー
description: スタックの 1 つのデバイスでの操作フロー
ms.assetid: b7e38844-2e00-48b8-9741-3bfc38869a6d
keywords:
- 1 つのデバイス スタック フロー WDK UMDF
- 操作フロー WDK UMDF
- I/O 要求の WDK UMDF、操作フロー
- 要求の WDK UMDF、操作のフローの処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8f8a9f7767ab02f08483303512e5443a5cb740f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548681"
---
# <a name="operation-flow-with-single-device-stack"></a>スタックの 1 つのデバイスでの操作フロー


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

次の図と UMDF 機能ドライバーを 1 つのデバイス スタック内の間に発生する操作の流れを示しています。

![ファイルの作成後、読み取り要求の呼び出しシーケンスを umdf](images/umdfflow.gif)

**注**  の図に示すように、カーネル モードでアプリケーションによって開始されるすべての I/O がルーティングされます、 [、UMDF のアーキテクチャ](https://msdn.microsoft.com/library/windows/hardware/ff554461)セクションで、上記の図にこのような状況が表示されない場合でも.

 

UMDF ドライバーの呼び出し、 [ **IWDFIoRequest::GetCreateParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff559088)メソッド、読み取り要求に関連付けられているファイルに関する情報が必要な場合のみです。 UMDF ドライバーの呼び出し、 [ **IWDFIoRequest::GetReadParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff559113)メソッドの詳細については、読み取り要求は必要な場合のみです。

UMDF ドライバーを呼び出すことができます、 [ **IWDFIoRequest::Complete** ](https://msdn.microsoft.com/library/windows/hardware/ff559070)メソッドではなく、 [ **IWDFIoRequest::CompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559074)読み取り操作で転送されるバイト数を指定する場合、メソッドは必要ありません。 UMDF ドライバー呼び出し**完了**または**CompleteWithInformation**読み取り操作が完了したシグナルは、アプリケーションは、読み取りデータへのアクセスにします。

 

 





