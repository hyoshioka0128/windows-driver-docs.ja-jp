---
title: イメージ取得 API 用のデバイス固有のコンポーネントの作成
description: イメージ取得 API 用のデバイス固有のコンポーネントの作成
ms.assetid: c4906dec-6d34-47f5-abde-0513c4499a66
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 729d8b24254b88b7a45eb6129624e9f1052fddc0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840866"
---
# <a name="creating-device-specific-components-for-image-acquisition-apis"></a>イメージ取得 API 用のデバイス固有のコンポーネントの作成





TWAIN などのイメージ取得 Api には、通常、TWAIN データソースなどのデバイス固有のコンポーネントが必要です。 これらのデバイス固有のコンポーネントでは、 [ISTILLIMAGE Com インターフェイス](istillimage-com-interface.md)と[Iのデバイス com インターフェイス](istidevice-com-interface.md)を使用して、ユーザーモードのイメージデバイスドライバーとイベントモニターとの通信を行う必要があります。

イメージ取得 Api は、 [**IStillImage:: getdevicevalue**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543786(v=vs.85))と[**IStillImage:: setdevicevalue**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543801(v=vs.85))を呼び出して、[静止イメージデバイスのレジストリエントリの](registry-entries-for-still-image-devices.md)読み取りと書き込みを行うことができます。 たとえば、静止画像デバイスの各 TWAIN データソースの名前は、レジストリに格納されます。

TWAIN API では、データソースを呼び出すときにアプリケーションがアクティブなデバイスを指定することは許可されていないため、通常、データソースは[**IStillImage:: GetDeviceList**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543784(v=vs.85))を呼び出して、すべての静止イメージデバイスの一覧を取得し、次にリストを検索して検索します。デバイスを修正します。通常は製造元とモデルの名前に基づいています。 製造元とモデルのテキスト名は、セットアップ情報 (INF) ファイルから取得されます。 TWAIN ではデータソース名に32文字の制限があり、WIA では互換性のある名前を作成するために "WIA-" が文字列に追加されるため、INF ファイル内のテキストは28文字を超えることはできません。 それ以外の場合、最初の32文字だけでなく文字列全体を比較する、TWAIN と互換性のあるアプリケーションは、アプリケーションの起動の原因となったデバイスを自動的に見つけることができない可能性があります。

デバイスにアクセスするために、イメージ取得ソフトウェアは[**IStillImage:: CreateDevice**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff543778(v=vs.85))を呼び出して、 **i デバイス**インターフェイスを定義する COM オブジェクトのインスタンスを作成します。 **Iのデバイス**インターフェイスには、デバイスの i/o 操作を実行するためのメソッドがいくつか用意されています。 オブジェクトインスタンスを作成するときは、イメージ取得ソフトウェアで "データ"[転送モード](transfer-modes.md)を指定する必要があります。

イメージ取得ソフトウェアは、 [**It device:: Subscribe**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-subscribe)を呼び出して、イベントモニターに[静止イメージデバイスイベント](still-image-device-events.md)の通知を配信するように要求できます。 通知が受信されると、 [**Iのデバイス:: GetLastNotificationData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-getlastnotificationdata)を呼び出して、イベントの種類を特定できます。 通知が不要になった場合は、 [**Iare device:: 講読**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-unsubscribe)を呼び出す必要があります。

イメージ取得ソフトウェアが**iのデバイス**インターフェイスの使用を終了したら、[**し device:: Release**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sti/nf-sti-istidevice-release)を呼び出す必要があります。

 

 




