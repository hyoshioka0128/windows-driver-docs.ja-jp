---
title: Windows 7 のデバイス ドライバー インターフェイス (DDI) の変更点
description: このトピックでは、新しい1394バスドライバーをサポートする一般的な DDI 変更の概要を示します。
ms.assetid: 5473C6AC-284C-41B1-AA67-75696BE96C24
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2692275893a29f067c68838eaa91017a6e64b904
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841541"
---
# <a name="device-driver-interface-ddi-changes-in-windows-7"></a>Windows 7 のデバイス ドライバー インターフェイス (DDI) の変更点

Windows 7 には、カーネルモードドライバーフレームワーク (KMDF) を使用して実装される新しい IEEE 1394 バスドライバーである 1394ohci .sys が含まれています。 新しい1394バスドライバーは、ポート/ミニポート configuration--1394bus と ochi1394 のレガシ IEEE バスドライバーを置き換えます。 1394ohci でサポートされている新機能に新しい DDIs が追加されました。 さらに、特定の 1394 DDIs は、1394b 仕様で定義されているよりも高速にサポートするように変更され、1394クライアントドライバーの開発を簡略化するために改善されました。

このトピックでは、新しい1394バスドライバーをサポートする一般的な DDI 変更の概要を示します。

* [拡張バスリセット通知](#extended-bus-reset-notification)
* [PHY パケットサポート用の新しい Ioctl](#new-ioctls-for-phy-packet-support)
* [構成 ROM を取得するための新しい IOCTL](#new-ioctl-to-retrieve-configuration-rom)
* [IEEE バスドライバー DDI の変更](#ieee-bus-driver-ddi-changes)
* [速度とペイロードのサイズに関する新しいフラグ](#new-flags-for-speed-and-payload-size)
* [IEEE 1394 IOCTL の変更](#ieee-1394-ioctl-changes)
* [関連トピック](#related-topics)

## <a name="extended-bus-reset-notification"></a>拡張バスリセット通知

1394ohci バスドライバーは、拡張バスリセット通知をサポートしています。 この通知では、バスのリセット通知のコンテキストで、バスの現在の世代 (世代数やノード id など) に関する情報が1394クライアントドライバーに返されます。 この情報を使用すると、1394クライアントドライバーが、生成カウント、ノード id、およびその他の情報の取得をバスリセット通知ハンドラーと同期する必要がなくなります。

拡張バスリセット通知に登録するには、クライアントドライバーが既存の[**要求\_バス\_** ](https://msdn.microsoft.com/library/windows/hardware/ff537638)使用して\_通知 i/o 要求をリセットし、u で新しい拡張\_通知\_ルーチンフラグを指定し**ます。BusResetNotification. の**パラメーター。 拡張\_通知\_ルーチンフラグが指定さ**れている**場合は、\_データ構造を[**リセット\_バス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_bus_reset_data)をポイントします。

## <a name="new-ioctls-for-phy-packet-support"></a>PHY パケットサポート用の新しい Ioctl

1394ohci のドライバーは、IEEE 1394a 仕様で定義されているように、PHY パケットを送受信するための次の新しい DDIs を公開しています。

* [ **\_PHY\_パケットの送信を要求\_** ](https://msdn.microsoft.com/library/windows/hardware/gg266407)
* [**要求\_\_PHY\_パケットを受信します**](https://msdn.microsoft.com/library/windows/hardware/gg266406)

[**要求\_\_phy\_構成\_パケットを送信**](https://msdn.microsoft.com/library/windows/hardware/ff537661)するのではなく、 [ **\_phy\_パケット**](https://msdn.microsoft.com/library/windows/hardware/gg266407)i/o 要求を送信\_には、新しい要求を使用する必要があります。 後者の i/o 要求では、生成数を指定することはできません。そのため、1394バスの誤った生成に PHY パケットが送信される可能性があります。

## <a name="new-ioctl-to-retrieve-configuration-rom"></a>構成 ROM を取得するための新しい IOCTL

新しい IOCTL、 [**REQUEST\_GET\_CONFIG\_rom**](https://msdn.microsoft.com/library/windows/hardware/gg266404)は、ノードの構成 rom のコンテンツを返します。最大サイズは 1 kb です。 1394ohci バスドライバーでサポートされているのは、レガシ1394バスドライバーと同じ 1 KB 構成 Rom のみです。

## <a name="ieee-bus-driver-ddi-changes"></a>IEEE バスドライバー DDI の変更

次の表では、新しい1394バスドライバーとレガシ1394バスドライバーによって公開される DDIs の機能動作の変更について説明します。

| デバイスドライバーインターフェイス                                                              | 説明                                                                                                                                                                                                                                                                          |
|--------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [**ローカル\_ホストの\_情報\_取得\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff537644)             | 1394ohci. sys バスドライバーでは、 **Nlevel**を設定して\_ホスト\_CSR\_コンテンツを取得し、\_\_マップの速度を**CsrBaseAddress**として指定することはサポートされていません。 速度マップは、IEEE 1394a 仕様では廃止されています。                                                                |
| [**トポロジ\_マップの\_速度\_取得\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff537646)     | [**要求\_\_速度\_トポロジ\_マップ**](https://msdn.microsoft.com/library/windows/hardware/ff537646)は、Windows 2000 以降のバージョンのオペレーティングシステムでは非推奨とされています。 この要求を1394ohci に送信すると、状態\_無効\_パラメーターとして返されます。                                            |
| [**要求\_\_デバイス間の\_速度\_を取得する**](https://msdn.microsoft.com/library/windows/hardware/ff537645) | 要求の送信[ **\_\_\_\_デバイス間**](https://msdn.microsoft.com/library/windows/hardware/ff537645)の要求の間に、1394ohci、ローカルノードとデバイス間の速度を取得します。 USE\_LOCAL\_NODE フラグは、 **GetMaxSpeedBetweenDevices**パラメーターで設定する必要があります。 |

## <a name="new-flags-for-speed-and-payload-size"></a>速度とペイロードのサイズに関する新しいフラグ

Windows 7 Windows Driver Kit の1394ヘッダーファイル (1394) では、高速でより高速なペイロード用に新しいフラグが定義されています。 このセクションでは、これらの新しいフラグと値について説明します。

次の表は、新しくサポートされる各速度の非同期ペイロードの最大サイズを示しています。

| Flag                       | Value | 説明 |
|----------------------------|-------|-------------|
| 非同期\_ペイロード\_800\_率  | 4096  | 800 Mb/秒    |
| 非同期\_ペイロード\_1600\_率 | 4096  | 160 Mb/秒    |
| 非同期\_ペイロード\_3200\_率 | 4096  | 3200 Mb/秒   |

次の表は、新たにサポートされた各速度の速度フラグを示しています。

| Flag               | Value | 説明 |
|--------------------|-------|-------------|
| 速度\_フラグ\_800  | 0x08  | 800 Mb/秒    |
| 速度\_フラグ\_1600 | 0x10  | 160 Mb/秒    |
| 速度\_フラグ\_3200 | 0x20  | 3200 Mb/秒   |

次の表は、新たにサポートされた各速度の速度コード値を示しています。

| Flag              | Value | 説明 |
|-------------------|-------|-------------|
| SCODE\_800\_率  | 3     | 800 Mb/秒    |
| SCODE\_1600\_率 | ホーム フォルダーが置かれているコンピューターにアクセスできない     | 160 Mb/秒    |
| SCODE\_3200\_率 | 5     | 3200 Mb/秒   |

## <a name="ieee-1394-ioctl-changes"></a>IEEE 1394 IOCTL の変更

このセクションでは、新しい速度とペイロードサイズの値を使用する 1394 i/o 要求について説明します。

[**要求\_非同期\_読み取り**](https://msdn.microsoft.com/library/windows/hardware/ff537634)  
**AsyncRead. nBlockSize**

1394ノードから読み取られるデータストリーム内の各ブロックのサイズを指定します。 このパラメーターが0の場合、raw モードのアドレス指定が使用されていない限り、選択されたデバイスと速度の最大パケットサイズが、これらの読み取り要求を発行するために使用されます。

**Nblocksize**メンバーでは、ASYNC\_PAYLOAD\_*XXX*フラグを指定できます。 クライアントドライバーが**Nblocksize**メンバーを0に設定することをお勧めします。これにより、raw モードのアドレス指定が使用されない限り、1394バス driver1394ohci はサポートされている最大値を使用します。

Raw モードのアドレス指定が使用されている場合、クライアントドライバーは、接続速度でデバイスでサポートされている非同期ペイロードの最大サイズに**Nblocksize**メンバーを設定する必要があります。

未加工モードのアドレス指定の詳細については、「 [IEEE 1394 バスでの非同期 I/o 要求パケットの送信](https://docs.microsoft.com/windows-hardware/drivers/ieee/sending-asynchronous-i-o-request-packets-on-the-ieee-1394-bus)」を参照してください。

[**要求\_非同期\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff537636)  

### <a name="uasyncreadnblocksize"></a>AsyncRead. nBlockSize

1394ノードに書き込まれるデータストリーム内の各ブロックのサイズを指定します。 このパラメーターが0の場合、raw モードのアドレス指定が使用されていない限り、選択した速度の最大パケットサイズを使用してこれらの書き込み要求を分割します。

**Nblocksize**メンバーでは、ASYNC\_PAYLOAD\_*XXX*フラグを指定できます。 クライアントドライバーが**Nblocksize**メンバーを0に設定することをお勧めします。これにより、raw モードアドレス指定が使用されていない限り、1394バスドライバーはサポートされる最大値を使用します。

Raw モードのアドレス指定が使用されている場合、クライアントドライバーは、接続速度でデバイスでサポートされている非同期ペイロードの最大サイズに**Nblocksize**メンバーを設定する必要があります。

[**要求\_ISOCH\_割り当て\_帯域幅**](https://msdn.microsoft.com/library/windows/hardware/ff537647)  
"**速度"** \_フラグ\_*XXX*フラグを指定できます。 新しい1394バスドライバーは、 **SpeedSelected**メンバーのフラグ\_*XXX*フラグ\_新しい速度を返すことができます。

### <a name="uisochallocatebandwidthfulspeed"></a>u. IsochAllocateBandwidth 幅

帯域幅の割り当てに使用する接続速度を指定します。 使用可能な速度の値は、 *xxx*\_の速度\_フラグです。 *xxx*は (概算) 転送速度 (mbps) です。

### <a name="uisochallocatebandwidthspeedselected"></a>u. IsochAllocateBandwidth

帯域幅を割り当てるために選択される実際の速度を指定します。 この値は、 *XXX*\_の速度\_フラグの1つです (対数のメンバーの説明を**参照して**ください)。

[**要求\_ISOCH\_割り当て\_リソース**](https://msdn.microsoft.com/library/windows/hardware/ff537649)  
"**速度"** \_フラグ\_*XXX*フラグを指定できます。

### <a name="uisochallocateresourcesfulspeed"></a>IsochAllocateResources 速度

チャネルでの通信に使用する接続速度を指定します。 使用可能な速度の値は、 *xxx*\_の速度\_フラグです。 *xxx*は (概算) 転送速度 (mbps) です。

[**要求\_ISOCH\_空き\_帯域幅**](https://msdn.microsoft.com/library/windows/hardware/ff537652)  
"**速度"** \_フラグ\_*XXX*フラグを指定できます。

### <a name="uisochfreebandwidthfulspeed"></a>u. IsochFreeBandwidth 幅

帯域幅を解放するために使用する接続速度を指定します。 使用可能な速度の値は、 *xxx*\_の速度\_フラグです。 *xxx*は (概算) 転送速度 (mbps) です。

> [!NOTE]
> 新しい1394バスドライバーで**は、IRB**\_フラグ\_有効にすると\_REMOTE\_FREE フラグが設定され、IRB\_フラグ\_使用して\_値を計算\_を使用します。IRB の**フラグにフラグ**が設定されていません。 それ以外の場合、新しい1394バスドライバーは、1対1の**速度**を無視します。

[**デバイス\_XMIT\_プロパティ\_設定\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff537662)  
"**速度"** \_フラグ\_*XXX*フラグを指定できます。

### <a name="usetdevicexmitpropertiesfulspeed"></a>SetDeviceXmitProperties 速度

デバイスに対するトランザクションの最大速度を指定します。 使用可能な速度の値は、 *xxx*\_の速度\_フラグです。 *xxx*は (概算) 転送速度 (mbps) です。

[**要求\_非同期\_ストリーム**](https://msdn.microsoft.com/library/windows/hardware/ff537635)  
**Nspeed**メンバーでは、SPEED\_フラグ\_*XXX*フラグを指定できます。

### <a name="uasyncstreamnspeed"></a>u. AsyncStream. n 速度

転送速度を指定します。 使用可能な速度の値は、 *xxx*\_の速度\_フラグです。 *xxx*は (概算) 転送速度 (mbps) です。

[要求\_ISOCH\_変更\_ストリーム\_のプロパティ](https://docs.microsoft.com/windows-hardware/drivers/ddi/1394/ns-1394-_irb_req_isoch_modify_stream_properties)"**速度"** \_フラグ\_*XXX*フラグを指定できます。

### <a name="uisochmodifystreampropertiesfulspeed"></a>u. IsochModifyStreamProperties. 米国の速度

デバイスに対するトランザクションの最大速度を指定します。 使用可能な速度の値は、 *xxx*\_の速度\_フラグです。 *xxx*は (概算) 転送速度 (mbps) です。

[**要求\_\_デバイス間の\_速度\_を取得する**](https://msdn.microsoft.com/library/windows/hardware/ff537645)  
"**速度"** \_フラグ\_*XXX*フラグを指定できます。

### <a name="ugetmaxspeedbetweendevicesfulspeed"></a>GetMaxSpeedBetweenDevices 速度

ソースデバイスとターゲットデバイスのセットの間で可能なトランザクションの最大速度を指定します。 返される値は、すべてのデバイスが同時にサポートする最大速度です。 使用可能な速度の値は、 *xxx*\_の速度\_フラグです。 *xxx*は (概算) 転送速度 (mbps) です。

> [!NOTE]
> クライアントドライバーでは、 **GetMaxSpeedBetweenDevices**で SCODE\_speed フラグを\_使用するように指定することもできます。このフラグは、Scode\_*XXX*\_レート速度のコード値が速度ではなく、1対 1**速度**で返されるように要求します。\_フラグ\_xxx 値です。

## <a name="related-topics"></a>関連トピック

[IEEE 1394 ドライバー スタック](https://docs.microsoft.com/windows-hardware/drivers/ieee/the-ieee-1394-driver-stack)  
[Windows 7 の IEEE 1394 バスドライバー](https://docs.microsoft.com/windows-hardware/drivers/ieee/IEEE-1394-Bus-Driver-in-Windows-7)  
