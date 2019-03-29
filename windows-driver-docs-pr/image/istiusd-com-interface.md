---
title: IStiUSD COM インターフェイス
description: IStiUSD COM インターフェイス
ms.assetid: 2f805955-8c66-4c9e-839e-c8a98c6637a8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea4f4f5b4670df9aff4a33719d5d0904c22f1ce7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572787"
---
# <a name="istiusd-com-interface"></a>IStiUSD COM インターフェイス





**IStiUSD**の COM インターフェイスは、の方法で、 [IStiDevice COM インターフェイス](istidevice-com-interface.md)静止画像デバイスと通信します。 **IStiUSD**インターフェイスのメソッドは、各ベンダーから提供されたによって実装される[ユーザー モードのままイメージ ミニドライバー](overview-of-sti-components.md#ddk-user-mode-still-image-minidrivers-si)します。

通常、 **IStiUSD**インターフェイス メソッドは、によって定義された同じ名前のメソッドによって呼び出される、 **IStiDevice**インターフェイス。 イメージのミニドライバーが通常実装も**IStiUSD**インターフェイス メソッドを呼び出して、適切なカーネル モード ドライバー。 各ミニドライバーがメソッドでない場合は、すべてのインターフェイス メソッドを定義する必要がありますに必要な STIERR を返すこと\_サポートされていません。

によって定義されたメソッド、 **IStiUSD**インターフェイスには、次が含まれます。

<a href="" id="istiusd--devicereset"></a>[**IStiUSD::DeviceReset**](https://msdn.microsoft.com/library/windows/hardware/ff543812)  
静止画像デバイスを既知の初期化された状態にリセットします。

<a href="" id="istiusd--diagnostic"></a>[**IStiUSD::Diagnostic**](https://msdn.microsoft.com/library/windows/hardware/ff543814)  
静止画像デバイスでは、診断テストを実行します。

<a href="" id="istiusd--escape"></a>[**IStiUSD::Escape**](https://msdn.microsoft.com/library/windows/hardware/ff543815)  
静止画像デバイスのベンダー固有の I/O 操作を実行します。

<a href="" id="istiusd--getcapabilities"></a>[**IStiUSD::GetCapabilities**](https://msdn.microsoft.com/library/windows/hardware/ff543817)  
デバイスの機能に静止画像を返します。

<a href="" id="istiusd--getlasterrorinfo"></a>[**IStiUSD::GetLastErrorInfo**](https://msdn.microsoft.com/library/windows/hardware/ff543820)  
静止画像デバイスに関連付けられている最後の既知のエラーに関する情報を返します。

<a href="" id="istiusd--getnotificationdata"></a>[**IStiUSD::GetNotificationData**](https://msdn.microsoft.com/library/windows/hardware/ff543821)  
静止画像デバイスで発生した最新のイベントの説明を返します。

<a href="" id="istiusd--getstatus"></a>[**IStiUSD::GetStatus**](https://msdn.microsoft.com/library/windows/hardware/ff543823)  
静止画像デバイスの状態を返します。

<a href="" id="istiusd--initialize"></a>[**IStiUSD::Initialize**](https://msdn.microsoft.com/library/windows/hardware/ff543824)  
定義する COM オブジェクトのインスタンスを初期化します、 **IStiUSD**インターフェイス。

<a href="" id="istiusd--lockdevice"></a>[**IStiUSD::LockDevice**](https://msdn.microsoft.com/library/windows/hardware/ff543829)  
呼び出し元によって排他的に使用のデバイスをロックします。

<a href="" id="istiusd--rawreadcommand"></a>**IStiUSD::RawReadCommand**  
読み取りは、静止画像デバイスからの情報をコマンドします。

<a href="" id="istiusd--rawreaddata"></a>[**IStiUSD::RawReadData**](https://msdn.microsoft.com/library/windows/hardware/ff543834)  
静止画像デバイスからデータを読み取ります。

<a href="" id="istiusd--rawwritecommand"></a>[**IStiUSD::RawWriteCommand**](https://msdn.microsoft.com/library/windows/hardware/ff543836)  
静止画像デバイスにコマンド情報を書き込みます。

<a href="" id="istiusd--rawwritedata"></a>[**IStiUSD::RawWriteData**](https://msdn.microsoft.com/library/windows/hardware/ff543839)  
静止画像デバイスにデータを書き込みます。

<a href="" id="istiusd--setnotificationhandle"></a>[**IStiUSD::SetNotificationHandle**](https://msdn.microsoft.com/library/windows/hardware/ff543840)  
デバイス イベントの呼び出し元に通知するために、ミニドライバーが使用する必要がありますイベント ハンドルを指定します。 通常、静止画像イベント モニターによって呼び出されます。

<a href="" id="istiusd--unlockdevice"></a>[**IStiUSD::UnLockDevice**](https://msdn.microsoft.com/library/windows/hardware/ff543843)  
デバイスのロックを解除します。

 

 




