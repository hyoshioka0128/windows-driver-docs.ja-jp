---
title: カーネル ストリーミングに関する考慮事項
description: カーネル ストリーミングに関する考慮事項のトピックで要件を明確にし、Bluetooth に関連するその他の注意事項は、オーディオ ストリーミングをバイパスします。
ms.assetid: CFC4ACA0-050D-48E1-AA6A-7649040EBF7A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f867918bbfad43a430fc2b1eca2e6409d0d4899
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333395"
---
# <a name="kernel-streaming-considerations"></a>カーネル ストリーミングに関する考慮事項


カーネル ストリーミングに関する考慮事項のトピックでは、要件とすべてのオーディオ ドライバー以外の他の特別な考慮事項を明確です。 これらは、カーネルの Bluetooth バイパスのオーディオのストリーミングに関連する複数の考慮事項をストリーミングします。

オーディオ ドライバーは、「プル モード」を含む、WaveRT ポート ドライバーに完全にサポートする必要があります。 詳細については、次を参照してください。 [WaveRT ポート ドライバー導入](introducing-the-wavert-port-driver.md)します。 および実装する必要はありませんが、同期接続指向 (SCO) のハードウェアのオーディオ エンジンが出力をバイパス、行っても問題はありません。

Windows ロゴの要件形式のサポートにはには、Bluetooth の例外が含まれます。

オーディオ ドライバーには、側波帯ハードウェア使用可能な形式をサポートする必要があります。 これは、通常、8 KHz のモノ オーディオ ストリーミングです。

## <a name="span-idtopologyspanspan-idtopologyspanspan-idtopologyspantopology"></a><span id="Topology"></span><span id="topology"></span><span id="TOPOLOGY"></span>トポロジ


ハンズフリーのすべてのデバイスでは、両方のキャプチャをサポートし、レンダリングします。 オーディオ ドライバーは、ストリーミング (KS) カーネルを公開する必要がありますように両方をサポートする次の図に示すように楽にデバイスのトポロジのレンダリング、キャプチャします。

![ks トポロジ レンダリングとキャプチャをサポートするために、楽にデバイスのオーディオ ドライバーが公開していることを示す図。](images/btth-bypass-topology.png)

**注**  オーディオ ドライバー開発者は、両方をキャプチャおよびレンダリング パス、または別のフィルター処理のために、1 つのフィルターを実装するかどうかを選択できます。 ただし、HFP デバイスのみを使うと、1 つのファイル オブジェクト guid\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_HCIBYPASS デバイス インターフェイス。 したがって 2 つのフィルターを使用する設計では、両方のフィルターを 1 つのファイル オブジェクトの共有を許可する必要があります。

 

DAC と ADC ノードは、アナログ/デジタル変換を表しますが、KS プロパティをサポートしていません。

