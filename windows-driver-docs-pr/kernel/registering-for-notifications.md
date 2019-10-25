---
title: 通知登録
description: 通知登録
ms.assetid: 06109726-77e8-49de-9486-4fa2a5aceb1c
keywords:
- レジストリのフィルター処理による WDK カーネルの呼び出し、通知の登録
- レジストリフィルタリングドライバー WDK カーネル、通知の登録
- フィルターレジストリ呼び出し通知を登録しています
- 事前通知オプション WDK フィルタのレジストリ呼び出し
- 通知後オプション WDK フィルターレジストリ呼び出し
- 通知 WDK フィルタのレジストリ呼び出し
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22cd7e06bdd7032e0bf50204019effee2e8806ba
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827479"
---
# <a name="registering-for-notifications"></a>通知登録


レジストリ呼び出しをフィルター処理するには、まず、カーネルモードのレジストリフィルタードライバーが[**cmregistercallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallback)または[**Cmregistercallback ex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmregistercallbackex)を呼び出して、 [**registrycallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ex_callback_function)ルーチンを登録する必要があります。 (Windows Vista 以降のバージョンのオペレーティングシステムの場合、ドライバーは**Cmregistercallback**の代わりに**Cmregistercallback ex**を使用する必要があります)。

ドライバーが*Registrycallback*ルーチンを登録した後、構成マネージャーは、スレッドがレジストリ操作を実行しようとするたびにルーチンを呼び出します。 レジストリ操作を実行するスレッドは、ユーザーモードのレジストリルーチン (**Regcreatekeyex**、 **regopenkeyex が**など) を呼び出すユーザーモードアプリケーションや、カーネルモードのレジストリルーチンを呼び出すドライバー ([**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey)、 [**Zwopenkey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey)など)。

ほとんどの操作では、configuration manager がレジストリ操作 (*事前通知*) を処理する前、または操作が完了した直後 (ただし、configuration manager が呼び出し元-*通知後*)。 ドライバーが受信できる通知の種類の一覧については、「 [**REG\_NOTIFY\_クラス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_reg_notify_class)」を参照してください。

ドライバーが**Cmregistercallback**または**Cmregistercallback ex**を呼び出した後、ドライバーは[**cmunregistercallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-cmunregistercallback)を呼び出すか、またはアンロードされるまで、通知を受信します。

 

 




