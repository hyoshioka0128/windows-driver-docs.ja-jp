---
title: DRM コンテンツ ID の転送
description: DRM コンテンツ ID の転送
ms.assetid: 62bcc44f-303a-4e72-8140-4b9bee59c252
keywords:
- デジタル Rights Management WDK オーディオ、セキュリティで保護されたデータパス
- DRM WDK オーディオ、セキュリティで保護されたデータパス
- コンテンツ Id WDK オーディオ
- WDK オーディオの識別子
- コンテンツ Id の転送
- コンテンツのスクランブル解除の WDK オーディオ
- デジタル Rights Management WDK オーディオ、コンテンツ Id
- DRM WDK オーディオ、コンテンツ Id
- デジタルからアナログへの変換
- DRM コンテンツ Id WDK オーディオを認証する
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6dab7a390a87f0071113b3075298b627f500d690
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833383"
---
# <a name="forwarding-drm-content-ids"></a>DRM コンテンツ ID の転送


## <span id="forwarding_drm_content_ids"></span><span id="FORWARDING_DRM_CONTENT_IDS"></span>


[Drmk システムドライバー](kernel-mode-wdm-audio-components.md#drmk_system_driver)は、保護されたコンテンツを含むオーディオ再生ストリームを解除します。 DRMK は、スクランブルされたデータを含む入力ストリームを取得し、それを unscrambles し、いくつかのカーネル常駐モジュールで構成されるデータパスに unscrambles ストリームをフィードする KS フィルターを実装します。 これらのモジュールは、KS フィルターや他の種類のドライバーにすることができます。 データパスは通常、オーディオレンダリングデバイスで終了します。このデバイスは、デジタルコンテンツをスピーカーで再生できるアナログ信号に変換します。

非スクランブルコンテンツにデータパスの入力を許可する前に、DRMK はデータパスがセキュリティで保護されていることを確認します。 これを行うために、DRMK はデータパスの各モジュールを認証します。これは、データパスの上流側のモジュールから始まり、データパスのもう一方の端まで下流に移動します。 このプロセスを次の図に示します。

![セキュリティで保護されたデータパスを示す図](images/securepath.png)

上の図では、実線矢印はデータパスを表し、破線の矢印はデータパスがセキュリティで保護されていることを確認するために必要な通信を表しています。 Unscrambled されたデータは、DRMK がそのパス内のすべてのモジュールの認証を完了した後にのみパスに入力されます。

DRMK が各モジュールを認証した後、そのモジュールは、データパス内の次のモジュールに関する情報を DRMK に提供して、それも認証できるようにします。 各モジュールは認証されると、ストリームを識別する DRM コンテンツ ID を受け取ります。

セキュリティで保護されたデータパスの上流側では、DRMK はコンテンツ ID をモジュール A に転送し、さらにコンテンツ ID をモジュール B に転送します。このプロセスは、コンテンツ ID が、セキュリティで保護されたデータパスの最後のモジュールであるモジュール Z に転送されるまで続行されます。

次の図は、データパス内の隣接するモジュールのペアを示しています。

![コンテンツ id の転送を示す図](images/forwardid.png)

上流側のモジュールは、次の[DRM 関数](https://docs.microsoft.com/windows-hardware/drivers/audio/drm-functions)のいずれかを呼び出し、drmk にダウンストリームモジュールに関する情報を提供し、コンテンツ ID をそのモジュールに転送します。

[**DrmForwardContentToDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmforwardcontenttodeviceobject)

[**DrmForwardContentToInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmforwardcontenttointerface)

[**DrmAddContentHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmaddcontenthandlers)

これらの "転送" 関数はそれぞれ、保護されたストリームを識別する DRM コンテンツ ID と、DRMK が下流モジュールを認証するために必要な情報を提供します。 これら3つの関数のどちらを呼び出すかは、保護されたコンテンツの転送を管理する2つの隣接するモジュールが相互に通信するために使用するインターフェイスの種類によって異なります。

1.  上流モジュールが下流モジュールと通信するために[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)を呼び出す場合、ダウンストリームモジュールは WDM ドライバーの一部です。 この場合、上流モジュールは**DrmForwardContentToDeviceObject**を呼び出して、ダウンストリームモジュールを表すデバイスオブジェクトを drmk に提供します。 DRMK は、デバイスオブジェクトを使用して下流モジュールを認証します。

2.  2つのモジュールが、ダウンストリームモジュールが実装する COM インターフェイスを介して通信する場合、上流モジュールは**Drmforwardcontenttointerface**を呼び出します。 この呼び出しは、ダウンストリームモジュールの COM インターフェイスへのポインターを持つ DRMK を提供します。 DRMK は、このインターフェイスの**IUnknown**メソッドのみを呼び出し、他のメソッドについては想定しません。ただし、2つのモジュール自体は、これらのメソッドの動作に同意する必要があります。 DRMK は、インターフェイスの各メソッドのエントリポイントが、認証されたモジュールに属していることを確認します。 エントリポイントが複数のモジュールに分散されている場合、DRMK はこれらのすべてのモジュールを認証します。

3.  2つのモジュールが COM インターフェイスも**IoCallDriver**関数も使用して通信する場合、上流モジュールは**DrmAddContentHandlers**を呼び出して、drmk に "コンテンツハンドラー" のエントリポイントのリストを提供します。これは、ダウンストリームモジュール。 DRMK は、コンテンツハンドラーを呼び出さず、実行する関数についての仮定を行いません。 ただし、DRMK は、エントリポイントが存在するモジュール (またはモジュール) を認証します。

ダウンストリームモジュールは、認証された後、次の情報を必要とします。

-   保護されたコンテンツを含むストリームを識別する DRM コンテンツ ID。 モジュールは、保護されたコンテンツの送信を予定している任意のモジュール (さらに下流) の DRMK に通知するためにこの ID を必要とします。

-   保護されたコンテンツに関連付けられている DRM コンテンツの権限。 このモジュールでは、適切なレベルのセキュリティを適用するためにコンテンツ権限が必要です。

これら3つの転送関数は、この情報をモジュールにわずかに異なる方法で提供します。

1.  **DrmForwardContentToDeviceObject**関数は、 [**DRMAUDIOSTREAM\_CONTENTID 要求\_ksk プロパティ**](https://docs.microsoft.com/previous-versions/ff537351(v=vs.85))を下流のモジュールの device オブジェクトに送信します。 この要求は、ストリームのコンテンツ ID とコンテンツの権限を下流のモジュールに転送します。

2.  **Drmforwardcontenttointerface**関数は、 [IDrmAudioStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nn-drmk-idrmaudiostream)インターフェイスの下流モジュールの COM インターフェイスに対してクエリを行います。 クエリが成功した場合、関数は[**IDrmAudioStream:: SetContentId**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-idrmaudiostream-setcontentid)メソッドを呼び出して、コンテンツ ID とコンテンツの権限を下流のモジュールに転送します。

3.  **DrmAddContentHandlers**関数の場合、呼び出し元 (上流モジュール) はストリームのコンテンツ ID とコンテンツ権限を下流のモジュールに転送します。 ダウンストリームモジュールが認証されたことを示す成功コードで**DrmAddContentHandlers**が返されると、上流モジュールは、コンテンツハンドラーのいずれかを呼び出すことによって、コンテンツ ID とコンテンツの権限を下流のモジュールに渡します。

アップストリームモジュールが WaveCyclic または WavePci ミニポートドライバーの場合、次のいずれかの方法で間接的に適切な DRM 関数を呼び出すことができます。

[**IDrmPort2::ForwardContentToDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport2-forwardcontenttodeviceobject)

[**IDrmPort:: ForwardContentToInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport-forwardcontenttointerface)

[**IDrmPort2::AddContentHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport2-addcontenthandlers)

詳細については、「 [DRM Functions](https://docs.microsoft.com/windows-hardware/drivers/audio/drm-functions)」を参照してください。

わかりやすくするために、前述の説明では、データパス内の各モジュールが1つのソースからのストリームを受け入れ、そのストリームを最大1つの下流モジュールに転送することを前提としています。 実際、モジュールは2つ以上の下流モジュールにストリームを転送できますが、3つの転送関数のいずれかを呼び出すことによって、最初に各ダウンストリームモジュールを認証する必要があります。 同様に、モジュールは複数の入力ストリームを混在させることができますが、混合出力ストリームに適切なレベルの保護を提供することによって、入力ストリームのコンテンツ権限を尊重する必要があります。 詳細については、「[コンテンツ id とコンテンツ権限](content-ids-and-content-rights.md)」の[**DrmCreateContentMixed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/drmk/nf-drmk-drmcreatecontentmixed)関数の説明を参照してください。

一般的なセキュリティで保護されたデータパスは、 [KMixer システムドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver)の後にオーディオレンダリングデバイスを表す wave フィルターで構成されます。 フィルターは、対応するポートドライバーと組み合わせて、WaveCyclic または WavePci ミニポートドライバーとして実装されます。 データパスがセキュリティで保護されていることを確認するために、DRMK はコンテンツ ID を KMixer に転送し、さらにコンテンツ ID をフィルターに転送します。 汎用フィルター機能を実装するポートドライバーは、コンテンツ ID を受け取り、それをミニポートドライバーに転送します。 具体的には、ポートドライバーは、 **Drmforwardcontenttointerface**関数を呼び出して、ミニポートドライバーがインスタンス化したストリームオブジェクトにコンテンツ ID を転送し、オーディオレンダリングデバイスの wave 出力ピンを表します。 この呼び出しのパラメーター値の1つは、ストリームオブジェクトの[IMiniportWaveCyclicStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclicstream)インターフェイスまたは[IMiniportWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepcistream)インターフェイスへのポインターです。 このインターフェイスを使用して、関数は、 **IDrmAudioStream**インターフェイスのストリームオブジェクトに対してクエリを実行し、そのインターフェイスの**SetContentId**メソッドを呼び出します。

詳細については、Microsoft Windows Driver Kit (WDK) の sb16 および msvad サンプルドライバーの**SetContentId**メソッドの実装を参照してください。

 

 




