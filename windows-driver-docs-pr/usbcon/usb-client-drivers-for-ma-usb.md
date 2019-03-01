---
Description: USB device driver that sends MA-USB packets.
title: メディアに依存しない (USB MA) の USB クライアント ドライバー
ms.date: 09/26/2017
ms.localizationpriority: medium
ms.openlocfilehash: 572dcf688633987f3b14b9fae2da9cf889a8c82e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527244"
---
# <a name="usb-client-drivers-for-media-agnostic-ma-usb"></a>メディアに依存しない (USB MA) の USB クライアント ドライバー

Windows 10 バージョン 1709 で USB ドライバー スタック パケットを送信できます USB USB 以外の物理メディアなど、Wi-fi 経由でメディアに依存しない USB (USB MA) プロトコルを使用しています。 新しい機能は、既存の USB クライアント ドライバーに必要な変更が最小限に抑えるように設計されています。 この一連の変更では、トランスポートに関する追加情報を含めます。

-   アイソクロナス/ストリーミング エンドポイントを持つデバイスは、クライアント ドライバーは、プログラミングの転送に関連する遅延を把握し、デバイスが、時間にアイソクロナス パケットを取得することを確認して、ドライバーを行える、完了を転送する必要があります。

-   クライアント ドライバーでは、プロトコルの上位のレイヤーの選択を最適化するために、その informationf を使用できます。 たとえば、ディスプレイ ドライバーは、最適なコーデックとバッファリング スキームを選択するのに、待機時間と帯域幅の情報を使用できます。 このような特性は、動的に変わる可能性がある、ドライバーは、変更を確認する必要があります。

## <a name="getting-the-delays-for-isochronous-transfers"></a>アイソクロナス転送の遅延を取得します。

アイソクロナス エンドポイントは、クライアント ドライバーは、プログラミングの最大待機時間と最大の完了の待機時間を把握する必要があります。 MA USB 仕様は、ホストがこれらの値を計算するためのメカニズムを提供します。 その待機時間は、同じデバイス上の複数のエンドポイントに対して異なるできるので、その要求は特定のパイプの対象となる必要があります。 

ドライバーを使用する必要があります、その要求を構築する、 **_URB_GET_ISOCH_PIPE_TRANSFER_PATH_DELAYS** URB します。

> [!NOTE]
> このリリースでは、この機能は KMDF と WDM ベースのドライバーのみを使用できます。 

この URB を構築するためのベスト プラクティスを次に示します。


