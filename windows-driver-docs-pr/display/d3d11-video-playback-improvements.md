---
title: Direct3D 11 のビデオ再生の機能強化
description: メインストリームアプリで Microsoft Direct3D 10 テクノロジが広く導入されているため、一部のアプリ開発者はすべてのコンテンツを同じように扱う必要があります。
ms.assetid: BB32F074-16E8-46E4-B9CF-6AEBE331B549
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4aefec16b91c6be2880a841816eefdef0d69302
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839770"
---
# <a name="direct3d-11-video-playback-improvements"></a>Direct3D 11 のビデオ再生の機能強化


メインストリームアプリで Microsoft Direct3D 10 テクノロジが広く導入されているため、一部のアプリ開発者はすべてのコンテンツを同じように扱う必要があります。 これは、すべての2-d および3-d コンテンツが Direct3D 10 または 11 Api を介して処理される場合に、Microsoft Direct3D 9 API でビデオを扱うことが困難です。 Windows 8 には Microsoft Direct3D 11 のビデオが導入されているため、アプリケーションは、1つの API を使用してすべてのグラフィカル操作を実行できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left">Windows Display Driver Model (WDDM) の最小バージョン</td>
<td align="left">1.2</td>
</tr>
<tr class="even">
<td align="left">Windows の最小バージョン</td>
<td align="left">8</td>
</tr>
<tr class="odd">
<td align="left">ドライバーの実装—完全なグラフィックスとレンダーのみ</td>
<td align="left">Microsoft Direct3D 10-、10.1-、11または11.1 対応のハードウェア (またはそれ以降) を使用するすべての WDDM 1.2 ドライバーに必須</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit">必要条件</a>とテスト</td>
<td align="left"><p><strong>デバイスグラフィックの DX11 ビデオデコードの FeatureLevel 9</strong></p>
<p><strong>DX11 のヲ、VideoProcessing</strong></p></td>
</tr>
</tbody>
</table>

 

Direct3D 11 を使用する場合の主な利点は次のとおりです。

-   Direct3D 11 video は、Microsoft メディアファンデーションと Microsoft DirectX テクノロジ間の相互運用性を容易にします。
-   複数の Api を使用するとプログラミングが困難になるため、Direct3D 11 でビデオを使用するとプログラミングエクスペリエンスが簡素化され、アプリの効率が向上します。 API では、デコードおよび処理されたビデオをより柔軟に使用できます。
-   ステレオスコピック3-d ビデオ用 Direct3D 11 API は、ステレオフレームを左および右目の画像にアンパックします。
-   これは、デコードおよびビデオ処理機能における DirectX Video セラレーション (DXVA) 2.0 および DXVA と同等の機能を備えています。
-   これは、変換のシナリオでセッション0で機能します。

## <a name="span-iddirect3d_11_video_device_driver_interfaces__ddis_spanspan-iddirect3d_11_video_device_driver_interfaces__ddis_spanspan-iddirect3d_11_video_device_driver_interfaces__ddis_spandirect3d11-video-device-driver-interfaces-ddis"></a><span id="Direct3D_11_video_device_driver_interfaces__DDIs_"></span><span id="direct3d_11_video_device_driver_interfaces__ddis_"></span><span id="DIRECT3D_11_VIDEO_DEVICE_DRIVER_INTERFACES__DDIS_"></span>Direct3D 11 ビデオデバイスドライバーインターフェイス (DDIs)


これらのデバイスドライバーインターフェイス (DDIs) は、Windows 8 用に新しく追加または更新されています。

-   [*CalcPrivateCryptoSessionSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivatecryptosessionsize)
-   [*CalcPrivateAuthenticatedChannelSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivateauthenticatedchannelsize)
-   [*CalcPrivateVideoDecoderOutputViewSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivatevideodecoderoutputviewsize)
-   [*CalcPrivateVideoDecoderSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivatevideodecodersize)
-   [*CalcPrivateVideoProcessorEnumSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivatevideoprocessorenumsize)
-   [*CalcPrivateVideoProcessorInputViewSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivatevideoprocessorinputviewsize)
-   [*CalcPrivateVideoProcessorOutputViewSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivatevideoprocessoroutputviewsize)
-   [*CalcPrivateVideoProcessorSize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_calcprivatevideoprocessorsize)
-   [*CheckFormatSupport*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_checkformatsupport)
-   [*CheckVideoDecoderFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_checkvideodecoderformat)
-   [*CheckVideoProcessorFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_checkvideoprocessorformat)
-   [*ConfigureAuthenticatedChannel (D3D11\_1)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_configureauthenticatedchannel)
-   [*Create認証 Atedchannel (D3D11\_1)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createauthenticatedchannel)
-   [*CreateCryptoSession*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createcryptosession)
-   [*CreateResource2*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource2)
-   [*CreateVideoDecoder*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createvideodecoder)
-   [*CreateVideoDecoderOutputView*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createvideodecoderoutputview)
-   [*CreateVideoProcessor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createvideoprocessor)
-   [*CreateVideoProcessorEnum*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createvideoprocessorenum)
-   [*CreateVideoProcessorInputView*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createvideoprocessorinputview)
-   [*CreateVideoProcessorOutputView*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_createvideoprocessoroutputview)
-   [*CryptoSessionGetHandle*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_cryptosessiongethandle)
-   [*DecryptionBlt (D3D11\_1)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_decryptionblt)
-   [*Destroy認証 Atedchannel*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroyauthenticatedchannel)
-   [*DestroyCryptoSession*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroycryptosession)
-   [*DestroyVideoDecoder*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroyvideodecoder)
-   [*DestroyVideoDecoderOutputView*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroyvideodecoderoutputview)
-   [*DestroyVideoProcessor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroyvideoprocessor)
-   [*DestroyVideoProcessorEnum*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroyvideoprocessorenum)
-   [*DestroyVideoProcessorInputView*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroyvideoprocessorinputview)
-   [*DestroyVideoProcessorOutputView*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_destroyvideoprocessoroutputview)
-   [*EncryptionBlt (D3D11\_1)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_encryptionblt)
-   [*Sessionkeyrefresh の終了*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_finishsessionkeyrefresh)
-   [*GetCaptureHandle*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getcapturehandle)
-   [*GetCertificate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getcertificate)
-   [*Getした Esize*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getcertificatesize)
-   [*GetContentProtectionCaps*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getcontentprotectioncaps)
-   [*GetCryptoKeyExchangeType*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getcryptokeyexchangetype)
-   [*GetEncryptionBltKey*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getencryptionbltkey)
-   [*GetVideoDecoderBufferInfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideodecoderbufferinfo)
-   [*GetVideoDecoderBufferTypeCount*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideodecoderbuffertypecount)
-   [*GetVideoDecoderConfig*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideodecoderconfig)
-   [*GetVideoDecoderConfigCount*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideodecoderconfigcount)
-   [*GetVideoDecoderProfile*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideodecoderprofile)
-   [*GetVideoDecoderProfileCount*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideodecoderprofilecount)
-   [*GetVideoProcessorCaps*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideoprocessorcaps)
-   [*GetVideoProcessorCustomRate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideoprocessorcustomrate)
-   [*GetVideoProcessorFilterRange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideoprocessorfilterrange)
-   [*GetVideoProcessorRateConversionCaps*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_getvideoprocessorrateconversioncaps)
-   [*NegotiateAuthenticatedChannelKeyExchange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_negotiateauthenticatedchannelkeyexchange)
-   [*NegotiateCryptoSessionKeyExchange*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_negotiatecryptosessionkeyeschange)
-   [*Query認証 Atedchannel (D3D11\_1)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_queryauthenticatedchannel)
-   [*RetrieveSubObject (D3D11\_1)* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_retrievesubobject)
-   [*StartSessionKeyRefresh*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_startsessionkeyrefresh)
-   [*VideoDecoderBeginFrame*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videodecoderbeginframe)
-   [*VideoDecoderEndFrame*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videodecoderendframe)
-   [*VideoDecoderExtension*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videodecoderextension)
-   [*VideoDecoderGetHandle*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videodecodergethandle)
-   [*VideoDecoderSubmitBuffers*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videodecodersubmitbuffers)
-   [*VideoProcessorBlt*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorblt)
-   [*VideoProcessorGetOutputExtension*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorgetoutputextension)
-   [*VideoProcessorGetStreamExtension*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorgetstreamextension)
-   [*VideoProcessorInputViewReadAfterWriteHazard*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorinputviewreadafterwritehazard)
-   [*VideoProcessorSetOutputAlphaFillMode*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetoutputalphafillmode)
-   [*VideoProcessorSetOutputBackgroundColor*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetoutputbackgroundcolor)
-   [*VideoProcessorSetOutputColorSpace*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetoutputcolorspace)
-   [*VideoProcessorSetOutputConstriction*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetoutputconstriction)
-   [*VideoProcessorSetOutputExtension*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetoutputextension)
-   [*VideoProcessorSetOutputStereoMode*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetoutputstereomode)
-   [*VideoProcessorSetOutputTargetRect*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetoutputtargetrect)
-   [*VideoProcessorSetStreamAlpha*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamalpha)
-   [*VideoProcessorSetStreamAutoProcessingMode*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamautoprocessingmode)
-   [*VideoProcessorSetStreamColorSpace*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamcolorspace)
-   [*VideoProcessorSetStreamDestRect*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamdestrect)
-   [*VideoProcessorSetStreamExtension*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamextension)
-   [*VideoProcessorSetStreamFilter*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamfilter)
-   [*Videoprocessorsetstreamフレーム形式*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamframeformat)
-   [*VideoProcessorSetStreamLumaKey*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamlumakey)
-   [*VideoProcessorSetStreamOutputRate*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamoutputrate)
-   [*VideoProcessorSetStreamPalette*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreampalette)
-   [*VideoProcessorSetStreamPixelAspectRatio*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreampixelaspectratio)
-   [*VideoProcessorSetStreamRotation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamrotation)
-   [*VideoProcessorSetStreamSourceRect*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamsourcerect)
-   [*VideoProcessorSetStreamStereoFormat*](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d11_1ddi_videoprocessorsetstreamstereoformat)
-   [**D3D10\_DDI\_リソース\_バインド\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10_ddi_resource_bind_flag)
-   [**D3D10\_DDI\_リソース\_その他の\_フラグ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d10_ddi_resource_misc_flag)
-   [**D3D10DDIARG\_CREATEDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d10ddiarg_createdevice)
-   [**D3D11\_1DDI\_VIDEO\_PROCESSOR\_ALPHA\_FILL\_MODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_alpha_fill_mode)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_自動\_ストリーム\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_auto_stream_caps)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_caps)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_色\_領域**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_color_space)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_コンテンツ\_DESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_content_desc)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_変換\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_conversion_caps)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_カスタム\_率**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_custom_rate)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_デバイス\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_device_caps)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_機能\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_feature_caps)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_フィルター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_filter)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_フィルター\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_filter_caps)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_フィルター\_範囲**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_filter_range)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_形式\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_format_caps)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_形式\_サポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_format_support)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_ITELECINE\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_itelecine_caps)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_出力\_率**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_output_rate)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_レート\_変換\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_rate_conversion_caps)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_ローテーション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_rotation)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_ステレオ\_キャップ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_stereo_caps)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_ステレオ\_フリップ\_モード**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_stereo_flip_mode)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_ステレオ\_形式**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_processor_stereo_format)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_ストリーム**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_video_processor_stream)
-   [**D3D11\_1DDI\_ビデオ\_の使用状況**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_1ddi_video_usage)
-   [**D3D11\_1DDI\_VIDEODEVICEFUNCS 関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddi_videodevicefuncs)
-   [**D3D11\_1DDIARG\_CREATE認証 ATEDCHANNEL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createauthenticatedchannel)
-   [**D3D11\_1DDIARG\_CREATECRYPTOSESSION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createcryptosession)
-   [**D3D11\_1DDIARG\_CREATEVIDEODECODER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createvideodecoder)
-   [**D3D11\_1DDIARG\_CREATEVIDEODECODEROUTPUTVIEW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createvideodecoderoutputview)
-   [**D3D11\_1DDIARG\_CREATEVIDEOPROCESSOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createvideoprocessor)
-   [**D3D11\_1DDIARG\_CREATEVIDEOPROCESSORENUM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createvideoprocessorenum)
-   [**D3D11\_1DDIARG\_CREATEVIDEOPROCESSORINPUTVIEW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createvideoprocessorinputview)
-   [**D3D11\_1DDIARG\_CREATEVIDEOPROCESSOROUTPUTVIEW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_createvideoprocessoroutputview)
-   [**D3D11\_1DDIARG\_署名\_エントリ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_signature_entry)
-   [**D3D11\_1DDIARG\_ステージ\_IO\_署名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_stage_io_signatures)
-   [**D3D11\_1DDIARG\_テセレーション\_IO\_署名**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_tessellation_io_signatures)
-   [**D3D11\_1DDIARG\_VIDEODECODERBEGINFRAME**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_videodecoderbeginframe)
-   [**D3D11\_1DDIARG\_VIDEODECODEREXTENSION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_1ddiarg_videodecoderextension)
-   [**D3D11\_DDI\_SHADER\_MIN\_PRECISION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_ddi_shader_min_precision)
-   [**D3D11\_DDI\_シェーダー\_最小\_精度\_データ\_サポート**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11_ddi_shader_min_precision_support_data)
-   [**D3D11\_DDI\_VIDEO\_デコーダー\_BUFFER\_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11_ddi_video_decoder_buffer_type)
-   [**D3D11DDI\_HANDLETYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ne-d3d10umddi-d3d11ddi_handletype)
-   [**D3D11DDIARG\_CREATEDEFERREDCONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createdeferredcontext)
-   [**D3D11DDIARG\_CREATERESOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d10umddi/ns-d3d10umddi-d3d11ddiarg_createresource)
-   [**D3DDDI\_RESOURCEFLAGS2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddi_resourceflags2)
-   [**D3DDDIARG\_CREATERESOURCE2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource2)
-   [**DXVAHDDDI\_ローテーション**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_dxvahdddi_rotation)
-   [**DXVAHDDDI\_STREAM\_の状態**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_dxvahdddi_stream_state)
-   [**DXVAHDDDI\_STREAM\_の状態\_ローテーション\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_stream_state_rotation_data)
-   [**DXVAHDDDI\_VPDEVCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_vpdevcaps)
-   [**FORMATOP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_formatop)

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定の要件


Direct3D 11 API のサポートは、すべての Windows 8 ハードウェアで必要です。

ハードウェアデバイスがこの機能を実装するときに満たす必要がある要件の詳細については、デバイス上の関連する[WHCK のドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)を参照してください。グラフィックスのヒントでは、**ビデオデコード機能レベル 9**と**DX11 videoprocessing**

Windows 8 で追加された機能の確認については、「 [WDDM 1.2 の機能](wddm-v1-2-features.md)」を参照してください。

 

 





