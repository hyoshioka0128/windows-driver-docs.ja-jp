---
Description: MA USB パケットを送信する USB デバイスドライバー。
title: Media-Agnostic (MA-USB) 用 USB クライアント ドライバー
ms.date: 09/26/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e5cce8e6c3cec069a3d1aa69d3c6376e2b73855
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843197"
---
# <a name="usb-client-drivers-for-media-agnostic-ma-usb"></a>Media-Agnostic (MA-USB) 用 USB クライアント ドライバー

Windows 10 バージョン1709では、USB ドライバースタックは、メディアに依存しない USB (MA) プロトコルを使用して、Wi-fi などの非 USB 物理メディア経由で USB パケットを送信できます。 新しい機能は、USB クライアントドライバーの既存に必要な変更が最小限になるように設計されています。 この一連の変更には、トランスポートに関する追加情報が含まれます。

-   アイソクロナス/ストリーミングエンドポイントを使用するデバイスの場合、クライアントドライバーは、デバイスが常時アイソクロナスパケットを確実に取得できるように、転送プログラミングおよび転送完了に関連する遅延を知る必要があります。

-   クライアントドライバーは、その情報 f を使用して、より高いレイヤーのプロトコルの選択を最適化できます。 たとえば、ディスプレイドライバーは、待ち時間と帯域幅の情報を使用して、最適なコーデックとバッファリングスキームを選択できます。 これらの特性は動的に変更される可能性があるため、ドライバーは変更を判断する必要があります。

## <a name="getting-the-delays-for-isochronous-transfers"></a>アイソクロナス転送の遅延を取得する

アイソクロナスエンドポイントの場合、クライアントドライバーは、最大のプログラミング待機時間と最大完了待機時間を把握している必要があります。 この要求は、特定のパイプを対象としている必要があります。これは、同じデバイス上の異なるエンドポイントの待機時間が、ホストがこれらの値を計算するメカニズムを提供するためです。 

この要求をビルドするには、ドライバーが **_URB_GET_ISOCH_PIPE_TRANSFER_PATH_DELAYS** URB を使用する必要があります。

> [!NOTE]
> このリリースでは、KMDF と WDM ベースのドライバーのみがこの機能を使用できます。 

この URB を構築するためのベストプラクティスを次に示します。


-    クライアントの dirver は、 [WdfUsbTargetDeviceCreateUrb](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)または[USBD_UrbAllocate](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate)を呼び出すことによって、この URB を割り当てる必要があります。 
- URB は < = ディスパッチレベルで送信できます。
- URB が非アイソクロナスエンドポイントを対象としている場合、USB ドライバースタックは要求に失敗します。
- クライアントドライバーは、この URB がサードパーティの USB スタックでサポートされていると想定してはいけません。 これは、Microsoft が提供するすべての受信トレイの USB クライアントドライバーでサポートされます。

ストリーミングの連続するアイソクロナスの場合、クライアントドライバーは通常、複数の未処理の読み取り要求を発行します。 ドライバーはラウンドトリップ時間を使用して、未処理の読み取り要求の数に基づいて、読み取り要求に含まれる必要があるアイソクロナスパケットの数を計算できます。

たとえば、未処理の要求の数が2の場合、合計ラウンドトリップ時間 = MaximumSendPathDelayInMilliSeconds + を使用して、URB 内のアイソクロナスパケットの数は少なくとも (ラウンドトリップ時間の合計)/(サービス間隔の長さ) である必要があります。Maximum○ Pathdelayinmilliseconds

送信遅延 = 10 ミリ秒、完了遅延 = 15msec 秒、合計ラウンドトリップ数 = 25msec 秒。
サービス間隔の長さが、連続ストリーミングの場合、アイソクロナス URBs = 2 の長さが5ミリ秒の場合、各アイソクロナス URBs のアイソクロナスパケットの数は少なくとも 25/5 = 5 パケットである必要があります。

## <a name="getting-the-host-controller-transport-characteristics"></a>ホストコントローラーのトランスポート特性を取得する
クライアントドライバーは、次のような Ioctl 要求を送信することによって、トランスポートの特性を取得できます。

-    [IOCTL_USB_GET_TRANSPORT_CHARACTERISTICS](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_get_transport_characteristics)
-    [IOCTL_USB_REGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_register_for_transport_characteristics_change)
-    [IOCTL_USB_NOTIFY_ON_TRANSPORT_CHARACTERISTICS_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_notify_on_transport_characteristics_change) 
-    [IOCTL_USB_UNREGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_unregister_for_transport_characteristics_change)

USB ドライバースタックは基になるトランスポートに依存してそれらの値を公開するため、トランスポートの特性はすべてのケースで使用できるとは限りません。 そのため、クライアントドライバーは、IOCTL 要求が失敗したときに、他のメカニズムを介して情報を特定する必要があります。 

### <a name="query-for-the-current-transport-characterisctics"></a>現在のトランスポート characterisctics のクエリ

クライアントドライバーは、 [IOCTL_USB_GET_TRANSPORT_CHARACTERISTICS](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_get_transport_characteristics)要求を送信することによって、特定の時点でトランスポートの特性を照会できます。 USB ドライバースタックは、要求を受信すると、現在のトランスポート特性に関する情報を USB_TRANSPORT_CHARACTERISTICS 構造ですぐに完了します。 情報が常に変更されていることを示すわけではないため、この要求は、アルゴリズムを決定したり、ストリームを開始したりするためにドライバーによって使用されます。 

### <a name="receive-changes-in-trasport-characteristics"></a>Trasport の特性の変更を受信する
MA USB の場合、基になるトランスポートは有線、ワイヤレスになります。 これらのメディアのトランスポート特性は、時間の経過と共に大きく変化する可能性があります。 クライアントドライバーは、進行中の変更について通知を受け取ることができます。

