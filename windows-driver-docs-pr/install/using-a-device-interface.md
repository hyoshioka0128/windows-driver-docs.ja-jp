---
title: デバイスのインターフェイスを使用します。
description: デバイスのインターフェイスを使用します。
ms.assetid: a41f9ae2-6128-43e2-a6b5-4d0bd45371bd
keywords:
- インターフェイス クラス WDK デバイスのインストール
- デバイスのインターフェイス クラス WDK デバイスのインストール
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ec0ae9ba565aad37e6c5312ce6353bfb29d6ced2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531510"
---
# <a name="using-a-device-interface"></a>デバイスのインターフェイスを使用します。





デバイスのインターフェイスは、カーネル モード コンポーネントとユーザー モード アプリケーションの両方に使用します。 ユーザー モード コードで使用できる **SetupDi * * * Xxx*関数について説明する登録されている、デバイスのインターフェイスを有効にします。 参照してください[SetupDi デバイス インターフェイス関数](using-device-installation-functions.md#ddk-setupdi-device-interface-functions-dg)詳細についてはします。

カーネル モード コンポーネントには、特定のデバイスまたはファイル オブジェクトを使用できます、前に、次の操作する必要があります。

1.  必要なデバイスのインターフェイス クラスが登録され、有効になっているかどうかを決定します。

    ドライバー、PnP マネージャー デバイス インターフェイスのインスタンスを有効または無効になっているときに通知を登録できます。 登録するコンポーネントの呼び出しに[ **IoRegisterPlugPlayNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549526)します。 このルーチンは、デバイス インターフェイスのインスタンスのインスタンスを有効または無効になっている、指定したデバイス クラスのたびに呼び出されるドライバーが指定したコールバックのアドレスを格納します。 コールバック ルーチンの受信、 [ **DEVICE_INTERFACE_CHANGE_NOTIFICATION** ](https://msdn.microsoft.com/library/windows/hardware/ff543134)構造体、インターフェイス インスタンスのシンボリック リンクを表す Unicode 文字列が含まれています。 参照してください[PnP のデバイス インターフェイスの変更通知を使用して](https://msdn.microsoft.com/library/windows/hardware/ff565474)詳細についてはします。

    ドライバーまたはその他のカーネル モード コンポーネントを呼び出すことも[ **IoGetDeviceInterfaces** ](https://msdn.microsoft.com/library/windows/hardware/ff549186) 、登録されているすべての一覧を取得するには、デバイス インターフェイスのクラスのインスタンスを特定のデバイス インターフェイスを有効にします。 返された一覧には、デバイス インターフェイスのインスタンスを識別する Unicode シンボリック リンクの文字列へのポインターが含まれています。

2.  インターフェイスのインスタンスに対応するデバイスまたはファイル オブジェクトへのポインターを取得します。

    特定のデバイス オブジェクトにアクセスするドライバーを呼び出す必要があります[ **IoGetDeviceObjectPointer**](https://msdn.microsoft.com/library/windows/hardware/ff549198)、必要なインターフェイスでの Unicode 文字列を渡す、 *ObjectName*パラメーター。 ファイル オブジェクトにアクセスするドライバーを呼び出す必要があります[ **InitializeObjectAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff547804)での Unicode 文字列を渡す、 *ObjectName*パラメーターであり、パス、正常に呼び出しに属性の構造を初期化[ **ZwCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff566424)します。

 

 





