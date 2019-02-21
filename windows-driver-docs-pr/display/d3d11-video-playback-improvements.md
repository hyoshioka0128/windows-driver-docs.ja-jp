---
title: Direct3d11 のビデオ再生の機能強化
description: メイン ストリームのアプリケーションで direct3d10 Microsoft テクノロジの広く普及で、一部のアプリ開発者は、同じすべてのコンテンツを処理するとします。
ms.assetid: BB32F074-16E8-46E4-B9CF-6AEBE331B549
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03c48a09e9d84ccf56214c00e21c2466ac89b8c4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537939"
---
# <a name="direct3d-11-video-playback-improvements"></a>Direct3d11 のビデオ再生の機能強化


メイン ストリームのアプリケーションで direct3d10 Microsoft テクノロジの広く普及で、一部のアプリ開発者は、同じすべてのコンテンツを処理するとします。 これは、機能は、Direct3D 10 または 11 Api を介して、2-d および 3-D コンテンツのすべての処理時に Microsoft direct3d9 API でのビデオの扱いに困難です。 Windows 8 には、Microsoft direct3d11 でビデオが導入されています、ために、アプリケーションは、すべてのグラフィカルな操作を実行するのに 1 つの API を使用できます。

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
<td align="left">ドライバーの実装: 完全なグラフィックスとレンダリングのみ</td>
<td align="left">すべての WDDM 1.2 ドライバーと Microsoft Direct3D 10 で、必須 10.1、11、または 11.1 対応ハードウェア (またはそれ以降)</td>
</tr>
<tr class="even">
<td align="left"><a href="https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit">WHCK</a>要件とテスト</td>
<td align="left"><p><strong>Device.Graphics... DX11 ビデオのデコード FeatureLevel 9</strong></p>
<p><strong>Device.Graphics... DX11 VideoProcessing</strong></p></td>
</tr>
</tbody>
</table>

 

Direct3d11 を使用する主な利点を次に示します。

-   Direct3d11 のビデオでは、Microsoft Media Foundation および Microsoft DirectX テクノロジ間の相互運用が簡略化します。
-   複数の Api を使用して、プログラムに難しくなります direct3d11 でビデオを使用してプログラミング エクスペリエンスを簡素化とアプリより効率的です。 API より柔軟に処理し、デコードされたビデオを使用して提供します。
-   ステレオスコ ピック 3-D ビデオ、direct3d11 API は、イメージの左と右の目に、ステレオのフレームをアンパックします。
-   デコードおよびビデオの処理機能での DirectX ビデオ アクセラレータ (DXVA) 2.0 と DXVA HD パリティがあります。
-   トランス コード シナリオのセッション 0 で動作します。

## <a name="span-iddirect3d11videodevicedriverinterfacesddisspanspan-iddirect3d11videodevicedriverinterfacesddisspanspan-iddirect3d11videodevicedriverinterfacesddisspandirect3d11-video-device-driver-interfaces-ddis"></a><span id="Direct3D_11_video_device_driver_interfaces__DDIs_"></span><span id="direct3d_11_video_device_driver_interfaces__ddis_"></span><span id="DIRECT3D_11_VIDEO_DEVICE_DRIVER_INTERFACES__DDIS_"></span>Direct3d11 のビデオ デバイス ドライバー インターフェイス (Ddi)


これらのデバイス ドライバー インターフェイス (Ddi) は、新しい Windows 8 向けに更新されました。

