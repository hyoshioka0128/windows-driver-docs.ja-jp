---
title: Windows 7 のデバイス ドライバー インターフェイス (DDI) の変更点
description: このトピックでは、新しい 1394 バス ドライバーをサポートする一般的な DDI 変更をまとめたものです。
ms.assetid: 5473C6AC-284C-41B1-AA67-75696BE96C24
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a13152caf8d7e79e729df0efcfcefcea9eb9f29
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385780"
---
# <a name="device-driver-interface-ddi-changes-in-windows-7"></a>Windows 7 のデバイス ドライバー インターフェイス (DDI) の変更点

Windows 7 には、1394ohci.sys、カーネル モード ドライバー フレームワーク (KMDF) を使用して実装されている新しい IEEE 1394 バス ドライバーが含まれています。 新しい 1394 バス ドライバーでは、レガシ IEEE バス ドライバー ポート/ミニポート構成--1394bus.sys と ochi1394.sys が置き換えられます。 新しい Ddi は 1394ohci.sys によってサポートされる新機能に追加されました。 さらに、特定 1394 Ddi された 1394 b 仕様で定義された速度をサポートするために変更し、1394 クライアント ドライバーの開発を簡略化が向上します。

このトピックでは、新しい 1394 バス ドライバーをサポートする一般的な DDI 変更をまとめたものです。

