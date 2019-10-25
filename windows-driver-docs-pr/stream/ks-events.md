---
title: KS のイベント
description: KS のイベント
ms.assetid: 3eaa1d65-8417-4a07-b358-823394baec9b
keywords:
- カーネルストリーミング WDK、イベント
- KS WDK、イベント
- イベント WDK カーネルストリーミング
- イベントセット WDK カーネルストリーミング
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a8cbd98e9f3d02d5d3b288d4a658e3f4b385ee3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842518"
---
# <a name="ks-events"></a>KS のイベント





AVStream ミニドライバーを作成する場合は、 [avstream のイベント処理に](event-handling-in-avstream.md)関する記述を参照してください。

イベントセットは、リスナーが通知を要求できる関連イベントのグループです。 たとえば、リスナーはデバイスの状態の変更またはストリームの位置の変更が通知されるように登録できます。 イベントが発生すると、カーネルストリーミングは、このイベントに登録されているすべてのクライアントに通知します。

ミニドライバーは、ルーチンを処理するポインターを含む[**KSEVENT\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksevent_item)の構造を提供することによって、イベントがどのようにサポートされるかを説明します。

リスナーは、IOCTL\_\_KS を使用してカーネルストリームプロキシルーチン[**KsSynchronousDeviceControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksproxy/nf-ksproxy-kssynchronousdevicecontrol)を呼び出して、通知を登録します。これにより、 [**KSEVENT**](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))と[**KSEVENTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)への\_イベント制御コードとポインターが有効になります。構成.

IOCTL\_KS\_無効化\_イベント要求は、指定されたイベントを無効にします。 イベントを有効にするために使用したものと同じポインターを使用して無効にする必要があります。 このポインターは、イベントを一意に識別します。 必要に応じて、クライアントは**NULL**ポインターと長さ0を指定して、クライアントのすべてのアクティブなイベントを無効にすることができます。

すべてのイベントセットで、KSEVENT\_TYPE\_BASICSUPPORT フラグがサポートされている必要があります。 使用可能なイベントフラグの一覧については、 [**KSEVENT**](https://docs.microsoft.com/previous-versions/ff561744(v=vs.85))を参照してください。

一部のイベントの種類では、イベント通知に登録するために追加のパラメーターが必要です。 たとえば、クロックが特定のタイムスタンプに達したときに、時計の[**KSEVENT\_clock\_POSITION\_MARK**](https://docs.microsoft.com/windows-hardware/drivers/stream/ksevent-clock-position-mark)イベントがトリガーされます。 そのため、このイベントの通知を受け取るように登録されているクライアントは、イベントをトリガーするタイムスタンプを指定する必要があります。

このような場合、ミニドライバーは、 [**KSEVENTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)構造体の後に、データバッファーに追加のデータパラメーターを渡します。 このようなイベントの種類をサポートするミニドライバーは、通知データを保持するために、最初のメンバーが KSEVENTDATA 型である拡張データ構造を使用します。

 

 




