---
title: エラー メッセージのソースとしての登録
description: エラー メッセージのソースとしての登録
ms.assetid: 5428950c-9c28-411a-9ec0-b029ad311a00
keywords:
- ソースの登録の WDK エラー
- エラー WDK カーネル
- エラー メッセージのソースの登録
- レジストリの WDK エラー ログ
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec9724a0588d10dae007381b30eb38aa85aa4458
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373478"
---
# <a name="registering-as-a-source-of-error-messages"></a>エラー メッセージのソースとしての登録





ドライバーは、レジストリにエラー メッセージのソースを登録します。 ドライバーは、下の 2 つのキーを設定する必要があります**HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Services\\EventLog\\System\\** <em>DriverName</em>:

<a href="" id="eventmessagefile--reg-expand-sz-"></a>**EventMessageFile** (REG\_展開\_SZ)  
セミコロンで区切られたエラー メッセージのソースの一覧。 ドライバーは、標準エラーの種類を使用している場合、この一覧は iologmsg.dll を含める必要があります。 ドライバーがドライバーのイメージに接続されているエラー メッセージを使用する場合、ドライバーのイメージの名前をこの必要があります。

<a href="" id="typessupported--reg-dword-"></a>**TypesSupported** (REG\_DWORD)  
ログに記録できる可能性の重大度レベルのビットマスクを指定します。 これは、ドライバーが通常設定から 7 を示すすべての重大度レベルを記録することがあります。

ドライバーの INF ファイルからこれらのレジストリ キーを設定する方法については、次を参照してください。 [**登録イベントをログに記録**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)します。

 

 