* [拡張のバスのリセット通知](#extended-bus-reset-notification)
* [新しい Ioctl PHY パケットのサポート](#new-ioctls-for-phy-packet-support)
* [新しい IOCTL ROM の構成を取得するには](#new-ioctl-to-retrieve-configuration-rom)
* [IEEE バス ドライバー DDI の変更](#ieee-bus-driver-ddi-changes)
* [速度とペイロードのサイズの新しいフラグ](#new-flags-for-speed-and-payload-size)
* [IEEE 1394 IOCTL を変更します。](#ieee-1394-ioctl-changes)
* [関連トピック](#related-topics)

## <a name="extended-bus-reset-notification"></a>拡張のバスのリセット通知

1394ohci.sys バス ドライバーでは、拡張のバスのリセット通知をサポートします。 この通知は、バスのリセット通知のコンテキストで 1394 クライアント ドライバー (世代の数とノード id) などのバスの現在の生成に関する情報を返します。 この情報には、1394 クライアント ドライバー生成数、ノード id、およびその他の情報の取得の同期、使用すると、バスには、通知ハンドラーをリセットする必要があります。

クライアント ドライバーが、既存を使用するには拡張のバスのリセット通知の登録、 [**要求\_BUS\_リセット\_通知**](https://msdn.microsoft.com/library/windows/hardware/ff537638) I/O 要求を指定します新しい拡張\_通知\_ルーチン フラグ、 **u.BusResetNotification.fulFlags**パラメーター。 ときに拡張された\_通知\_ルーチン フラグが指定されて、 **u.BusResetNotification.ResetContext**パラメーターが指す、 [ **BUS\_のリセット\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/1394/ns-1394-_bus_reset_data)構造体。

## <a name="new-ioctls-for-phy-packet-support"></a>新しい Ioctl PHY パケットのサポート

1394ohci.sys バス ドライバーは、IEEE 1394 a 仕様で定義されている、PHY パケットを送受信するための次の新しい Ddi を公開します。

* [**要求\_送信\_PHY\_パケット**](https://msdn.microsoft.com/library/windows/hardware/gg266407)
* [**要求\_受信\_PHY\_パケット**](https://msdn.microsoft.com/library/windows/hardware/gg266406)

新たに使用する必要があります[**要求\_送信\_PHY\_パケット**](https://msdn.microsoft.com/library/windows/hardware/gg266407) I/O 要求の代わりに[**要求\_送信\_PHY\_CONFIG\_パケット**](https://msdn.microsoft.com/library/windows/hardware/ff537661)します。 PHY パケットが間違った 1394 バスの生成に送信される可能性が生成数を指定するのには、後者の I/O 要求することはできません。

## <a name="new-ioctl-to-retrieve-configuration-rom"></a>新しい IOCTL ROM の構成を取得するには

新しい IOCTL [**要求\_取得\_CONFIG\_ROM**](https://msdn.microsoft.com/library/windows/hardware/gg266404)、1 キロバイト (KB) の最大サイズの最大のノードの構成、ROM の内容を返します。 1394ohci.sys バス ドライバーでは、従来の 1394 バス ドライバーと同じである、のみ 1 KB の構成、Rom をサポートしています。

## <a name="ieee-bus-driver-ddi-changes"></a>IEEE バス ドライバー DDI の変更

次の表では、新しい 1394 バス ドライバーと従来の 1394 バス ドライバーによって公開される Ddi の機能の動作の変更について説明します。

| デバイス ドライバー インターフェイス                                                              | 説明                                                                                                                                                                                                                                                                          |
|--------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**要求\_取得\_ローカル\_ホスト\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff537644)             | 1394ohci.sys バス ドライバーに設定がサポートされていません**nLevel** GET に\_ホスト\_CSR\_内容と速度を指定する\_マップ\_と場所**CsrBaseAddress**します。 速度のマップとは、IEEE 1394 a 仕様で廃止されています。                                                                |
| [**要求\_取得\_速度\_トポロジ\_マップ**](https://msdn.microsoft.com/library/windows/hardware/ff537646)     | [**要求\_取得\_速度\_トポロジ\_マップ**](https://msdn.microsoft.com/library/windows/hardware/ff537646) Windows 2000 以降のバージョンのオペレーティング システムでは非推奨です。 ステータスを返します 1394ohci.sys にこの要求を送信する\_無効な\_パラメーター。                                            |
| [**要求\_取得\_速度\_BETWEEN\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff537645) | 送信、 [**要求\_取得\_速度\_BETWEEN\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff537645) 1394ohci.sys への要求がローカル ノードの間の速度を取得し、デバイスです。 使用\_ローカル\_ノード フラグを設定する必要があります、 **u.GetMaxSpeedBetweenDevices.fulFlags**パラメーター。 |

## <a name="new-flags-for-speed-and-payload-size"></a>速度とペイロードのサイズの新しいフラグ

1394 ヘッダー ファイル、1394.h、Windows 7 の Windows Driver Kit では、高速より大きなペイロードの新しいフラグを定義します。 このセクションでは、これらの新しいフラグと値について説明します。

次の表では、各新しくサポートされた速度の最大非同期ペイロードのサイズについて説明します。

| Flag                       | Value | 説明 |
|----------------------------|-------|-------------|
| 非同期\_ペイロード\_800\_率  | 4096  | 800 mb/秒    |
| 非同期\_ペイロード\_1600\_率 | 4096  | 160 mb/秒    |
| 非同期\_ペイロード\_3200\_率 | 4096  | 3200 mb/秒   |

次の表では、各新しくサポートされた速度の速度フラグについて説明します。

| Flag               | Value | 説明 |
|--------------------|-------|-------------|
| 速度\_フラグ\_800  | 0x08  | 800 mb/秒    |
| 速度\_フラグ\_1600 | 0x10  | 160 mb/秒    |
| 速度\_フラグ\_3200 | 0x20  | 3200 mb/秒   |

次の表では、各新しくサポートされた速度の速度のコードの値について説明します。

| Flag              | Value | 説明 |
|-------------------|-------|-------------|
| SCODE\_800\_率  | 3     | 800 mb/秒    |
| SCODE\_1600\_率 | 4     | 160 mb/秒    |
| SCODE\_3200\_率 | 5     | 3200 mb/秒   |

## <a name="ieee-1394-ioctl-changes"></a>IEEE 1394 IOCTL を変更します。

このセクションでは、新しい速度やペイロード サイズの値を使用する 1394 I/O 要求について説明します。

[**要求\_ASYNC\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff537634)  
**u.AsyncRead.nBlockSize**

1394 ノードから読み取られるデータのストリーム内の各ブロックのサイズを指定します。 このパラメーターが 0 の場合は、raw モードのアドレス指定を使用しない場合、これらの読み取り要求を発行すると、デバイスの速度が選択されている最大パケット サイズが使用します。

非同期を指定する\_ペイロード\_*XXX*のフラグ、 **nBlockSize**メンバー。 Microsoft がそのクライアント ドライバーのセットをお勧めします、 **nBlockSize**メンバーを 0 に 1394 バス driver1394ohci.sys を使用するようにサポートされる最大値、raw モードのアドレス指定を使用しない場合。

クライアント ドライバーを設定する必要があります、raw モードのアドレス指定を使用する場合、 **nBlockSize**メンバー接続の速度でのデバイスでサポートされている非同期ペイロードの最大サイズにします。

Raw モードのアドレス指定の詳細については、次を参照してください。[を送信する非同期 I/O 要求パケットの IEEE 1394 バス](https://docs.microsoft.com/windows-hardware/drivers/ieee/sending-asynchronous-i-o-request-packets-on-the-ieee-1394-bus)します。

[**要求\_ASYNC\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff537636)  

### <a name="uasyncreadnblocksize"></a>u.AsyncRead.nBlockSize

1394 ノードに書き込まれたデータのストリーム内の各ブロックのサイズを指定します。 選択された速度の最大パケット サイズを使用して、このパラメーターが 0 の場合除算のような書き込み要求、raw モードのアドレス指定を使用しない場合。

非同期を指定する\_ペイロード\_*XXX*のフラグ、 **nBlockSize**メンバー。 Microsoft がそのクライアント ドライバーのセットをお勧めします、 **nBlockSize**メンバーを 0 に、1394 バス ドライバーを使用するようにサポートされる最大値、raw モードのアドレス指定を使用しない場合。

クライアント ドライバーを設定する必要があります、raw モードのアドレス指定を使用する場合、 **nBlockSize**メンバー接続の速度でのデバイスでサポートされている非同期ペイロードの最大サイズにします。

[**要求\_アイソクロナス\_ALLOCATE\_帯域幅**](https://msdn.microsoft.com/library/windows/hardware/ff537647)  
速度を指定する\_フラグ\_*XXX*のフラグ、 **fulSpeed**メンバー。 新しい 1394 バス ドライバーは、新しい速度を返すことができます\_フラグ\_*XXX*のフラグ、 **SpeedSelected**メンバー。

### <a name="uisochallocatebandwidthfulspeed"></a>u.IsochAllocateBandwidth.fulSpeed

帯域幅の割り当てに使用する接続の速度を指定します。 可能な速度の値は速度\_フラグ\_*XXX*ここで、 *XXX* (概算) の転送率 (mbps) です。

### <a name="uisochallocatebandwidthspeedselected"></a>u.IsochAllocateBandwidth.SpeedSelected

帯域幅を割り当てることが選択されている実際の速度を指定します。 値が 1 の速度の\_フラグ\_*XXX* (を参照してください、 **fulSpeed**メンバーの説明)。

[**要求\_アイソクロナス\_ALLOCATE\_リソース**](https://msdn.microsoft.com/library/windows/hardware/ff537649)  
速度を指定する\_フラグ\_*XXX*のフラグ、 **fulSpeed**メンバー。

### <a name="uisochallocateresourcesfulspeed"></a>u.IsochAllocateResources.fulSpeed

チャネルで通信するために使用する接続の速度を指定します。 可能な速度の値は速度\_フラグ\_*XXX*ここで、 *XXX* (概算) の転送率 (mbps) です。

[**要求\_アイソクロナス\_FREE\_帯域幅**](https://msdn.microsoft.com/library/windows/hardware/ff537652)  
速度を指定する\_フラグ\_*XXX*のフラグ、 **fulSpeed**メンバー。

### <a name="uisochfreebandwidthfulspeed"></a>u.IsochFreeBandwidth.fulSpeed

使用して帯域幅を解放する接続の速度を指定します。 可能な速度の値は速度\_フラグ\_*XXX*ここで、 *XXX* (概算) の転送率 (mbps) です。

> [!NOTE]
> 新しい 1394 バス ドライバーを使用して、 **fulSpeed**メンバー場合にのみ、IRB\_フラグ\_許可\_リモート\_無料フラグが設定され、IRB\_フラグ\_の使用\_プレ\_CALCULATE\_値のフラグが設定されていない**フラグ**IRB の。 その他のすべてのケースで新しい 1394 バス ドライバーを無視**fulSpeed**します。

[**要求\_設定\_デバイス\_XMIT\_プロパティ**](https://msdn.microsoft.com/library/windows/hardware/ff537662)  
速度を指定する\_フラグ\_*XXX*のフラグ、 **fulSpeed**メンバー。

### <a name="usetdevicexmitpropertiesfulspeed"></a>u.SetDeviceXmitProperties.fulSpeed

デバイスへのトランザクションの最大速度を指定します。 可能な速度の値は速度\_フラグ\_*XXX*ここで、 *XXX* (概算) の転送率 (mbps) です。

[**要求\_ASYNC\_ストリーム**](https://msdn.microsoft.com/library/windows/hardware/ff537635)  
速度を指定する\_フラグ\_*XXX*のフラグ、 **nSpeed**メンバー。

### <a name="uasyncstreamnspeed"></a>u.AsyncStream.nSpeed

転送速度を指定します。 可能な速度の値は速度\_フラグ\_*XXX*ここで、 *XXX* (概算) の転送率 (mbps) です。

[要求\_アイソクロナス\_変更\_ストリーム\_プロパティ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/1394/ns-1394-_irb_req_isoch_modify_stream_properties)速度を指定する\_フラグ\_*XXX*のフラグ、 **fulSpeed**メンバー。

### <a name="uisochmodifystreampropertiesfulspeed"></a>u.IsochModifyStreamProperties.fulSpeed

デバイスへのトランザクションの最大速度を指定します。 可能な速度の値は速度\_フラグ\_*XXX*ここで、 *XXX* (概算) の転送率 (mbps) です。

[**要求\_取得\_速度\_BETWEEN\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff537645)  
速度を指定する\_フラグ\_*XXX*のフラグ、 **fulSpeed**メンバー。

### <a name="ugetmaxspeedbetweendevicesfulspeed"></a>u.GetMaxSpeedBetweenDevices.fulSpeed

ソース デバイスと送信先デバイスのセット間の最大の可能なトランザクション速度を指定します。 返される値は、すべてのデバイスを同時にサポートする最大速度です。 可能な速度の値は速度\_フラグ\_*XXX*ここで、 *XXX* (概算) の転送率 (mbps) です。

> [!NOTE]
> クライアント ドライバーでは、使用を指定できますも\_SCODE\_速度フラグ**u.GetMaxSpeedBetweenDevices.fulFlags**を要求できる SCODE\_*XXX* \_レート速度コード値で返す**fulSpeed**速度ではなく\_フラグ\_xxx の値。

## <a name="related-topics"></a>関連トピック

[IEEE 1394 ドライバー スタック](https://docs.microsoft.com/windows-hardware/drivers/ieee/the-ieee-1394-driver-stack)  
[Windows 7 での IEEE 1394 バス ドライバー](https://docs.microsoft.com/windows-hardware/drivers/ieee/IEEE-1394-Bus-Driver-in-Windows-7)  
