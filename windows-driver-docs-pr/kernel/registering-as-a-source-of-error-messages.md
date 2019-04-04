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
ms.openlocfilehash: b22a2fed4cacaec5eac40c9c61b15084f11c493f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574071"
---
# <a name="registering-as-a-source-of-error-messages"></a>エラー メッセージのソースとしての登録





ドライバーは、レジストリにエラー メッセージのソースを登録します。 ドライバーは、下の 2 つのキーを設定する必要があります**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\サービス\\EventLog\\システム\\** <em>DriverName</em>:

<a href="" id="eventmessagefile--reg-expand-sz-"></a>**EventMessageFile** (REG\_展開\_SZ)  
セミコロンで区切られたエラー メッセージのソースの一覧。 ドライバーは、標準エラーの種類を使用している場合、この一覧は iologmsg.dll を含める必要があります。 ドライバーがドライバーのイメージに接続されているエラー メッセージを使用する場合、ドライバーのイメージの名前をこの必要があります。

<a href="" id="typessupported--reg-dword-"></a>**TypesSupported** (REG\_DWORD)  
ログに記録できる可能性の重大度レベルのビットマスクを指定します。 これは、ドライバーが通常設定から 7 を示すすべての重大度レベルを記録することがあります。

ドライバーの INF ファイルからこれらのレジストリ キーを設定する方法については、[**登録イベントをログに記録**](https://msdn.microsoft.com/library/windows/hardware/ff546326)を参照してください。

 

 




