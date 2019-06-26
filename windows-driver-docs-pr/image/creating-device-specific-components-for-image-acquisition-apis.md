---
title: イメージ取得 API 用のデバイス固有のコンポーネントの作成
description: イメージ取得 API 用のデバイス固有のコンポーネントの作成
ms.assetid: c4906dec-6d34-47f5-abde-0513c4499a66
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9388db615a5e62de877fd1d1d1b80dadfee8d697
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370074"
---
# <a name="creating-device-specific-components-for-image-acquisition-apis"></a>イメージ取得 API 用のデバイス固有のコンポーネントの作成





画像を取得、TWAIN などの Api には、TWAIN データ ソースなどのデバイスに固有のコンポーネントが通常必要があります。 これらのデバイスに固有のコンポーネントを使用する必要があります、 [IStillImage COM インターフェイス](istillimage-com-interface.md)と[IStiDevice COM インターフェイス](istidevice-com-interface.md)静止画像デバイス ドライバーをユーザー モードとイベントのモニターと通信します。

イメージの取得 Api を呼び出すことができます[ **IStillImage::GetDeviceValue** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543786(v=vs.85))と[ **IStillImage::SetDeviceValue** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543801(v=vs.85)) を読み書きする[レジストリ エントリは、デバイスを静止画像](registry-entries-for-still-image-devices.md)します。 たとえば、各静止画像デバイスの TWAIN データ ソースの名前は、レジストリに格納されます。

TWAIN API では、アプリケーションをデータ ソースを呼び出すときに、アクティブなデバイスを指定することはできません、ため、データ ソースが呼び出す通常[ **IStillImage::GetDeviceList** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543784(v=vs.85))まだすべての一覧を取得するにはデバイスのイメージし、は、通常、製造元とモデルの名前に基づく、適切なデバイスを検索するリストを検索し。 製造元とモデルのテキスト名は、セットアップ情報 (INF) ファイルから取得されます。 ため、TWAIN データ ソース名には 32 文字の制限があり、WIA は「WIA の」互換性のある名前を構築する文字列を追加、ため、INF ファイル内のテキストは 28 文字より長くできません必要があります。 文字列全体で最初の 32 文字だけでなく、比較を実行するアプリケーションがそれ以外の場合、TWAIN と互換性のあるできない自動的に起動するアプリケーションの原因となったデバイスを検索することがあります。

デバイスにアクセスするイメージの購入ソフトウェア呼び出し[ **IStillImage::CreateDevice** ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543778(v=vs.85))を定義する COM オブジェクトのインスタンスを作成する、 **IStiDevice**インターフェイス。 **IStiDevice**インターフェイスには、デバイスの I/O 操作を実行するためのいくつかの方法が用意されています。 イメージの取得のソフトウェアが「データ」を指定する必要がありますオブジェクト インスタンスを作成するときに[転送モード](transfer-modes.md)します。

イメージの取得のソフトウェアを呼び出すことができます[ **IStiDevice::Subscribe** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-subscribe)要求の通知を配信するイベントの監視に[イメージ デバイス イベントではまだ](still-image-device-events.md)します。 通知を受け取ったら、 [ **IStiDevice::GetLastNotificationData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-getlastnotificationdata)イベントの種類を決定するということができます。 [**IStiDevice::UnSubscribe** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-unsubscribe)通知が不要になったときに呼び出す必要があります。

イメージの購入ソフトウェアがいつ終了したを使用して、 **IStiDevice**インターフェイスを呼び出す必要があります[ **IStiDevice::Release**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sti/nf-sti-istidevice-release)します。

 

 