1.    通知を登録するための[IOCTL_USB_REGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_register_for_transport_characteristics_change)要求を送信します。 登録が成功した場合、クライアントドライバーは、トランスポート特性のハンドルと初期値を受け取ります。

2.  手順 1. で取得した登録ハンドルを使用して[IOCTL_USB_NOTIFY_ON_TRANSPORT_CHARACTERISTICS_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_notify_on_transport_characteristics_change)要求を送信します。 USB ドライバースタックは、要求を保留状態のままにします。 トランスポートの特性が変更されるたびに、保留中の要求はトランスポート特性の新しい値で完了します。

3.  クライアントが実行され、さらに通知されないようにするには、スタックに保留中の Ioctl がないことを確認してから、サブコード[IOCTL_USB_UNREGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_unregister_for_transport_characteristics_change)で ioctl を送信し、登録ハンドルを渡します。 クライアントが保留中の変更要求で登録を解除すると、USB スタックは、IOCTL の登録解除を完了する前にそれらを完了させます。

### <a name="query-for-device-characteristics"></a>デバイスの特性に関するクエリ

要求の送信と受信の最大遅延など、USB デバイスに関する e 特性を判別するために、クライアントドライバーは[IOCTL_USB_GET_DEVICE_CHARACTERISTICS](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ns-usbioctl-_usb_device_characteristics)要求を送信できます。

## <a name="setting-priority-for-a-bulk-endpoint"></a>一括エンドポイントの優先順位の設定

場合によっては、一括転送の優先度クラスに収まらないさまざまな種類のデータを送信するために、特定のクライアントドライバーが一括エンドポイントを使用することがあります。 たとえば、USB ディスプレイドライバーでは、表示フレームとカーソルの更新を行うために一括エンドポイントを使用できます。 MIDI 用の USB オーディオドライバーでは、オーディオ/音声データを伝送するために一括エンドポイントを使用できます。
このようなクライアントドライバーを使用したユーザーエクスペリエンスを向上させるために、ドライバーはデータの種類に基づいて一括転送の優先順位を設定する必要があります。 たとえば、マウスカーソルの更新またはオーディオ/音声データを伝送する一括エンドポイントは、最も優先度の高いものとしてマークする必要がありますが、表示/ビデオまたはストレージデータを保持する一括エンドポイントは "中" の優先順位に設定する必要があります。

クライアントドライバーは、デバイスの HW レジストリキーのデバイスパラメーターサブキーで、特定の一括エンドポイントの priorties を定義することで、オプションを設定できます。  

レジストリ値の形式は、 **Endpointpriorities**という名前の文字列です。  複数文字列内の各文字列は、特定のエンドポイントの優先度を定義します。  文字列の形式は次のとおりです。 "<CONFIG>、<INTERFACE>、<ALTSETTING>、<TYPE>、<ORDER>、<PRIORITY>"

各項目の意味は次のとおりです。

-    CONFIG –構成記述子で定義されているエンドポイントを含む構成の**Bconfigurationvalue**値を示す10進値。  値0は無効です。  ワイルドカード値 "*" を指定すると、すべての構成に適用されることを示すことができます。

-    INTERFACE-インターフェイス記述子で定義されている、エンドポイントを含む構成内のインターフェイスの**bInterfaceNumber**を示す10進値。  ワイルドカード値 "*" を指定すると、すべてのインターフェイスに適用されることを示すことができます。  レジストリ設定が USB デバイス全体ではなく複合 USB 関数に適用されている場合、インターフェイスの値はを示します。

-    ALTSETTING-インターフェイスの代替設定の bAlternateSetting 値を示す10進値。  ワイルドカード値 "*" を使用して、インターフェイス内のすべての代替設定に適用されることを示すことができます。

-    TYPE-指定されているエンドポイントの種類と方向を示します。  有効な文字列は**BULK_IN**、 **BULK_OUT**、 **INTERRUPT_IN**、 **INTERRUPT_OUT**、 **ISOCHRONOUS_IN**、 **ISOCHRONOUS_OUT**、および**コントロール**します。  

-    POSITION-インターフェイス内で優先順位が適用されるエンドポイントを示す0から始まる10進値。  たとえば、インターフェイスに3つの BULK_OUT エンドポイントがある場合、最初のエンドポイントは、position 値が0、2番目のエンドポイントが1によって指定されます。  複合 USB デバイス上の関数の場合、インターフェイス番号は親の USB デバイスではなく、複合関数に割り当てられたインターフェイスに対して相対的です。

以下に例を示します。

```cpp

REG_MULTI_SZ:"EndpointPriorities" = 
“"1,0,*,BULK_IN,0,VIDEO",   // BULK IN endpoint in interface 0, configuration 1, all alternate settings has VIDEO priority. 
"1,1,*,BULK_OUT,0,VOICE",  // First BULK OUT endpoint in interface 1, configuration 1, all alternate settings has VOICE priority. 
"2,1,0,BULK_OUT,1,INTERACTIVE"” // BULK OUT endpoint in configuration 2, interface 1, alt setting 1 has INTERACTIVE priority.
```
## <a name="see-also"></a>参照
[WdfUsbTargetDeviceCreateUrb](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreateurb)

[USBD_UrbAllocate](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_urballocate)
[IOCTL_USB_GET_TRANSPORT_CHARACTERISTICS](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_get_transport_characteristics)

[IOCTL_USB_REGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_register_for_transport_characteristics_change)

[IOCTL_USB_NOTIFY_ON_TRANSPORT_CHARACTERISTICS_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_notify_on_transport_characteristics_change)

[IOCTL_USB_UNREGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbioctl/ni-usbioctl-ioctl_usb_unregister_for_transport_characteristics_change)
