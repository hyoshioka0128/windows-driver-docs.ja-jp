---
title: KS のイベント
description: KS のイベント
ms.assetid: 3eaa1d65-8417-4a07-b358-823394baec9b
keywords:
- カーネルの WDK、イベントのストリーミング
- KS WDK、イベント
- ストリーミング イベント WDK カーネル
- WDK カーネル ストリーミング イベントを設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7753843fe9ccabccb34978f279f23deb1864374
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382511"
---
# <a name="ks-events"></a>KS のイベント





AVStream、ミニドライバーを作成する場合は、次を参照してください。 [AVStream でのイベント処理](event-handling-in-avstream.md)します。

イベントのセットは、リスナーが通知を要求できる関連するイベントのグループです。 たとえば、リスナーは、デバイス状態の変更、またはストリームの位置の変更の通知を受ける登録でした。 イベントが発生したときにカーネルのストリーミング、このイベントに対して登録されているすべてのクライアントに通知します。

ミニドライバーは、提供することで、イベントに活かす方法について説明します、 [ **KSEVENT\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksevent_item)処理ルーチンへのポインターを含む構造体。

プロキシのルーチンをストリーミングするカーネルを呼び出すことによって、リスナーが通知の登録[ **KsSynchronousDeviceControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksproxy/nf-ksproxy-kssynchronousdevicecontrol) IOCTL で\_KS\_を有効にする\_イベント制御コードとポインター [ **KSEVENT** ](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))と[ **KSEVENTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata).structures します。

IOCTL\_KS\_を無効にする\_イベント要求は、指定したイベントを無効にします。 無効にするイベントを有効にするために使用された同じポインターを使用する必要があります。 このポインターは、イベントを一意に識別します。 クライアントを必要に応じて、指定することがあります、 **NULL**ポインターと長さが 0、クライアントのすべてのアクティブなイベントを無効にします。

すべてのイベント セットに、KSEVENT をサポートする必要があります\_型\_BASICSUPPORT フラグ。 参照してください[ **KSEVENT** ](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))使用可能なイベント フラグの一覧についてはします。

いくつかのイベントの種類には、イベント通知の登録に追加のパラメーターが必要です。 たとえば、 [ **KSEVENT\_クロック\_位置\_マーク**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-clock-position-mark)クロックが特定のタイムスタンプに達すると、時計のイベントがトリガーされます。 したがって、このイベントの通知を登録するクライアントでは、イベントをトリガーするタイムスタンプを指定する必要があります。

このような場合は、ミニドライバーは後のデータ バッファーに追加のデータ パラメーターを渡す、 [ **KSEVENTDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kseventdata)構造体。 このようなイベントの種類をサポートするミニドライバーは、通知のデータを保持するために、KSEVENTDATA、型のうち最初のメンバーは、拡張データ構造体を使用します。

 

 




