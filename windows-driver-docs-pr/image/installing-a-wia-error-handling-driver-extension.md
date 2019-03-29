---
title: WIA エラー処理ドライバーの拡張機能のインストール
description: WIA エラー処理ドライバーの拡張機能のインストール
ms.assetid: 8a16b0db-25ed-4512-8b45-0256fed6b83e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 42239d5ce8c1a6b002e0218e0ad0d14c9592f721
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581596"
---
# <a name="installing-a-wia-error-handling-driver-extension"></a>WIA エラー処理ドライバーの拡張機能のインストール


エラー処理拡張機能は、WIA ドライバーと共にインストールする必要があります。 ドライバーとドライバーのエラー ハンドラーをインストールするには、ドライバーの INF ファイルを少数の追加を行う必要があります。

次の例では、エラー ハンドラーを含めるように、既存のドライバーの INF ファイルを変更する方法を示します。

```INF
MyDriver.AddReg]
...
HKCR,CLSID\{UiClassId}\shellex\ErrorHandler\{ErrorHandlerCLSID}
...
HKCR,CLSID\{ErrorHandlerCLSID },,,"My Error Handler"
HKCR,CLSID\{ErrorHandlerCLSID }\InProcServer32,,,%11%\myerrhandler.dll
HKCR,CLSID\{ErrorHandlerCLSID }\InProcServer32,ThreadingModel,,"Both"
...

[MyDriver.CopyFiles]
...
myerrhandler.dll
...

[SourceDisksFiles.x86]
...
myerrhandler.dll=1
...
```

{UiClassId} のクラス ID は、ドライバー、WIA から返される値\_DIP\_UI\_CLSID プロパティと {ErrorHandlerCLSID} は、エラー ハンドラーのクラス ID。 この例で*myerrhandler.dll*エラー ハンドラーの実装が含まれています。

最初のエントリで、 **AddReg**セクションでは、ドライバーの WIA 拡張機能として、エラー ハンドラーを登録します。 次の 3 つのエントリは、COM コンポーネントとして、エラー ハンドラーを登録します。

*ThreadingModel*値、エラー処理拡張機能である必要があります**両方**します。

 

 