-    呼び出すことによってこの URB を割り当てる必要がありますクライアント dirver [WdfUsbTargetDeviceCreateUrb](https://msdn.microsoft.com/library/windows/hardware/hh439423)または[USBD_UrbAllocate](https://msdn.microsoft.com/library/windows/hardware/hh406250)します。 
- URB に送信されることができます < = ディスパッチ レベル。
- URB は非アイソクロナス エンドポイントを対象となる、USB ドライバー スタックでは、要求が失敗します。
- クライアント ドライバーはこの URB がサード パーティ製の USB スタックでサポートされていると想定する必要があります。 すべて Microsoft によってサポートされる指定された受信トレイの USB クライアント ドライバーを = です。

継続的なアイソクロナス streaming では、クライアント ドライバー通常問題の未処理の複数の読み取り要求。 ドライバーは、ラウンドト リップ時間を使用して、未処理の読み取り要求の数に基づいて、読み取り要求に存在する必要があるアイソクロナス パケットの数を計算します。

たとえば、未処理の要求の数が 2 つの場合で、URB isochronous パケットの数以上でなければなりません (ラウンド トリップ時間の合計)/(サービス間隔の長さ)、ラウンド トリップ時間の合計 = MaximumSendPathDelayInMilliSeconds +MaximumCompletionPathDelayInMilliSeconds

送信を遅らせるかどうか = 10 ミリ秒、完了遅延 = 15msec、合計のラウンド トリップ 25msec を =。
場合サービス間隔の長さ = 5 ミリ秒アイソクロナス翻訳の数 = 2、継続的なストリーミングの各アイソクロナス翻訳で isochronous パケットの数する必要がありますが、少なくとも、= 25 5/5 パケットを =。

## <a name="getting-the-host-controller-transport-characteristics"></a>ホスト コント ローラーのトランスポート特性を取得します。
クライアント ドライバーでは、これらの Ioctl 要求を送信することによってトランスポート特性を取得できます。

-    [IOCTL_USB_GET_TRANSPORT_CHARACTERISTICS](https://msdn.microsoft.com/Library/Windows/Hardware/36CF2034-C816-421A-8B59-A4DC4EFFEB70)
-    [IOCTL_USB_REGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](https://msdn.microsoft.com/Library/Windows/Hardware/4192501F-5A30-463C-924D-CD4F2C8C3764)
-    [IOCTL_USB_NOTIFY_ON_TRANSPORT_CHARACTERISTICS_CHANGE](https://msdn.microsoft.com/Library/Windows/Hardware/1B71794C-EBAD-4F6C-A71C-C0D419D486BE) 
-    [IOCTL_USB_UNREGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](https://msdn.microsoft.com/Library/Windows/Hardware/A6D17761-4E5F-42FC-AB40-C2BCE7769243)

トランスポートの特性は、USB ドライバー スタックがそれらの値を公開する、基になるトランスポートに依存するために常に利用できない可能性があります。 そのため、クライアント ドライバーする必要があります情報を決定する、他のメカニズムを介して IOCTL 要求が失敗したときにします。 

### <a name="query-for-the-current-transport-characterisctics"></a>現在のトランスポート characterisctics のクエリ

クライアント ドライバーは送信することによって特定の時点でのトランスポート特性をクエリすることができます、 [IOCTL_USB_GET_TRANSPORT_CHARACTERISTICS](https://msdn.microsoft.com/Library/Windows/Hardware/36CF2034-C816-421A-8B59-A4DC4EFFEB70)要求。 要求を受信するには、USB ドライバー スタックがと共に直ちに完了 USB_TRANSPORT_CHARACTERISTICS 構造内の現在のトランスポート特性に関する情報。 情報は示しませんが常に、この要求での変更をアルゴリズムを決定する、またはストリームの開始のドライバーで使用できます。 

### <a name="receive-changes-in-trasport-characteristics"></a>Trasport 特性の変更を受信します。
MA USB、基になるトランスポートがワイヤード (有線)、ワイヤレスで可能性があります。 これらのメディアのトランスポート特性は、時間の経過と共に大きく異なることができます。 クライアント ドライバーで継続的な変更通知を受け取ることができます。

1.    送信、 [IOCTL_USB_REGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](https://msdn.microsoft.com/Library/Windows/Hardware/4192501F-5A30-463C-924D-CD4F2C8C3764)要求の通知を登録します。 登録が成功した場合、クライアント ドライバーは、ハンドルとトランスポート特性の初期値を受け取ります。

2.  送信、 [IOCTL_USB_NOTIFY_ON_TRANSPORT_CHARACTERISTICS_CHANGE](https://msdn.microsoft.com/Library/Windows/Hardware/1B71794C-EBAD-4F6C-A71C-C0D419D486BE)手順 1. で登録ハンドルを要求します。 USB ドライバー スタックは、保留中の要求を保持します。 トランスポート特性の変更のたびに、トランスポートの特性の新しい値で保留中の要求が完了しました。

3.  クライアントが完了し、さらに通知の取得中に関心がない、そのことを確認しますが、スタック内の保留中の Ioctl がないと、IOCTL サブ コードを送信して[IOCTL_USB_UNREGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](https://msdn.microsoft.com/Library/Windows/Hardware/A6D17761-4E5F-42FC-AB40-C2BCE7769243)登録ハンドルを渡して、します。 クライアントは、保留中の変更要求の登録を解除場合、USB スタックは完了して IOCTL 登録解除を完了する前にします。

### <a name="query-for-device-characteristics"></a>デバイスの特性のクエリ

Determione に最大値などの USB デバイスに関する標準の特性が送信し、クライアント ドライバーを送信するすべての要求の遅延を受信、 [IOCTL_USB_GET_DEVICE_CHARACTERISTICS](https://msdn.microsoft.com/Library/Windows/Hardware/D4A8DE43-3E81-4A1C-B1C0-ABE6000D9F11)要求。

## <a name="setting-priority-for-a-bulk-endpoint"></a>一括エンドポイントの優先度の設定

特定のクライアント ドライバーでは、一括エンドポイントを使用して、さまざまな種類のデータを一括転送の優先度クラスに収まらないを実行するための場合があります。 たとえば、USB のディスプレイ ドライバーは、ディスプレイのフレームとカーソルの更新プログラムを実行するため一括エンドポイントを使用することができます。 MIDI の USB オーディオ ドライバーでは、オーディオ/音声データを実行するため、一括のエンドポイントを使用できます。
ユーザー良好なエクスペリエンス MA USB 経由でこのようなクライアント ドライバーで、ドライバーはデータの種類に基づく一括転送を優先する必要があります。 たとえば、マウス カーソルの更新実行する一括エンドポイントまたはオーディオ/音声データ設定されなければなりません最も高い優先度表示/ビデオまたはストレージのデータを保持する一括エンドポイントは中位の優先順位を設定することは。

クライアント ドライバーでは、デバイスのハードウェアのレジストリ キーのデバイス パラメーターのサブキーの特定の一括エンドポイント priorties を定義することで、オプションを設定できます。  

レジストリ値の形式は、という名前の複数**EndpointPriorities**します。  複数行文字列内の各文字列は、特定のエンドポイントの優先順位を定義します。  文字列の形式のとおりです:"<CONFIG>、<INTERFACE>、<ALTSETTING>、<TYPE>、<ORDER>、<PRIORITY>"

各項目の意味は次のとおりです。

-    – CONFIG を示す値を 10 進数、 **bConfigurationValue**構成記述子で定義されているエンドポイントを格納している構成の値。  0 の値が無効です。  ワイルドカード値"*"を示すすべての構成に適用される指定することがあります。

-    インターフェイスの 10 進値を示す、 **bInterfaceNumber**インターフェイス記述子で定義されているエンドポイントが含まれた構成内のインターフェイスとして。  ワイルドカード値"*"を示すすべてのインターフェイスに適用される指定することがあります。  USB デバイス全体ではなく複合 USB 関数にレジストリ設定を適用されている場所の場合は、インターフェイスの値を示します。

-    ALTSETTING - インターフェイスの bAlternateSetting 値を表す 10 進値の代替設定します。  ワイルドカード値"*"に、インターフェイス内のすべての代替設定に適用されるかを示すことができます。

-    入力 - 型および指定されているエンドポイントの方向を示します。  有効な文字列は**BULK_IN**、 **BULK_OUT**、 **INTERRUPT_IN**、 **INTERRUPT_OUT**、 **ISOCHRONOUS_IN**、 **ISOCHRONOUS_OUT**、および**コントロール**します。  

-    配置 - に適用されます、インターフェイス内でエンドポイントの優先順位を示す 0 から始まる 10 進値。  たとえば、インターフェイスが 3 つの BULK_OUT エンドポイントがある場合は、最初のエンドポイントが 0 の位置の値、1 と 2 番目のエンドポイントによって指定されます。  複合 USB デバイス上の関数のインターフェイスの番号、インターフェイスを基準に割り当てられます複合の関数では、親の USB デバイスではありません。

以下に例を示します。

```cpp

REG_MULTI_SZ:"EndpointPriorities" = 
“"1,0,*,BULK_IN,0,VIDEO",   // BULK IN endpoint in interface 0, configuration 1, all alternate settings has VIDEO priority. 
"1,1,*,BULK_OUT,0,VOICE",  // First BULK OUT endpoint in interface 1, configuration 1, all alternate settings has VOICE priority. 
"2,1,0,BULK_OUT,1,INTERACTIVE"” // BULK OUT endpoint in configuration 2, interface 1, alt setting 1 has INTERACTIVE priority.
```
## <a name="see-also"></a>参照
[WdfUsbTargetDeviceCreateUrb](https://msdn.microsoft.com/library/windows/hardware/hh439423)

[USBD_UrbAllocate](https://msdn.microsoft.com/library/windows/hardware/hh406250)
[IOCTL_USB_GET_TRANSPORT_CHARACTERISTICS](https://msdn.microsoft.com/Library/Windows/Hardware/36CF2034-C816-421A-8B59-A4DC4EFFEB70)

[IOCTL_USB_REGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](https://msdn.microsoft.com/Library/Windows/Hardware/4192501F-5A30-463C-924D-CD4F2C8C3764)

[IOCTL_USB_NOTIFY_ON_TRANSPORT_CHARACTERISTICS_CHANGE](https://msdn.microsoft.com/Library/Windows/Hardware/1B71794C-EBAD-4F6C-A71C-C0D419D486BE)

[IOCTL_USB_UNREGISTER_FOR_TRANSPORT_CHARACTERISTICS_CHANGE](https://msdn.microsoft.com/Library/Windows/Hardware/A6D17761-4E5F-42FC-AB40-C2BCE7769243)
