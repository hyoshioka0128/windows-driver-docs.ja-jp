---
title: 仮想ミニポートの初期化
description: 仮想ミニポートの初期化
ms.assetid: b712fe29-fd56-4abd-bab6-e335350a20c2
keywords:
- 基になるアダプターが WDK ネットワークを開く
- 基になるアダプターを開く
- 仮想ミニポート WDK ネットワーク
- 仮想ミニポートの初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64ade6793baf5249b53c256bd5dc5b7e731b8f05
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824409"
---
# <a name="initializing-virtual-miniports"></a>仮想ミニポートの初期化





中間ドライバーは、基になるミニポートアダプターが正常に開かれ、要求を受け入れて仮想ミニポートで送信する準備ができた後に、その仮想ミニポートを初期化します。 中間ドライバーは、 [*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)関数から[**NdisIMInitializeDeviceInstanceEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisiminitializedeviceinstanceex)を1回以上呼び出して、1つまたは複数の仮想ミニポートの初期化を要求します。

基になるミニポートアダプターを開いたときに**NdisIMInitializeDeviceInstanceEx**を呼び出すために中間ドライバーが必要ない  に**注意**してください。 仮想ミニポートとオープンアダプターの間には、一対一のリレーションシップは必要ありません。

 

**NdisIMInitializeDeviceInstanceEx**の*driverinstance*パラメーターに、初期化する仮想ミニポートのデバイス名を設定します。 中間ドライバーは、 **UpperBindings**レジストリキーからデバイス名を取得します。

1つの物理 NIC に対して複数の仮想ミニポートをレイヤーする*n*対1の MUX 中間ドライバーの場合は、すべての仮想ミニポートにデバイス名が必要です。 MUX 中間ドライバーには、仮想ミニポートデバイス名の一覧を保持する notify オブジェクトが必要です。 一覧の推奨される場所は、 **UpperBindings**レジストリキーです。 この場合、 **UpperBindings**レジストリキーは、デバイス名の一覧を含む複数\_SZ エントリです。 MUX 中間ドライバーは、[デバイス名] の一覧に指定されているデバイス名ごとに**NdisIMInitializeDeviceInstanceEx**を呼び出します。

**NdisIMInitializeDeviceInstanceEx**を呼び出すと、中間ドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出して、指定された仮想ミニポートの初期化を実行します。これは、NDIS が\_デバイスを起動して、デバイスを起動するために開始される IRP\_\_を受け取った場合に発生します。 NDIS がこのような IRP を受信しない場合、NDIS は中間ドライバーの*MiniportInitializeEx*関数を呼び出しません。 *MiniportInitializeEx*の呼び出しは、後で発生する可能性があるため、必ずしも**NdisIMInitializeDeviceInstanceEx**の呼び出しのコンテキスト内にあるとは限りません。 NDIS が**NdisIMInitializeDeviceInstanceEx**の呼び出しで参照される仮想ミニポートに対して*MiniportInitializeEx*を呼び出さず、中間ドライバーが仮想ミニポートを必要としない場合、中間ドライバーは[**NdisIMCancelInitializeDeviceInstance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisimcancelinitializedeviceinstance)を呼び出して仮想ミニポートの初期化をキャンセルする必要があります。 たとえば、基になるミニポートへのバインドが成功した場合に、中間ドライバーが仮想ミニポートを作成したとします。 NDIS が*MiniportInitializeEx*を呼び出す前にバインドが削除された場合、中間ドライバーは**NdisIMCancelInitializeDeviceInstance**を呼び出してミニポートの初期化をキャンセルする必要があります。

*MiniportInitializeEx*は、仮想ミニポート固有のコンテキスト領域を割り当てて初期化する必要があります。 コンテキスト領域の指定の詳細については、「[仮想ミニポートの初期化](initializing-a-virtual-miniport.md)」を参照してください。

中間ドライバーは、逆シリアル化されたドライバーとして動作する必要があります。 逆シリアル化されたドライバーの詳細については、「シリアル化解除された[NDIS ミニポートドライバー](deserialized-ndis-miniport-drivers.md)

中間ドライバーは、管理する状態情報が適切に初期化されていることを確認する必要があります。 ドライバーが送信関連のリソースを必要とする場合 (たとえば、新しい[**net\_buffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)は、 [*Miniportsendnetbufferlists*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists)が次の下位の層に送信するネットワークデータの\_のリスト構造) を必要とします。この時点で、NET\_バッファー\_リスト構造プールを割り当てることができます。

 

 





