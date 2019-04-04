---
title: 通知を登録します。
description: 通知を登録します。
ms.assetid: 06109726-77e8-49de-9486-4fa2a5aceb1c
keywords:
- 通知の登録、レジストリ呼び出し WDK カーネルをフィルター処理
- レジストリのフィルター ドライバー WDK カーネル、通知を登録します。
- フィルターのレジストリの呼び出しの通知を登録します。
- 前の通知オプション WDK フィルター レジストリ呼び出し
- 通知後オプション WDK フィルター レジストリ呼び出し
- WDK の通知がレジストリの呼び出しをフィルター処理します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d05a12dd9048ba3a7949ba45556ca89d70117f8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531702"
---
# <a name="registering-for-notifications"></a>通知を登録します。


レジストリの呼び出しをフィルター処理するドライバーをフィルター処理、カーネル モードのレジストリは呼び出す必要がありますまず[ **CmRegisterCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff541918)または[ **CmRegisterCallbackEx** ](https://msdn.microsoft.com/library/windows/hardware/ff541921)を登録する、 [ **RegistryCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff560903)ルーチン。 (Windows Vista およびそれ以降のオペレーティング システム バージョンでは、ドライバーを使用する必要があります**CmRegisterCallbackEx**の代わりに**CmRegisterCallback**)。

ドライバーが登録した後、 *RegistryCallback* 、日常的な configuration manager によってルーチンを呼び出すスレッドは、レジストリの操作を実行しようとするたびにします。 レジストリの操作を実行するスレッドがユーザー モードのレジストリのルーチンを呼び出すユーザー モード アプリケーションから指定できます (**RegCreateKeyEx**、 **RegOpenKeyEx**など) からドライバーを呼び出すと、カーネル モードのレジストリ ルーチン ([**ZwCreateKey**](https://msdn.microsoft.com/library/windows/hardware/ff566425)、 [ **ZwOpenKey**](https://msdn.microsoft.com/library/windows/hardware/ff567014)など)。

大部分の操作には、ドライバー通知を受信できる、configuration manager は、レジストリの操作を処理する前に (、*事前通知*) またはすぐに、操作の完了後 (ただし、構成する前にマネージャーが、呼び出し元に戻ります:、*通知後*)。 ドライバーが受信可能な通知の種類の一覧は、[ **REG\_通知\_クラス**](https://msdn.microsoft.com/library/windows/hardware/ff560950)を参照してください。

ドライバーが呼び出された後**CmRegisterCallback**または**CmRegisterCallbackEx**、ドライバーは、それを呼び出すまで、通知を受け取る[ **CmUnRegisterCallback**](https://msdn.microsoft.com/library/windows/hardware/ff541928)またはアンロードされています。

 

 




