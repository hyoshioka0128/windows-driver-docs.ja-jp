---
title: PCM 以外のピン ファクトリの要件
description: PCM 以外のピン ファクトリの要件
ms.assetid: 3ba5da2e-f96f-4645-8a37-dd985287a9f2
keywords:
- PCM 以外のオーディオ形式 WDK、pin ファクトリ
- ファクトリ WDK オーディオをピン留めする
- データ交差ハンドラー WDK オーディオ、PCM 以外の wave 形式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 00a7953817a2fe3809abc8fc898bf27a1c95de6c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830197"
---
# <a name="requirements-for-a-non-pcm-pin-factory"></a>PCM 以外のピン ファクトリの要件


## <span id="requirements_for_a_non_pcm_pin_factory"></span><span id="REQUIREMENTS_FOR_A_NON_PCM_PIN_FACTORY"></span>


Windows XP 以降、および Microsoft Windows Me では、PCM 以外の[**WAVEFORMATEX**](https://docs.microsoft.com/windows/desktop/api/mmreg/ns-mmreg-twaveformatex)形式を再生するドライバーは、次のガイドラインに従って pcm 以外の pin を公開する必要があります。

最初に、pcm ピン工場とは別の PCM データ形式以外の pin ファクトリを定義します。 唯一のピンのインスタンスが自動的に KMixer に割り当てられるため、PCM と非 PCM で同じ単一インスタンスのピンファクトリを共有することはできません。 ピンファクトリが複数のインスタンスをサポートしている場合は、PCM と PCM 以外は同じ pin ファクトリに共存できます。 ただし、この場合は、これらの pin インスタンスを実行時に PCM クライアントが使用できないことを保証することはできません。 PCM クライアントが既に割り当てている可能性があります。 最も安全なオプションは、PCM 以外の形式に個別の pin ファクトリを提供することです。

DirectSound 8 で pin が検出されて使用されるようにするには、PCM を既にサポートしているフィルターにこの PCM 以外の pin ファクトリを定義します。 それ以外の場合、DirectSound は PCM 以外の pin を検出しません。 これは、PCM をサポートしていないデバイスが PCM 形式ではサポートできないことも意味します。

2つ目の方法として、PCM 以外の pin に[データの交差ハンドラー](proprietary-data-intersection-handlers.md)を実装します。 PortCls には組み込みハンドラーが用意されていますが、この既定のハンドラーは常に PCM を選択するので、PCM 以外の形式に独自のハンドラーを追加する必要があります。 PCM 以外の pin の交差ハンドラーでは、WAVE\_形式\_PCM をサポートしないようにする必要があります。 このハンドラーは*Outputbufferlength* 0 で呼び出すことができます。この場合、呼び出し元は、データ自体ではなく、優先データ範囲のサイズのみを要求します。 この場合、ハンドラーは、PCM データ範囲のサイズを*resultの*形式の値パラメーターにコピーして、ステータス\_バッファー\_オーバーフローを返すことで応答する必要があります。 Windows Driver Kit (WDK) の Msvad サンプルには、ハンドラーの例として使用できる[**Datarangeintersection 集合**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-datarangeintersection)ルーチンのコードが含まれています。 **Datarangeintersection 部分**ルーチンをテストするには、 [ksk studio ユーティリティ](ksstudio-utility.md)を使用して pin をインスタンス化します。最初に、使用可能な既定の形式を決定するために、共通部分ハンドラーを呼び出します。 PCM 以外の形式をサポートするには、ドライバーが次の場所で適切に処理する必要があります。

-   [**IMiniport::D ataRangeIntersection 部分**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-datarangeintersection)

-   ミニポートドライバーのメソッド**init**と**newstream** (たとえば、「 [**IMiniportWavePci:: Init**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-init) 」と「 [**IMiniportWavePci:: newstream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-newstream)」を参照してください)。

-   ミニポート-ストリームメソッドの**setformat** (例[ **: IMiniportWavePciStream:: setformat**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepcistream-setformat)を参照)。

 

 




