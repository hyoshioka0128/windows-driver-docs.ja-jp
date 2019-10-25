---
title: DRM の関数とインターフェイス
description: DRM の関数とインターフェイス
ms.assetid: 62c739da-91e8-428e-b76c-ec9621b12597
keywords:
- Digital Rights Management WDK audio、functions
- DRM WDK audio, 関数
- デジタル Rights Management WDK オーディオ、インターフェイス
- DRM WDK オーディオ、インターフェイス
- インターフェイス WDK DRM
- functions WDK DRM
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 627e3a0fd72b8a0a06608bc5600cecc7cb8a0e48
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833793"
---
# <a name="drm-functions-and-interfaces"></a>DRM の関数とインターフェイス


## <span id="drm_functions_and_interfaces"></span><span id="DRM_FUNCTIONS_AND_INTERFACES"></span>


システムドライバーのコンポーネント*Drmk. sys*と*Portcls*は、ドライバーがカーネルストリーミングオーディオコンテンツのデジタル著作権を管理するために使用する DRM 関数とインターフェイスのコレクションを実装します。 *Drmk*コンポーネントはいくつかの**drmxxx**関数を実装し、 *Portcls*は、DRM 固有の**Pcxxx**関数のセットと[idrmport](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idrmport)および[IDrmPort2](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idrmport2)インターフェイスも実装しています。

次の DRM 機能を使用できます。

[**DrmAddContentHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmaddcontenthandlers)

保護されたコンテンツを処理するための関数の一覧で構成されるドライバーインターフェイスをシステムに提供します。
[**DrmCreateContentMixed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmcreatecontentmixed)

複数の入力ストリームの混合コンテンツを含む KS オーディオストリームを識別するために DRM コンテンツ ID を作成します。
[**DrmDestroyContent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmdestroycontent)

DRM コンテンツ ID を削除します。
[**DrmForwardContentToDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmforwardcontenttodeviceobject)

は、ドライバーを認証し、保護されたコンテンツを含むストリームに割り当てられた DRM コンテンツ ID およびコンテンツ権限を送信します。
[**DrmForwardContentToFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmforwardcontenttofileobject)

廃止された関数。
[**DrmForwardContentToInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmforwardcontenttointerface)

は、ドライバーオブジェクトを認証し、保護されたコンテンツを含むストリームに割り当てられた DRM コンテンツ ID およびコンテンツ権限を送信します。
[**DrmGetContentRights**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmgetcontentrights)

システムが DRM コンテンツ ID に割り当てた DRM コンテンツの権限を取得します。
この一覧の関数は、ヘッダーファイル Drmk. h で宣言されています。 カーネルモード[drmk システムドライバー](kernel-mode-wdm-audio-components.md#drmk_system_driver)である drmk. sys は、これらの関数のエントリポイントをエクスポートします。

Windows XP 以降では、PortCls システムドライバー Portcls によって、同じ DRM 関数のセットについて異なるエントリポイントセットがエクスポートされます。 PortCls 関数の名前は、前の一覧にあるものと似ていますが、Drm ではなく、プレフィックス Pc を使用している点が異なります。

[**PcAddContentHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcaddcontenthandlers)

[**PcCreateContentMixed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pccreatecontentmixed)

[**PcDestroyContent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcdestroycontent)

[**PcForwardContentToDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcforwardcontenttodeviceobject)

[**PcForwardContentToFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcforwardcontenttofileobject)

[**PcForwardContentToInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcforwardcontenttointerface)

[**PcGetContentRights**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcgetcontentrights)

これらの関数名は、ヘッダーファイル Portcls で宣言されています。 Portcls のエントリポイントは、Drmk. sys の対応する関数を呼び出すだけではありません。 PortCls エントリポイントは便宜上、Portcls に既に接続されているオーディオドライバーが Drmk. sys を明示的に読み込む必要がないようにするためだけに提供されています。

Windows XP 以降では、同じ関数のセットが[Idrmport](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idrmport)インターフェイスおよび[IDrmPort2](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-idrmport2)インターフェイスのメソッドとして公開されています。

[**IDrmPort2::AddContentHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport2-addcontenthandlers)

[**IDrmPort:: CreateContentMixed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport-createcontentmixed)

[**IDrmPort::D estroyContent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport-destroycontent)

[**IDrmPort2::ForwardContentToDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport2-forwardcontenttodeviceobject)

[**IDrmPort:: ForwardContentToFileObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport-forwardcontenttofileobject)

[**IDrmPort:: ForwardContentToInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport-forwardcontenttointerface)

[**IDrmPort:: GetContentRights**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport-getcontentrights)

**Idrmport**インターフェイスと**IDrmPort2**インターフェイスは、ヘッダーファイル Portcls で宣言され、Portcls に実装されています。 これらのメソッドは、Drmk. sys の対応する関数を呼び出すだけではありません。 ミニポートドライバーは、*このインターフェイスのポートドライバーに対してクエリを実行することで、 *Idrmport * * x*インターフェイスへの参照を取得します。対応する Drm xxx または Pc Xxx 関数*の代わりに*Idrmport * * x*インターフェイス*を使用する利点*は、ドライバーがこのクエリを使用して、オペレーティングシステムのバージョンが Drm をサポートしているかどうかを実行時に判断できることです。 これにより、DRM をサポートする新しいバージョンの Windows と、そうでない古いバージョンの両方で実行できる1つのドライバーを作成する作業が簡単になります。 **IDrmPort2**は**idrmport**から派生し、2つの追加のメソッドを提供します。

対応するミニポートドライバーでサポートされている場合、WaveCyclic および WavePci ポートドライバーは[IDrmAudioStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nn-drmk-idrmaudiostream)インターフェイスを使用します。 ポートドライバーは、 [**IDrmAudioStream:: SetContentId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-idrmaudiostream-setcontentid)メソッドを呼び出して、drm 保護をオーディオストリームのデジタルコンテンツに割り当てます。

[**定義\_drmrights\_default**](https://docs.microsoft.com/previous-versions/ff536254(v=vs.85))マクロは、ヘッダーファイル drmk. h で定義されており、 [**drmrights**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/ns-drmk-tagdrmrights)構造体のメンバーを既定値に初期化します。

 

 




