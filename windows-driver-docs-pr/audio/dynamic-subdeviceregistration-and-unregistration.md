---
title: 動的サブデバイスの登録と登録解除
description: 動的サブデバイスの登録と登録解除
ms.assetid: 7157b7b3-655b-49d9-be45-c4a86a3cc82d
keywords:
- 動的サブデバイス WDK オーディオ
- オーディオサブデバイス WDK
- オーディオサブデバイスの登録 (WDK)
- オーディオサブデバイスの登録解除 (WDK)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 870eda232a86e7316b008a3e14a52980d8a80802
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831253"
---
# <a name="dynamic-subdevice-registration-and-unregistration"></a>動的サブデバイスの登録と登録解除


何らかの形式のジャックのプレゼンス検出をサポートするデバイスは動的デバイスと呼ばれ、そのジャックは、 [**Ksk プロパティ\_ジャック\_DESCRIPTION**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-jack-description)プロパティをサポートしている必要があります。 次の手順では、動的デバイスのドライバーが、これらの動的デバイスに関連付けられたサブデバイスを作成、登録、または登録解除するために使用するアルゴリズムについて説明します。 サブデバイスは、フィルターの形式で作成されます。

次の手順では、オーディオデバイスドライバーが読み込まれたときに、オーディオデバイスがジャックに接続されている場合の動作を示します。

1.  ドライバーは、ジャックのプレゼンス検出を使用して、ジャックに接続されているデバイスがあることを確認します。 ドライバーは、 [**PcregiPortcls サブデバイス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregistersubdevice)を呼び出して、トポロジフィルターを[](introduction-to-port-class.md)に登録します。 トポロジフィルターの登録の結果として、 [**KSCATEGORY\_AUDIO**](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-audio)インターフェイスが作成されます。

2.  オーディオスタックには、 **KSCATEGORY\_audio**インターフェイスが作成されると通知されます。 [audioendpoint Builder](audio-endpoint-builder-algorithm.md)は、関連付けられているエンドポイントを作成および初期化し、その状態をアクティブに設定します。

3.  ドライバーが wave フィルターを Portcls に登録すると、オーディオスタックに通知されます。

4.  ドライバーは、 [**Pcregisterphysicalconnection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnection)を呼び出して、ウェーブフィルターをトポロジフィルターに接続します。 この物理接続は Portcls に登録されます。

5.  ドライバーは、 [ **\_DESCRIPTION**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksjack-description)構造体の IsConnected メンバーを**TRUE**に設定して、ジャックにデバイスが接続されていることを示します。

**注**   オーディオデバイスにジャックのプレゼンス検出がない場合は、 **IsConnected**メンバーが常に**TRUE**である必要があります。 デバイスがジャックのプレゼンス検出をサポートしているかどうかを確認するために、クライアントアプリケーションは[IKsJackDescription2:: GetJackDescription2](https://go.microsoft.com/fwlink/p/?linkid=143698)を呼び出して、 [**KSJACK\_DESCRIPTION2**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksjack-description2)構造体の JackCapabilities フラグを読み取ることができます。 このフラグに\_機能ビットセット\_検出する\_JACKDESC2 がある場合、エンドポイントがジャックプレゼンス検出をサポートしていることを示します。 その場合は、 **IsConnected**メンバーの戻り値を、ジャックの挿入状態の正確なリフレクションとして解釈できます。

 

次の手順では、ドライバーの読み込み時にオーディオデバイスがジャックに接続されていない場合の動作について説明します。

1.  ドライバーは、ジャックのプレゼンス検出を使用して、ジャックに接続されているデバイスがないことを確認します。 しかし、これにより、Portcls にジャックのトポロジフィルターが登録され、 **KSCATEGORY\_AUDIO**インターフェイスが作成されます。

2.  オーディオスタックには、 **KSCATEGORY\_audio**インターフェイスが作成されると通知されます。 AudioEndpointBuilder は、ミニポートドライバーに対してクエリを行い、 **Ksk ジャック\_DESCRIPTION**プロパティから、エンドポイントの状態を "切断" として設定するかどうかを判断します。

3.  ドライバーは、 **Ksk ジャック\_DESCRIPTION**構造体の**IsConnected**メンバーを**FALSE**に設定して、ジャックにデバイスが接続されていないことを示します。

オーディオエンドポイントのさまざまな状態の詳細については、「[オーディオエンドポイントビルダーアルゴリズム](audio-endpoint-builder-algorithm.md)」を参照してください。

サブデバイスの登録と登録解除のプロセスに関する前述の説明に従って、ジャックの存在検出をサポートするデバイスドライバーは、プラグの挿入と削除に応答して、次のように対処する必要があります。

**プラグ挿入へのデバイスドライバーの応答**

1.  ドライバーは、Portcls に wave フィルターを登録するために、 **Pcregi サブデバイス**を呼び出す必要があります。
    ドライバーが、ジャックにデバイスが接続されていない状態でドライバーが読み込まれたときに、トポロジフィルターで既に " **Pcregi" サブデバイス**と呼ばれてい  **ことに注意**してください。

     

2.  ドライバーは、Portcls との "wave to topology filter" 接続を登録するために、 **Pcregiphysicalconnection**を呼び出す必要があります。

3.  ドライバーは、 **Ksk ジャック\_DESCRIPTION**構造体の**IsConnected**メンバーを**TRUE**に設定する必要があります。

**プラグの削除に対するデバイスドライバーの応答**

1.  ドライバーは、wave フィルターとトポロジフィルター間の物理接続の登録を解除するために、 [**Iunregisterphysicalconnection:: unregisterphysicalconnection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iunregisterphysicalconnection-unregisterphysicalconnection)を呼び出す必要があります。

2.  ドライバーは、ウェーブフィルターの登録を解除するために、 [**Iunregistersubdevice:: unregistersubdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iunregistersubdevice-unregistersubdevice)を呼び出す必要があります。

3.  ドライバーは、 **Ksk ジャック\_DESCRIPTION**構造体**FALSE**の**IsConnected**メンバーを設定する必要があります。

 

 




