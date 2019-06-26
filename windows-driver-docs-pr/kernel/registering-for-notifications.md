---
title: 通知登録
description: 通知登録
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
ms.openlocfilehash: f5e37e58882ae9f7c1040406609fe837c6084b58
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373464"
---
# <a name="registering-for-notifications"></a>通知登録


レジストリの呼び出しをフィルター処理するドライバーをフィルター処理、カーネル モードのレジストリは呼び出す必要がありますまず[ **CmRegisterCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-cmregistercallback)または[ **CmRegisterCallbackEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-cmregistercallbackex)を登録する、 [ **RegistryCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ex_callback_function)ルーチン。 (Windows Vista およびそれ以降のオペレーティング システム バージョンでは、ドライバーを使用する必要があります**CmRegisterCallbackEx**の代わりに**CmRegisterCallback**)。

ドライバーが登録した後、 *RegistryCallback* 、日常的な configuration manager によってルーチンを呼び出すスレッドは、レジストリの操作を実行しようとするたびにします。 レジストリの操作を実行するスレッドがユーザー モードのレジストリのルーチンを呼び出すユーザー モード アプリケーションから指定できます (**RegCreateKeyEx**、 **RegOpenKeyEx**など) からドライバーを呼び出すと、カーネル モードのレジストリ ルーチン ([**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey)、 [ **ZwOpenKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopenkey)など)。

大部分の操作には、ドライバー通知を受信できる、configuration manager は、レジストリの操作を処理する前に (、*事前通知*) またはすぐに、操作の完了後 (ただし、構成する前にマネージャーが、呼び出し元に戻ります:、*通知後*)。 ドライバーが受信可能な通知の種類の一覧は、次を参照してください。 [ **REG\_通知\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ne-wdm-_reg_notify_class)します。

ドライバーが呼び出された後**CmRegisterCallback**または**CmRegisterCallbackEx**、ドライバーは、それを呼び出すまで、通知を受け取る[ **CmUnRegisterCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-cmunregistercallback)またはアンロードされています。

 

 




