---
title: IStiUSD COM インターフェイス
description: IStiUSD COM インターフェイス
ms.assetid: 2f805955-8c66-4c9e-839e-c8a98c6637a8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 412beac255f6be463bb8b8b6cb51c606b41d1fc5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840806"
---
# <a name="istiusd-com-interface"></a>IStiUSD COM インターフェイス





I、 **us** com インターフェイスは、 [ISIDE-BY-SIDE デバイス com インターフェイス](istidevice-com-interface.md)が静止イメージデバイスと通信する手段です。 **Iミニドライバー**のインターフェイスのメソッドは、ベンダーから提供されている各[ユーザーモードの Image](overview-of-sti-components.md#ddk-user-mode-still-image-minidrivers-si)によって実装されます。

通常、iare **us**インターフェイスメソッドは、 **iare device**インターフェイスによって定義された同様の名前付きメソッドによって呼び出されます。 静止画像ミニドライバーは、通常、適切なカーネルモードドライバーを呼び出すことによって**Istiusd**インターフェイスメソッドを実装します。 各ミニドライバーはすべてのインターフェイスメソッドを定義する必要がありますが、メソッドが不要な場合は、サポートされていないという\_エラーを返すことができます。

**I、usd**インターフェイスによって定義されるメソッドには、次のものがあります。

<a href="" id="istiusd--devicereset"></a>[**Ievicereset::D**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-devicereset)  
静止イメージデバイスを既知の初期状態にリセットします。

<a href="" id="istiusd--diagnostic"></a>[**I(米ドル)::D iとらわれない**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-diagnostic)  
静止イメージデバイスで診断テストを実行します。

<a href="" id="istiusd--escape"></a>[**I、Usd:: Escape**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-escape)  
静止イメージデバイスでベンダー固有の i/o 操作を実行します。

<a href="" id="istiusd--getcapabilities"></a>[**Iと Usd:: GetCapabilities**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getcapabilities)  
静止イメージデバイスの機能を返します。

<a href="" id="istiusd--getlasterrorinfo"></a>[**Iと Usd:: GetLastErrorInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getlasterrorinfo)  
静止イメージデバイスに関連付けられている最後の既知のエラーに関する情報を返します。

<a href="" id="istiusd--getnotificationdata"></a>[**I、Usd:: GetNotificationData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getnotificationdata)  
静止イメージデバイスで発生した最新のイベントの説明を返します。

<a href="" id="istiusd--getstatus"></a>[**IGetStatus::** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getstatus)  
静止イメージデバイスの状態を返します。

<a href="" id="istiusd--initialize"></a>[**Iと Usd:: Initialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize)  
**Iwhere-object**インターフェイスを定義する COM オブジェクトのインスタンスを初期化します。

<a href="" id="istiusd--lockdevice"></a>[**I_ Usd:: LockDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-lockdevice)  
呼び出し元によって排他的に使用されるようにデバイスをロックします。

<a href="" id="istiusd--rawreadcommand"></a>**IStiUSD:: RawReadCommand**  
静止イメージデバイスからコマンド情報を読み取ります。

<a href="" id="istiusd--rawreaddata"></a>[**IRawReadData::** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawreaddata)  
静止イメージデバイスからデータを読み取ります。

<a href="" id="istiusd--rawwritecommand"></a>[**IStiUSD:: RawWriteCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawwritecommand)  
コマンド情報を静止イメージデバイスに書き込みます。

<a href="" id="istiusd--rawwritedata"></a>[**IStiUSD:: RawWriteData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-rawwritedata)  
静止イメージデバイスにデータを書き込みます。

<a href="" id="istiusd--setnotificationhandle"></a>[**Iと Usd:: SetNotificationHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-setnotificationhandle)  
ミニドライバーがデバイスイベントの呼び出し元に通知するために使用するイベントハンドルを指定します。 通常、静止イメージイベントモニタによって呼び出されます。

<a href="" id="istiusd--unlockdevice"></a>[**IUnLockDevice::** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-unlockdevice)  
デバイスのロックを解除します。

 

 




