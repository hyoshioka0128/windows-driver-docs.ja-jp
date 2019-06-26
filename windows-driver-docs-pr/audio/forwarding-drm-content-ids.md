---
title: DRM コンテンツ ID の転送
description: DRM コンテンツ ID の転送
ms.assetid: 62bcc44f-303a-4e72-8140-4b9bee59c252
keywords:
- デジタル権利管理の WDK オーディオ、セキュリティで保護されたデータのパス
- DRM WDK オーディオ、セキュリティで保護されたデータのパス
- コンテンツ Id WDK オーディオ
- 識別子の WDK オーディオ
- コンテンツ Id の転送
- コンテンツの解読の WDK オーディオ
- Rights Management の WDK のデジタル オーディオ、コンテンツ Id
- DRM WDK オーディオ、コンテンツ Id
- アナログ デジタルに変換します。
- DRM コンテンツ Id WDK オーディオの認証
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29e39c6c88477fe421f6e9ec0b3f35f6c8d8361c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360031"
---
# <a name="forwarding-drm-content-ids"></a>DRM コンテンツ ID の転送


## <span id="forwarding_drm_content_ids"></span><span id="FORWARDING_DRM_CONTENT_IDS"></span>


[DRMK システム ドライバー](kernel-mode-wdm-audio-components.md#drmk_system_driver)保護されたコンテンツを含む、オーディオ再生のストリームを解読します。 DRMK は、スクランブルされたデータを格納している入力ストリームを受け取り、解読、および常駐カーネル モジュールのいくつかの数から成るデータ パスに unscrambled ストリームをフィードする KS フィルターを実装します。 これらのモジュールには、KS フィルターまたはその他の種類のドライバーを指定できます。 データ パスは、通常、デジタル コンテンツをスピーカーで再生できるアナログ信号に変換するオーディオ レンダリング デバイスで終了します。

データ パスを入力する unscrambled コンテンツを許可する前に、DRMK では、データ パスがセキュリティで保護されたことを確認します。 これを行うには、DRMK は、以降では、データ パスのアップ ストリームの末尾にあるモジュールと下流にあるデータ パスの他方の end への移行に、データ パス内の各モジュールを認証します。 次の図は、このプロセスを示しています。

![セキュリティで保護されたデータのパスを示す図](images/securepath.png)

上記の図では、実線の矢印は、データ パスを表すし、破線の矢印は、データ パスが安全であることを確認するために必要な通信を表します。 DRMK のモジュールは、そのパスのすべての認証が完了した後にのみ、unscrambled データはパスを入力します。

DRMK 各モジュールが認証されると、そのモジュールは認証もされるよう、データ パスでは、次のモジュールに関する情報を含む DRMK を提供します。 各モジュールが認証されると、ストリームを識別する DRM コンテンツ ID を受け取ります。

DRMK は転送をセキュリティで保護されたデータのパスのアップ ストリームの末尾以降には、モジュール A で、モジュール B. にコンテンツの ID を順番に転送するコンテンツの IDこのプロセスは、コンテンツ ID は、Z、セキュリティで保護されたデータ パスの最後のモジュールのモジュールに転送されるまで続きます。

次の図は、データ パスに隣接するモジュールのペアを示します。

![コンテンツ id の転送を示す図](images/forwardid.png)

アップ ストリーム側でモジュールを呼び出し、次のいずれか[DRM 関数](https://docs.microsoft.com/windows-hardware/drivers/audio/drm-functions)DRMK をダウン ストリームのモジュールに関する情報を提供し、そのモジュールにコンテンツの ID を転送します。

[**DrmForwardContentToDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmforwardcontenttodeviceobject)

[**DrmForwardContentToInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmforwardcontenttointerface)

[**DrmAddContentHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmaddcontenthandlers)

これらの関数を「転送」の各 DRMK、保護されたストリームを識別する DRM コンテンツ ID および DRMK をダウン ストリームのモジュールの認証が必要な情報を提供します。 呼び出す、これら 3 つの関数のうちの選択肢は、保護されたコンテンツの転送を管理するように、互いと通信する 2 つの隣接するモジュールを使用するインターフェイスの種類によって異なります。

1.  アップ ストリームのモジュールを呼び出す場合[**保留**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocalldriver)ダウン ストリームのモジュールをダウン ストリームのモジュールとの通信、WDM ドライバーの一部であります。 この場合、アップ ストリームのモジュールを呼び出す**DrmForwardContentToDeviceObject** DRMK をダウン ストリームのモジュールを表すデバイス オブジェクトを提供します。 DRMK では、デバイス オブジェクトを使用して、ダウン ストリームのモジュールを認証します。

2.  アップ ストリームのモジュールを呼び出す場合は、2 つのモジュールは、ダウン ストリームのモジュールを実装する COM インターフェイスを介して通信、 **DrmForwardContentToInterface**します。 この呼び出しは、ダウン ストリームのモジュールの COM インターフェイスへのポインターを DRMK を提供します。 DRMK 呼び出しのみ、 **IUnknown**このインターフェイスのメソッドと、2 つのモジュール自体は、これらのメソッドの実行に同意する必要がありますが、他の方法に関する仮定行われません。 DRMK は、インターフェイス内の各メソッドのエントリ ポイントが認証済みのモジュールに属していることを確認します。 エントリ ポイントは、いくつかのモジュール間で分散は、これらのモジュールすべて DRMK を認証します。

3.  2 つのモジュールはどちらも、COM インターフェイスを使用する場合も**保留**通信するために関数では、アップ ストリーム モジュール呼び出し**DrmAddContentHandlers** DRMK を"コンテンツへのエントリ ポイントの一覧を提供するにはハンドラーに"ダウン ストリームのモジュールで実装されています。 DRMK はコンテンツのハンドラーを 、により遂行の関数に関する前提条件です。 DRMK、ただし、認証モジュール (またはモジュール) のエントリ ポイントが存在します。

認証された後は、ダウン ストリームのモジュールには、次の情報が必要です。

-   保護されたコンテンツを含むストリームを識別する DRM コンテンツ ID。 モジュールには、保護されたコンテンツを送信する予定するダウン ストリーム、さらに任意のモジュールの DRMK を通知するためにこの ID が必要です。

-   保護されたコンテンツに関連付けられている DRM コンテンツ権限。 モジュールには、適切なレベルのセキュリティを適用するためにコンテンツの権限が必要です。

次の 3 つの転送関数のそれぞれは、少し異なる方法で、モジュールには、この情報を提供します。

1.  **DrmForwardContentToDeviceObject**関数の送信、 [ **KSPROPERTY\_DRMAUDIOSTREAM\_CONTENTID** ](https://docs.microsoft.com/previous-versions/ff537351(v=vs.85))への要求のプロパティの設定ダウン ストリームのモジュールのデバイス オブジェクト。 この要求は、ストリームのコンテンツ ID およびダウン ストリームのモジュールへのコンテンツの権限を転送します。

2.  **DrmForwardContentToInterface**関数は、ダウン ストリームのモジュールの COM インターフェイスをクエリ、 [IDrmAudioStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nn-drmk-idrmaudiostream)インターフェイス。 かどうか、クエリが成功すると、関数呼び出し、 [ **IDrmAudioStream::SetContentId** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-idrmaudiostream-setcontentid)コンテンツ ID と下位モジュールにコンテンツの権限を転送するメソッド。

3.  場合、 **DrmAddContentHandlers**関数、呼び出し元 (アップ ストリームのモジュール) は、ストリームのコンテンツ ID およびコンテンツの権限をダウン ストリームのモジュールに転送します。 1 回**DrmAddContentHandlers**ダウン ストリームのモジュールが認証されている、アップ ストリームのモジュールのいずれかを呼び出すことによって、コンテンツ ID およびコンテンツの権限、ダウン ストリームのモジュールを渡すことを示す成功コードを返しますその。コンテンツのハンドラー。

上位モジュールが WaveCyclic または WavePci ミニポート ドライバーである場合は、呼び出すことができましていない適切な DRM 関数直接では、次のいずれかの。

[**IDrmPort2::ForwardContentToDeviceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idrmport2-forwardcontenttodeviceobject)

[**IDrmPort::ForwardContentToInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idrmport-forwardcontenttointerface)

[**IDrmPort2::AddContentHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-idrmport2-addcontenthandlers)

詳細については、次を参照してください。 [DRM 関数](https://docs.microsoft.com/windows-hardware/drivers/audio/drm-functions)します。

わかりやすくするため、これまでの説明には、データ パス内の各モジュールが 1 つのソースからのストリームを受け入れるし、ダウン ストリーム モジュールは 1 つには、そのストリームの転送が想定しています。 実際には、モジュールは、2 つ以上の下位モジュールにストリーム転送できますが、各ダウン ストリームのモジュール 3 の転送関数のいずれかを呼び出すことによって最初に認証する必要があります。 同様に、モジュールがまとめて複数の入力ストリームで混在できますが、適切なレベルの混在の出力ストリームの保護を提供することで、入力ストリームのコンテンツの権利を尊重にする必要があります。 詳細については、の説明を参照してください、 [ **DrmCreateContentMixed** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/drmk/nf-drmk-drmcreatecontentmixed)関数[コンテンツの Id とコンテンツの権利](content-ids-and-content-rights.md)します。

一般的なセキュリティで保護されたデータのパスを構成、 [KMixer システム ドライバー](kernel-mode-wdm-audio-components.md#kmixer_system_driver)オーディオのレンダリング デバイスを表す wave フィルターを続けています。 フィルターは、WaveCyclic または WavePci ミニポート ドライバーの組み合わせに対応するポート ドライバーとして実装されます。 データ パスがセキュリティで保護されたことを確認するには、DRMK は KMixer で、さらに、フィルターにコンテンツの ID を転送するコンテンツの ID を転送します。 汎用フィルター機能を実装するには、ポート ドライバーは、コンテンツの ID を受け取り、ミニポート ドライバーに転送します。 具体的には、ポート ドライバー呼び出し、 **DrmForwardContentToInterface**オーディオのレンダリング デバイスで wave 出力ピンを表す、ミニポート ドライバーがインスタンス化するストリーム オブジェクトへのコンテンツ ID を転送するように関数. パラメーターのいずれかの値はこの呼び出しは、ストリーム オブジェクトへのポインター [IMiniportWaveCyclicStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavecyclicstream)または[IMiniportWavePciStream](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nn-portcls-iminiportwavepcistream)インターフェイス。 関数は、このインターフェイスからのストリーム オブジェクトに照会その**IDrmAudioStream**インターフェイスし、そのインターフェイスの呼び出し、 **SetContentId**メソッド。

詳細については、の実装を参照してください、 **SetContentId** sb16 と msvad サンプル ドライバーで、Microsoft Windows Driver Kit (WDK) のメソッド。

 

 




