---
title: コンテンツ ID とコンテンツの権利
description: コンテンツ ID とコンテンツの権利
ms.assetid: aee123e4-bc1b-4ba8-9f8d-a9d207297c8d
keywords:
- コンテンツ権限 WDK オーディオ
- コンテンツ Id WDK オーディオ
- デジタル Rights Management WDK オーディオ、コンテンツ Id
- DRM WDK オーディオ、コンテンツ Id
- デジタル Rights Management WDK audio、コンテンツ権限
- DRM WDK オーディオ, コンテンツ権限
- WDK オーディオの識別子
- 混合ストリーム WDK オーディオ
- DigitalOutputDisable フラグ
- CopyProtect フラグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d08bcd7e16d4187551c849dfb7af11c4fbafb26
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833630"
---
# <a name="content-ids-and-content-rights"></a>コンテンツ ID とコンテンツの権利


## <span id="content_ids_and_content_rights"></span><span id="CONTENT_IDS_AND_CONTENT_RIGHTS"></span>


コンテンツ ID (識別子) は、特定の pin にフィードするオーディオデータストリーム内の DRM で保護されたコンテンツを識別するために、 [Drmk システムドライバー](kernel-mode-wdm-audio-components.md#drmk_system_driver)によって実行時に生成される ULONG 値です。

コンテンツの権限は、DRM で保護されたコンテンツを再生およびコピーするために、コンテンツプロバイダーによってユーザーに与えられた権限をデジタルで表現したものです。 コンテンツ権限は、DRMK がオーディオドライバーに渡す[**Drmrights**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/ns-drmk-tagdrmrights)構造の形式で指定されます。

DRMRIGHTS には、 **DigitalOutputDisable**と**copyprotect**の2つのフラグが含まれています。 **DigitalOutputDisable**フラグが設定されている場合、ドライバーは、(たとえば、S/PDIF コネクタを介して) 外部デバイスに接続するすべてのデジタル出力を無効にする必要があります。 **Copyprotect**フラグが設定されている場合、ドライバーは、セキュリティで保護されたコンテンツの永続的なコピーをディスクまたは他の任意の形式の不揮発性ストレージに保存できる機能を無効にする必要があります。 たとえば、一般的なオーディオハードウェアでは、再生信号をキャプチャチャネル経由でルーティングすることができます。 この信号がデジタル形式の場合、キャプチャされた信号は、入力信号の完全なデジタルコピーである可能性があります。 再生ミックスに**Copyprotect**フラグが設定されているストリームのデータが含まれている場合、ドライバーは再生キャプチャパスをミュートする必要があります。

DRM 準拠のオーディオドライバーは、WaveCyclic および WavePci ミニポートドライバーオブジェクトの[IDrmAudioStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nn-drmk-idrmaudiostream)インターフェイスをサポートする必要があります。これにより、オーディオデータをレンダリングするためのシンクピンが公開されます。 ドライバーから**IDrmAudioStream**オブジェクトへの参照を取得するために、drmk はピンの**QueryInterface**メソッドを呼び出します。 Pin には、 [IMiniportWaveCyclicStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclicstream)または[IMiniportWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepcistream)型のインターフェイスがあります。 **IDrmAudioStream**インターフェイスは、 [**IDrmAudioStream:: SetContentId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-idrmaudiostream-setcontentid)の3つの**IUnknown**メソッドに加えて、1つのメソッドのみをサポートしています。 DRMK が**SetContentId**を呼び出すと、コンテンツ ID とコンテンツの権利が渡され、ドライバーが pin のデータストリームに関連付けられます。

WaveCyclic または WavePci のミニポートドライバーは、 [IDrmPort2](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idrmport2)インターフェイスを使用して drm 関数に直接アクセスできます (**IDrmPort2**は基本クラスの[idrmport](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idrmport)から派生します)。 Microsoft Windows XP 以降では、WaveCyclic および WavePci ポートドライバーが**IDrmPort2**をサポートしています。 ミニポートドライバーは、REFIID IID\_IDrmPort2 を使用してポートオブジェクトの**QueryInterface**メソッドを呼び出すことによって、ポートドライバーの**IDrmPort2**インターフェイスへの参照を取得します。

一部のオーディオドライバーでは、ハードウェアの混合がサポートされており、複数の入力データストリームを同時に処理できます。 この種類のドライバーは、個々のストリームのコンテンツ Id と、すべてのストリームの複合コンテンツの権限を追跡する必要があります。 ドライバーは、 [**Idrmport:: CreateContentMixed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport-createcontentmixed)を呼び出して、混合ストリームの複合権限を判別し、そのストリームを識別するためのコンテンツ ID を作成します。 ドライバーがコンテンツ ID を使用して終了した場合、コンテンツ id を削除するには、 [**Idrmport::D estroycontent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport-destroycontent)を呼び出す必要があります。

ミキサーに入力ストリームが追加または削除されるたびに、ドライバーは古いミックスのコンテンツ ID を削除し、新しいミックス用に新しいコンテンツ ID を作成する必要があります。 古いコンテンツ id を削除する前に、ドライバーは、先に古いコンテンツ id を転送したすべてのストリームに新しいコンテンツ ID を正常に転送する必要があります。 詳細については、「 [DRM コンテンツ id の転送](forwarding-drm-content-ids.md)」を参照してください。

 

 