ボリューム ノード サポート[ **KSPROPERTY\_オーディオ\_VOLUMELEVEL** ](https://msdn.microsoft.com/library/windows/hardware/ff537309)と[ **KSEVENT\_コントロール\_変更** ](https://msdn.microsoft.com/library/windows/hardware/ff537128) HFP ドライバーにとると GETVOLUMESTATUSUPDATE Ioctl を送信しています。

[ボリューム] ノードは、次のように実装する必要があります。

-   Bluetooth ヘッドセットには、ボリューム コントロールがサポートする場合、オーディオ ドライバーは KS トポロジでは、[ボリューム] ノードを含める必要があります。 オーディオ ドライバーのボリューム プロパティ ハンドラーは、上記の IOCLTs をボリュームを処理するために、Bluetooth HFP ドライバーに送信します。

-   Bluetooth ヘッドセットはハードウェアのボリュームを実装していないコーデック (または DSP) がハードウェアのボリューム、オーディオ ドライバーはコーデック (または DSP) のボリューム コントロールを処理する必要があります。

-   Bluetooth ヘッドセットとオーディオ デバイスはハードウェアのボリューム コントロールを持たない場合、[ボリューム] ノードを提示されませんし、Windows はソフトウェアのボリューム コントロール ノードを挿入します。

ミュート ノードは省略可能です。 DSP またはオーディオ コーデックは、Bluetooth コント ローラーに渡す前にバイパス PCM の信号をミュートする機能を提供します。 場合にのみ、オーディオ ドライバーは、[ミュート] ノードを実装する必要があります。 ミュート ノード サポート[ **KSPROPERTY\_オーディオ\_ミュート**](https://msdn.microsoft.com/library/windows/hardware/ff537293)します。

## <a name="span-idpropertyrequestsspanspan-idpropertyrequestsspanspan-idpropertyrequestsspanproperty-requests"></a><span id="Property_requests"></span><span id="property_requests"></span><span id="PROPERTY_REQUESTS"></span>プロパティの要求


オーディオ ドライバーでは、次 KS プロパティを使用して、すべてのオーディオ ジャックに関する情報を取得またはオーディオのパスでジャックします。 おり、オーディオ ドライバーでは、適切なプロパティの要求をまたはオーディオのパスで Bluetooth オーディオ デバイスへの接続を中断させるのにでも使用できます。

**KSPROPERTY\_ジャック\_の説明**

このプロパティを返します、 [ **KSJACK\_説明**](https://msdn.microsoft.com/library/windows/hardware/ff537136)構造体。 オーディオ ドライバーを設定する必要があります、 [ **KSPROPERTY\_ジャック\_説明**](https://msdn.microsoft.com/library/windows/hardware/ff537364)フィールドを次のようにします。
ChannelMapping KSAUDIO =\_スピーカー\_MONO 色 = 0 ConnectionType eConnTypeOtherDigital 地理的位置情報を = = eGeoLocNotApplicable GenLocation eGenLocOther PortConnection を = = ePortConnUnknown IsConnected = &lt; *現在の接続状態の BOOL* &gt; **KSPROPERTY\_ジャック\_DESCRIPTION2**

このプロパティを返します、 [ **KSJACK\_DESCRIPTION2** ](https://msdn.microsoft.com/library/windows/hardware/ff537138)構造体。 オーディオ ドライバーを設定する必要があります、 [ **KSPROPERTY\_ジャック\_DESCRIPTION2** ](https://msdn.microsoft.com/library/windows/hardware/ff537365)フィールドを次のようにします。
DeviceStateInfo = 0 JackCapabilities = JACKDESC2\_プレゼンス\_検出\_機能**KSPROPERTY\_ONESHOT\_再接続**

オーディオ ドライバーのフィルターをサポートする必要があります[ **KSPROPERTY\_ONESHOT\_再接続**](https://msdn.microsoft.com/library/windows/hardware/ff537369)します。 オーディオ ドライバーの送信を作成し、この構造体の初期化、 [ **IOCTL\_BTHHFP\_デバイス\_要求\_CONNECT** ](https://msdn.microsoft.com/library/windows/hardware/dn265114) HFP ドライバーにします。 HFP ドライバーは、この要求を完了し、オーディオの Bluetooth デバイスに非同期的に接続を試みます。
**KSPROPERTY\_ONESHOT\_切断**

オーディオ ドライバーのフィルターをサポートする必要があります[ **KSPROPERTY\_ONESHOT\_切断**](https://msdn.microsoft.com/library/windows/hardware/hh706181)します。 オーディオ ドライバーの送信を作成し、この構造体の初期化、 [ **IOCTL\_BTHHFP\_デバイス\_要求\_切断**](https://msdn.microsoft.com/library/windows/hardware/dn265115) HFP ドライバーにします。 HFP ドライバーでは、この要求が完了すると、Bluetooth のオーディオ デバイスから非同期的に切断しようとします。
オーディオ ドライバーでは、これらのプロパティをサポートするときに、コントロール パネルの [サウンド] ダイアログ ボックスは HFP エンドポイントの接続と切断のコマンドを公開します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[操作の理論を概説します。](theory-of-operation.md)  



