---
title: PCM 以外のピン ファクトリの要件
description: PCM 以外のピン ファクトリの要件
ms.assetid: 3ba5da2e-f96f-4645-8a37-dd985287a9f2
keywords:
- 非 PCM オーディオ形式 WDK、暗証番号 (pin) ファクトリ
- 暗証番号 (pin) ファクトリ WDK オーディオ
- 交差部分のデータ ハンドラーの WDK オーディオ、wave 形式の非 PCM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29c63c268a9631e7dcc4f87fdd77f9eb6b0b5949
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355283"
---
# <a name="requirements-for-a-non-pcm-pin-factory"></a>PCM 以外のピン ファクトリの要件


## <span id="requirements_for_a_non_pcm_pin_factory"></span><span id="REQUIREMENTS_FOR_A_NON_PCM_PIN_FACTORY"></span>


Windows xp 以降、および Microsoft Windows Me、非 PCM を再生ドライバー [ **WAVEFORMATEX** ](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)形式は次のガイドラインに従って PCM 以外の pin を公開する必要があります。

最初に、PCM 非データ形式は、PCM の暗証番号 (pin) ファクトリから別のピン留めするファクトリを定義します。 PCM と PCM 以外は、自動的にピン留めする唯一のインスタンスが KMixer に割り当てられるため、同じ単一インスタンスの暗証番号 (pin) ファクトリを共有することはできません。 暗証番号 (pin) ファクトリは、複数のインスタンスをサポートする PCM および非 PCM が同じ pin ファクトリで共存できます。 この場合、ただしは保証できないことは、これらのピン留めするインスタンスは実行時に非 PCM クライアントに使用可能な - PCM クライアントが既にが割り当てられていること。 最も安全なオプションでは、PCM 以外の形式のピン留めする個別のファクトリを提供します。

Pin が検出され、DirectSound 8 で使用されるためには、PCM を既にサポートしているフィルターでこの非 PCM 暗証番号 (pin) ファクトリを定義します。 それ以外の場合、DirectSound では、非 PCM の暗証番号 (pin) が検出されません。 PCM をまったくサポートしないデバイスが非 PCM 形式をサポートできないことも意味します。

第 2 に、実装、[交差部分のデータ ハンドラー](proprietary-data-intersection-handlers.md)非 PCM pin にします。 PortCls、組み込みのハンドラーを提供しますが、この既定のハンドラーは、PCM 以外の形式の独自のハンドラーを追加する必要がありますので常に、PCM を選択します。 WAVE をサポートする必要がありますいない\_形式\_非 PCM pin の積集合のハンドラーで PCM。 このハンドラーを呼び出すことができるに注意してください、 *OutputBufferLength* 0 の場合、呼び出し元がデータ自体ではなく、優先されるデータの範囲のサイズに対してのみを要求します。 この場合、ハンドラーに PCM 以外のデータ範囲のサイズをコピーすることで応答する必要が、 *ResultantFormatLength*パラメーターと状態を返す\_バッファー\_オーバーフローします。 Windows Driver Kit (WDK) で Msvad サンプルにはコードが含まれています、 [ **DataRangeIntersection** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiport-datarangeintersection)ハンドラーの例として使用できるルーチン。 テストする、 **DataRangeIntersection**ルーチンを使用して、 [KsStudio ユーティリティ](ksstudio-utility.md)暗証番号 (pin)--をインスタンス化する、最初にハンドラーを呼び出す、積集合、使用可能な既定の形式を決定するためにします。 PCM 以外の形式をサポートして、ドライバーする必要があります適切に処理するには、次の場所。

-   [**IMiniport::DataRangeIntersection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiport-datarangeintersection)

-   ミニポート ドライバー メソッド**Init**と**NewStream** (たとえばを参照してください[ **IMiniportWavePci::Init** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-init)と[ **IMiniportWavePci::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-newstream))。

-   ミニポート ストリーム メソッド**SetFormat** (たとえばを参照してください[ **IMiniportWavePciStream::SetFormat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepcistream-setformat))。

 

 