-   [*CalcPrivateCryptoSessionSize*](https://msdn.microsoft.com/library/windows/hardware/hh451606)
-   [*CalcPrivateAuthenticatedChannelSize*](https://msdn.microsoft.com/library/windows/hardware/hh451604)
-   [*CalcPrivateVideoDecoderOutputViewSize*](https://msdn.microsoft.com/library/windows/hardware/hh451608)
-   [*CalcPrivateVideoDecoderSize*](https://msdn.microsoft.com/library/windows/hardware/hh451610)
-   [*CalcPrivateVideoProcessorEnumSize*](https://msdn.microsoft.com/library/windows/hardware/hh451611)
-   [*CalcPrivateVideoProcessorInputViewSize*](https://msdn.microsoft.com/library/windows/hardware/hh451612)
-   [*CalcPrivateVideoProcessorOutputViewSize*](https://msdn.microsoft.com/library/windows/hardware/hh451613)
-   [*CalcPrivateVideoProcessorSize*](https://msdn.microsoft.com/library/windows/hardware/hh451614)
-   [*CheckFormatSupport*](https://msdn.microsoft.com/library/windows/hardware/ff539390)
-   [*CheckVideoDecoderFormat*](https://msdn.microsoft.com/library/windows/hardware/hh451615)
-   [*CheckVideoProcessorFormat*](https://msdn.microsoft.com/library/windows/hardware/hh451616)
-   [*ConfigureAuthenticatedChannel(D3D11\_1)*](https://msdn.microsoft.com/library/windows/hardware/hh451617)
-   [*CreateAuthenticatedChannel(D3D11\_1)*](https://msdn.microsoft.com/library/windows/hardware/hh451618)
-   [*CreateCryptoSession*](https://msdn.microsoft.com/library/windows/hardware/hh451619)
-   [*CreateResource2*](https://msdn.microsoft.com/library/windows/hardware/hh406287)
-   [*CreateVideoDecoder*](https://msdn.microsoft.com/library/windows/hardware/hh451620)
-   [*CreateVideoDecoderOutputView*](https://msdn.microsoft.com/library/windows/hardware/hh451621)
-   [*CreateVideoProcessor*](https://msdn.microsoft.com/library/windows/hardware/hh451622)
-   [*CreateVideoProcessorEnum*](https://msdn.microsoft.com/library/windows/hardware/hh451623)
-   [*CreateVideoProcessorInputView*](https://msdn.microsoft.com/library/windows/hardware/hh451624)
-   [*CreateVideoProcessorOutputView*](https://msdn.microsoft.com/library/windows/hardware/hh451625)
-   [*CryptoSessionGetHandle*](https://msdn.microsoft.com/library/windows/hardware/hh451626)
-   [*DecryptionBlt(D3D11\_1)*](https://msdn.microsoft.com/library/windows/hardware/hh451628)
-   [*DestroyAuthenticatedChannel*](https://msdn.microsoft.com/library/windows/hardware/hh451630)
-   [*DestroyCryptoSession*](https://msdn.microsoft.com/library/windows/hardware/hh451632)
-   [*DestroyVideoDecoder*](https://msdn.microsoft.com/library/windows/hardware/hh451634)
-   [*DestroyVideoDecoderOutputView*](https://msdn.microsoft.com/library/windows/hardware/hh451636)
-   [*DestroyVideoProcessor*](https://msdn.microsoft.com/library/windows/hardware/hh451638)
-   [*DestroyVideoProcessorEnum*](https://msdn.microsoft.com/library/windows/hardware/hh451639)
-   [*DestroyVideoProcessorInputView*](https://msdn.microsoft.com/library/windows/hardware/hh451642)
-   [*DestroyVideoProcessorOutputView*](https://msdn.microsoft.com/library/windows/hardware/hh451644)
-   [*EncryptionBlt(D3D11\_1)*](https://msdn.microsoft.com/library/windows/hardware/hh451646)
-   [*FinishSessionKeyRefresh*](https://msdn.microsoft.com/library/windows/hardware/hh451648)
-   [*GetCaptureHandle*](https://msdn.microsoft.com/library/windows/hardware/hh451650)
-   [*GetCertificate*](https://msdn.microsoft.com/library/windows/hardware/hh451652)
-   [*GetCertificateSize*](https://msdn.microsoft.com/library/windows/hardware/hh451654)
-   [*GetContentProtectionCaps*](https://msdn.microsoft.com/library/windows/hardware/hh451656)
-   [*GetCryptoKeyExchangeType*](https://msdn.microsoft.com/library/windows/hardware/hh451658)
-   [*GetEncryptionBltKey*](https://msdn.microsoft.com/library/windows/hardware/hh451660)
-   [*GetVideoDecoderBufferInfo*](https://msdn.microsoft.com/library/windows/hardware/hh451661)
-   [*GetVideoDecoderBufferTypeCount*](https://msdn.microsoft.com/library/windows/hardware/hh451663)
-   [*GetVideoDecoderConfig*](https://msdn.microsoft.com/library/windows/hardware/hh451665)
-   [*GetVideoDecoderConfigCount*](https://msdn.microsoft.com/library/windows/hardware/hh451668)
-   [*GetVideoDecoderProfile*](https://msdn.microsoft.com/library/windows/hardware/hh451670)
-   [*GetVideoDecoderProfileCount*](https://msdn.microsoft.com/library/windows/hardware/hh451672)
-   [*GetVideoProcessorCaps*](https://msdn.microsoft.com/library/windows/hardware/hh451674)
-   [*GetVideoProcessorCustomRate*](https://msdn.microsoft.com/library/windows/hardware/hh451676)
-   [*GetVideoProcessorFilterRange*](https://msdn.microsoft.com/library/windows/hardware/hh451689)
-   [*GetVideoProcessorRateConversionCaps*](https://msdn.microsoft.com/library/windows/hardware/hh451690)
-   [*NegotiateAuthenticatedChannelKeyExchange*](https://msdn.microsoft.com/library/windows/hardware/hh451691)
-   [*NegotiateCryptoSessionKeyExchange*](https://msdn.microsoft.com/library/windows/hardware/hh451692)
-   [*QueryAuthenticatedChannel(D3D11\_1)*](https://msdn.microsoft.com/library/windows/hardware/hh451694)
-   [*RetrieveSubObject(D3D11\_1)*](https://msdn.microsoft.com/library/windows/hardware/hh439849)
-   [*StartSessionKeyRefresh*](https://msdn.microsoft.com/library/windows/hardware/hh451696)
-   [*VideoDecoderBeginFrame*](https://msdn.microsoft.com/library/windows/hardware/hh451697)
-   [*VideoDecoderEndFrame*](https://msdn.microsoft.com/library/windows/hardware/hh451698)
-   [*VideoDecoderExtension*](https://msdn.microsoft.com/library/windows/hardware/hh451699)
-   [*VideoDecoderGetHandle*](https://msdn.microsoft.com/library/windows/hardware/hh451700)
-   [*VideoDecoderSubmitBuffers*](https://msdn.microsoft.com/library/windows/hardware/hh451701)
-   [*VideoProcessorBlt*](https://msdn.microsoft.com/library/windows/hardware/hh451703)
-   [*VideoProcessorGetOutputExtension*](https://msdn.microsoft.com/library/windows/hardware/hh451705)
-   [*VideoProcessorGetStreamExtension*](https://msdn.microsoft.com/library/windows/hardware/hh439773)
-   [*VideoProcessorInputViewReadAfterWriteHazard*](https://msdn.microsoft.com/library/windows/hardware/hh439775)
-   [*VideoProcessorSetOutputAlphaFillMode*](https://msdn.microsoft.com/library/windows/hardware/hh439778)
-   [*VideoProcessorSetOutputBackgroundColor*](https://msdn.microsoft.com/library/windows/hardware/dn459003)
-   [*VideoProcessorSetOutputColorSpace*](https://msdn.microsoft.com/library/windows/hardware/hh439782)
-   [*VideoProcessorSetOutputConstriction*](https://msdn.microsoft.com/library/windows/hardware/hh439784)
-   [*VideoProcessorSetOutputExtension*](https://msdn.microsoft.com/library/windows/hardware/hh439786)
-   [*VideoProcessorSetOutputStereoMode*](https://msdn.microsoft.com/library/windows/hardware/hh439788)
-   [*VideoProcessorSetOutputTargetRect*](https://msdn.microsoft.com/library/windows/hardware/hh439790)
-   [*VideoProcessorSetStreamAlpha*](https://msdn.microsoft.com/library/windows/hardware/hh439792)
-   [*VideoProcessorSetStreamAutoProcessingMode*](https://msdn.microsoft.com/library/windows/hardware/hh439794)
-   [*VideoProcessorSetStreamColorSpace*](https://msdn.microsoft.com/library/windows/hardware/hh439796)
-   [*VideoProcessorSetStreamDestRect*](https://msdn.microsoft.com/library/windows/hardware/dn459004)
-   [*VideoProcessorSetStreamExtension*](https://msdn.microsoft.com/library/windows/hardware/hh439800)
-   [*VideoProcessorSetStreamFilter*](https://msdn.microsoft.com/library/windows/hardware/hh439802)
-   [*VideoProcessorSetStreamFrameFormat*](https://msdn.microsoft.com/library/windows/hardware/hh439804)
-   [*VideoProcessorSetStreamLumaKey*](https://msdn.microsoft.com/library/windows/hardware/hh439805)
-   [*VideoProcessorSetStreamOutputRate*](https://msdn.microsoft.com/library/windows/hardware/hh439807)
-   [*VideoProcessorSetStreamPalette*](https://msdn.microsoft.com/library/windows/hardware/hh439809)
-   [*VideoProcessorSetStreamPixelAspectRatio*](https://msdn.microsoft.com/library/windows/hardware/hh439811)
-   [*VideoProcessorSetStreamRotation*](https://msdn.microsoft.com/library/windows/hardware/hh439813)
-   [*VideoProcessorSetStreamSourceRect*](https://msdn.microsoft.com/library/windows/hardware/hh439815)
-   [*VideoProcessorSetStreamStereoFormat*](https://msdn.microsoft.com/library/windows/hardware/hh439817)
-   [**D3D10\_DDI\_RESOURCE\_BIND\_FLAG**](https://msdn.microsoft.com/library/windows/hardware/ff541995)
-   [**D3D10\_DDI\_RESOURCE\_MISC\_FLAG**](https://msdn.microsoft.com/library/windows/hardware/ff542004)
-   [**D3D10DDIARG\_CREATEDEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff541664)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_アルファ\_入力\_モード**](https://msdn.microsoft.com/library/windows/hardware/hh450963)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_自動\_ストリーム\_キャップ**](https://msdn.microsoft.com/library/windows/hardware/hh450966)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_キャップ**](https://msdn.microsoft.com/library/windows/hardware/hh450968)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_色\_領域**](https://msdn.microsoft.com/library/windows/hardware/hh450970)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_コンテンツ\_DESC**](https://msdn.microsoft.com/library/windows/hardware/hh450972)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_変換\_キャップ**](https://msdn.microsoft.com/library/windows/hardware/hh450975)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_カスタム\_率**](https://msdn.microsoft.com/library/windows/hardware/hh450977)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_デバイス\_キャップ**](https://msdn.microsoft.com/library/windows/hardware/hh450978)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_機能\_キャップ**](https://msdn.microsoft.com/library/windows/hardware/hh450980)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_フィルター**](https://msdn.microsoft.com/library/windows/hardware/hh450982)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_フィルター\_キャップ**](https://msdn.microsoft.com/library/windows/hardware/hh450983)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_フィルター\_範囲**](https://msdn.microsoft.com/library/windows/hardware/hh450985)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_形式\_キャップ**](https://msdn.microsoft.com/library/windows/hardware/hh450986)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_形式\_サポート**](https://msdn.microsoft.com/library/windows/hardware/hh450987)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_ITELECINE\_キャップ**](https://msdn.microsoft.com/library/windows/hardware/hh450988)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_出力\_率**](https://msdn.microsoft.com/library/windows/hardware/hh450989)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_レート\_変換\_キャップ**](https://msdn.microsoft.com/library/windows/hardware/hh450990)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_回転**](https://msdn.microsoft.com/library/windows/hardware/hh451019)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_ステレオ\_キャップ**](https://msdn.microsoft.com/library/windows/hardware/hh451023)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_ステレオ\_反転\_モード**](https://msdn.microsoft.com/library/windows/hardware/hh451025)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_ステレオ\_形式**](https://msdn.microsoft.com/library/windows/hardware/hh451029)
-   [**D3D11\_1DDI\_ビデオ\_プロセッサ\_ストリーム**](https://msdn.microsoft.com/library/windows/hardware/hh451033)
-   [**D3D11\_1DDI\_ビデオ\_使用状況**](https://msdn.microsoft.com/library/windows/hardware/hh451037)
-   [**D3D11\_1DDI\_VIDEODEVICEFUNCS**](https://msdn.microsoft.com/library/windows/hardware/hh406452)
-   [**D3D11\_1DDIARG\_CREATEAUTHENTICATEDCHANNEL**](https://msdn.microsoft.com/library/windows/hardware/hh406306)
-   [**D3D11\_1DDIARG\_CREATECRYPTOSESSION**](https://msdn.microsoft.com/library/windows/hardware/hh406308)
-   [**D3D11\_1DDIARG\_CREATEVIDEODECODER**](https://msdn.microsoft.com/library/windows/hardware/hh406310)
-   [**D3D11\_1DDIARG\_CREATEVIDEODECODEROUTPUTVIEW**](https://msdn.microsoft.com/library/windows/hardware/hh406312)
-   [**D3D11\_1DDIARG\_CREATEVIDEOPROCESSOR**](https://msdn.microsoft.com/library/windows/hardware/hh406314)
-   [**D3D11\_1DDIARG\_CREATEVIDEOPROCESSORENUM**](https://msdn.microsoft.com/library/windows/hardware/hh406316)
-   [**D3D11\_1DDIARG\_CREATEVIDEOPROCESSORINPUTVIEW**](https://msdn.microsoft.com/library/windows/hardware/hh406318)
-   [**D3D11\_1DDIARG\_CREATEVIDEOPROCESSOROUTPUTVIEW**](https://msdn.microsoft.com/library/windows/hardware/hh406320)
-   [**D3D11\_1DDIARG\_署名\_エントリ**](https://msdn.microsoft.com/library/windows/hardware/hh406322)
-   [**D3D11\_1DDIARG\_ステージ\_IO\_署名**](https://msdn.microsoft.com/library/windows/hardware/hh406324)
-   [**D3D11\_1DDIARG\_テセレーション\_IO\_署名**](https://msdn.microsoft.com/library/windows/hardware/hh406326)
-   [**D3D11\_1DDIARG\_VIDEODECODERBEGINFRAME**](https://msdn.microsoft.com/library/windows/hardware/hh406328)
-   [**D3D11\_1DDIARG\_VIDEODECODEREXTENSION**](https://msdn.microsoft.com/library/windows/hardware/hh406330)
-   [**D3D11\_DDI\_シェーダー\_MIN\_有効桁数**](https://msdn.microsoft.com/library/windows/hardware/hh451059)
-   [**D3D11\_DDI\_シェーダー\_MIN\_精度\_サポート\_データ**](https://msdn.microsoft.com/library/windows/hardware/hh451062)
-   [**D3D11\_DDI\_ビデオ\_デコーダー\_バッファー\_型**](https://msdn.microsoft.com/library/windows/hardware/hh451066)
-   [**D3D11DDI\_HANDLETYPE**](https://msdn.microsoft.com/library/windows/hardware/ff542152)
-   [**D3D11DDIARG\_CREATEDEFERREDCONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff542044)
-   [**D3D11DDIARG\_CREATERESOURCE**](https://msdn.microsoft.com/library/windows/hardware/ff542062)
-   [**D3DDDI\_RESOURCEFLAGS2**](https://msdn.microsoft.com/library/windows/hardware/hh439286)
-   [**D3DDDIARG\_CREATERESOURCE2**](https://msdn.microsoft.com/library/windows/hardware/hh451074)
-   [**DXVAHDDDI\_ROTATION**](https://msdn.microsoft.com/library/windows/hardware/hh464119)
-   [**DXVAHDDDI\_STREAM\_STATE**](https://msdn.microsoft.com/library/windows/hardware/ff563068)
-   [**DXVAHDDDI\_STREAM\_STATE\_ROTATION\_DATA**](https://msdn.microsoft.com/library/windows/hardware/hh464120)
-   [**DXVAHDDDI\_VPDEVCAPS**](https://msdn.microsoft.com/library/windows/hardware/ff563113)
-   [**FORMATOP**](https://msdn.microsoft.com/library/windows/hardware/ff566438)

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>ハードウェア認定要件


すべての Windows 8 ハードウェアで direct3d11 API のサポートが必要です。

この機能を実装するときにハードウェア デバイスが満たす必要のある要件については、関連するを参照してください[WHCK ドキュメント](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)で**Device.Graphics... DX11 ビデオのデコード FeatureLevel 9**と**Device.Graphics... DX11 VideoProcessing**します。

参照してください[WDDM 1.2 機能](wddm-v1-2-features.md)に Windows 8 で追加された機能の説明。

 

 





