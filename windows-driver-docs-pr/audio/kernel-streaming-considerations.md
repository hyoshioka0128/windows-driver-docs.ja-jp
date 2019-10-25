---
title: カーネル ストリーミングに関する考慮事項
description: 「カーネルストリーミングに関する考慮事項」のトピックでは、Bluetooth バイパスオーディオストリーミングに関連する要件とその他の特別な考慮事項を明確にしています。
ms.assetid: CFC4ACA0-050D-48E1-AA6A-7649040EBF7A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71e1f44397d578f78736546011a930a5eab39669
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833170"
---
# <a name="kernel-streaming-considerations"></a>カーネル ストリーミングに関する考慮事項


カーネルストリーミングに関する考慮事項のトピックでは、すべてのオーディオドライバーの要件とその他の特別な考慮事項を明確にしています。 これらは、Bluetooth バイパスオーディオストリーミングに関連するカーネルストリーミングの考慮事項です。

オーディオドライバーは、"プルモード" を含む WaveRT ポートドライバーを完全にサポートする必要があります。 詳細については、「 [wavert ポートドライバーの概要](introducing-the-wavert-port-driver.md)」を参照してください。 また、同期接続指向 (SCO) バイパス出力にハードウェアオーディオエンジンを実装する必要はありませんが、そのような問題はありません。

形式サポートの Windows ロゴ要件には、Bluetooth の例外が含まれています。

オーディオドライバーは、sideband ハードウェアによって可能な形式をサポートする必要があります。 これは通常、8KHz mono オーディオストリーミングです。

## <a name="span-idtopologyspanspan-idtopologyspanspan-idtopologyspantopology"></a><span id="Topology"></span><span id="topology"></span><span id="TOPOLOGY"></span>モジュール


すべての Bluetooth ハンドフリーデバイスは、キャプチャとレンダリングの両方をサポートしています。 そのため、オーディオドライバーは、レンダリングとキャプチャの両方をサポートするために、次の図に示すように、ハンズフリーデバイス用のカーネルストリーミング (KS) トポロジを公開する必要があります。

![レンダリングとキャプチャをサポートするために、オーディオドライバーがハンドフリーデバイス用に公開する ks トポロジを示す図。](images/btth-bypass-topology.png)

**  オーディオ**ドライバーの開発者は、キャプチャパスとレンダリングパスの両方に対して1つのフィルターを実装するか、または個別のフィルターを実装するかを選択できます。 ただし、HFP デバイスでは、GUID\_DEVINTERFACE\_BLUETOOTH\_HFP\_SCO\_HCIバイパスデバイスインターフェイスで1つのファイルオブジェクトのみを使用できます。 したがって、2つのフィルターを使用する設計では、両方のフィルターで1つのファイルオブジェクトを共有できるようにする必要があります。

 

DAC ノードと ADC ノードは、アナログ/デジタル変換を表しますが、すべての KS プロパティをサポートしているわけではありません。

このボリュームノードでは、HFP ドライバーに SETVOLUME および GETVOLUMESTATUSUPDATE の Ioctl を送信することによって、VOLUMELEVEL と[**KSEVENT\_の\_変更**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksevent-control-change)によって、 [**KSK プロパティ\_AUDIO\_** ](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-volumelevel)がサポートされます。

ボリュームノードは次のように実装する必要があります。

-   Bluetooth ヘッドセットがボリュームコントロールをサポートしている場合、オーディオドライバーには、その KS トポロジにボリュームノードが含まれている必要があります。 オーディオドライバーのボリュームプロパティハンドラーは、上記の IOCLTs を Bluetooth HFP ドライバーに送信して、ボリュームを処理します。

-   Bluetooth ヘッドセットがハードウェアボリュームを実装しておらず、コーデック (または DSP) にハードウェアボリュームがある場合、オーディオドライバーはコーデック (または DSP) のボリュームコントロールを処理する必要があります。

-   Bluetooth ヘッドセットとオーディオデバイスにハードウェアボリュームコントロールがない場合、ボリュームノードは表示されず、Windows によってソフトウェアボリュームコントロールノードが挿入されます。

ミュートノードはオプションです。 オーディオドライバーがミュートノードを実装する必要があるのは、DSP または audio コーデックが、デバイスを Bluetooth コントローラーに渡す前に、バイパス PCM 信号をミュートする機能を提供する場合のみです。 ミュートノードでは、[**オーディオ\_ミュート\_Ksk プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-audio-mute)がサポートされています。

## <a name="span-idproperty_requestsspanspan-idproperty_requestsspanspan-idproperty_requestsspanproperty-requests"></a><span id="Property_requests"></span><span id="property_requests"></span><span id="PROPERTY_REQUESTS"></span>プロパティ要求


オーディオドライバーは、次の KS プロパティを使用して、オーディオパス内のオーディオジャックまたはジャックに関する情報を取得します。 また、オーディオドライバーは、適切なプロパティ要求を使用して、オーディオパス内の任意の Bluetooth オーディオデバイスへの接続を確立または切断することもできます。

**KSK プロパティ\_ジャック\_の説明**

このプロパティは、 [**Ksk ジャック\_DESCRIPTION**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksjack-description)構造体を返します。 オーディオドライバーでは、次のように[**Ksk プロパティ\_JACK\_DESCRIPTION**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-jack-description)フィールドを設定する必要があります。
ChannelMapping = KSAUDIO\_スピーカー\_MONO Color = 0 ConnectionType = eConnTypeOtherDigital 位置情報 = eGeoLocNotApplicable GenLocation = Egeolocnotapplicable = &lt;*ブール値の場合は BOOL です。接続の状態*&gt; **ksk プロパティ\_ジャック\_DESCRIPTION2**

このプロパティは、 [**DESCRIPTION2 構造体\_Ksk ジャック**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksjack-description2)を返します。 オーディオドライバーでは、次のように[**Ksk プロパティ\_JACK\_DESCRIPTION2**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-jack-description2)フィールドを設定する必要があります。
DeviceStateInfo = 0 JackCapabilities = JACKDESC2\_プレゼンス\_検出\_機能**Ksproperty\_ONESHOT\_再接続**

オーディオドライバーのフィルターは、 [**ONESHOT\_再接続**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-oneshot-reconnect)するために、ksproperty\_サポートする必要があります。 この構造体を作成して初期化するために、オーディオドライバーは[**BTHHFP\_デバイス\_要求\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_request_connect) hfp ドライバーに接続するように、IOCTL\_を送信します。 HFP ドライバーはこの要求を完了し、Bluetooth オーディオデバイスへの非同期接続を試みます。
**KSK プロパティ\_ONESHOT\_切断**

オーディオドライバーのフィルターでは、 [**ONESHOT\_切断を\_Ksk プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-oneshot-disconnect)がサポートされている必要があります。 この構造体を作成して初期化するために、オーディオドライバーは[**BTHHFP\_デバイス\_要求\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_request_disconnect) hfp ドライバーへの切断を\_送信します。 HFP ドライバーはこの要求を完了し、Bluetooth オーディオデバイスとの非同期の切断を試みます。
オーディオドライバーでこれらのプロパティがサポートされている場合、コントロールパネルの [サウンド] ダイアログボックスには、HFP エンドポイントの [接続] および [切断] コマンドが表示されます。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[操作の理論](theory-of-operation.md)  



