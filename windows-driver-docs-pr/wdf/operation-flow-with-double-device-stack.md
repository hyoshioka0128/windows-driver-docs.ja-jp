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
ms.openlocfilehash: 2ef4cb237dbc35d99d7111c8b7ba40f9f66eeda7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573112"
---
# <a name="operation-flow-with-double-device-stack"></a>ダブル デバイス スタックでの操作フロー


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

次の図は、UMDF フィルターおよび二重デバイス スタックの機能のドライバーとの間に発生する操作の流れを示しています。

![umdf フィルター ドライバーおよび umdf function ドライバーの umdf i/o 呼び出しシーケンス](images/umdfflow2.gif)

**注**  の図に示すように、カーネル モードでアプリケーションによって開始されるすべての I/O がルーティングされます、 [、UMDF のアーキテクチャ](https://msdn.microsoft.com/library/windows/hardware/ff554461)セクションで、上記の図にこのような状況が表示されない場合でも.

 

UMDF フィルターと関数のドライバーが呼び出すことも、 [ **IWDFIoRequest::GetCreateParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff559088)メソッドの場合は、読み取り要求に関連付けられているファイルに関する情報が必要です。 UMDF フィルターと関数のドライバーが呼び出すことも、 [ **IWDFIoRequest::GetReadParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff559113)メソッドの詳細については、読み取り要求は必要がある場合。

UMDF ドライバーの機能の呼び出し、 [ **IWDFIoRequest::Complete** ](https://msdn.microsoft.com/library/windows/hardware/ff559070)または[ **IWDFIoRequest::CompleteWithInformation** ](https://msdn.microsoft.com/library/windows/hardware/ff559074)メソッド読み取り操作が終了するフィルター ドライバーに通知します。 UMDF フィルター ドライバーがのメソッドを呼び出すことも、 [IWDFIoRequestCompletionParams](https://msdn.microsoft.com/library/windows/hardware/ff559055)インターフェイスの詳細については、読み取り要求を完了する必要がある場合。 UMDF ドライバー呼び出しをフィルター処理**完了**または**CompleteWithInformation**読み取り操作が完了したシグナルは、アプリケーションは、読み取りデータへのアクセスにします。

 

 





