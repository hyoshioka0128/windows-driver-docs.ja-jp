---
title: COPP のサンプル関数
description: COPP のサンプル関数
ms.assetid: 73c9cf1c-c20d-456c-8029-5316fd8979d5
keywords:
- 保護 WDK COPP、サンプル関数をコピーします。
- ビデオのコピー防止 WDK COPP、サンプル関数
- COPP WDK DirectX va なので、サンプル関数
- ビデオの WDK COPP サンプル関数を保護
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2b1d92c1c18c7adb0c7742c8d6e540f7971136e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365617"
---
# <a name="sample-functions-for-copp"></a>COPP のサンプル関数


## <span id="ddk_sample_functions_for_copp_gg"></span><span id="DDK_SAMPLE_FUNCTIONS_FOR_COPP_GG"></span>


**このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。**

サンプルの COPP 関数は、COPP 処理機能を実装する方法を示します。 これらのサンプル関数にマップ、[補正コールバック関数のモーション](motion-compensation-callbacks.md)で定義されている、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造体。 各関数のサンプルと、対応する COPP I/O 制御 (IOCTL) 要求を実装し、実装の完成に動き補正コード テンプレートとビデオのミニポート ドライバー テンプレートを使用できます。 詳細については、次を参照してください。 [DirectX VA デバイス用のコード例](example-code-for-directx-va-devices.md)します。

### <a name="span-idcoppsamplefunctionsspanspan-idcoppsamplefunctionsspanspan-idcoppsamplefunctionsspancopp-sample-functions"></a><span id="COPP_Sample_Functions"></span><span id="copp_sample_functions"></span><span id="COPP_SAMPLE_FUNCTIONS"></span>COPP サンプル関数

次の表にサンプル COPP 関数は、COPP デバイスを使用して呼び出されます。 COPP デバイスの詳細については、次を参照してください。 [COPP デバイス定義のテンプレート コード](copp-device-definition-template-code.md)と[COPP デバイス クラスを定義する](defining-the-copp-device-class.md)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">メンバー関数</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppopenvideosession" data-raw-source="[&lt;em&gt;COPPOpenVideoSession&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppopenvideosession)"><em>COPPOpenVideoSession</em></a></p></td>
<td align="left"><p>現在のビデオ セッションに使用される COPP デバイスを初期化します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppgetcertificatelength" data-raw-source="[&lt;em&gt;COPPGetCertificateLength&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppgetcertificatelength)"><em>COPPGetCertificateLength</em></a></p></td>
<td align="left"><p>グラフィックス ハードウェアで使用される証明書のバイト単位のサイズを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppkeyexchange" data-raw-source="[&lt;em&gt;COPPKeyExchange&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppkeyexchange)"><em>COPPKeyExchange</em></a></p></td>
<td align="left"><p>グラフィックス ハードウェアで使用されるデジタル証明書を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppsequencestart" data-raw-source="[&lt;em&gt;COPPSequenceStart&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppsequencestart)"><em>COPPSequenceStart</em></a></p></td>
<td align="left"><p>現在のビデオ セッションを保護モードに設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand" data-raw-source="[&lt;em&gt;COPPCommand&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)"><em>COPPCommand</em></a></p></td>
<td align="left"><p>COPP デバイスに関連付けられた物理コネクタには、保護レベルを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus" data-raw-source="[&lt;em&gt;COPPQueryStatus&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)"><em>COPPQueryStatus</em></a></p></td>
<td align="left"><p>COPP デバイスに関連付けられている保護されたビデオ セッションの状態を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppclosevideosession" data-raw-source="[&lt;em&gt;COPPCloseVideoSession&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppclosevideosession)"><em>COPPCloseVideoSession</em></a></p></td>
<td align="left"><p>COPP デバイス オブジェクトを終了し、COPP デバイスに関連付けられたハードウェア リソースを解放するドライバーに指示します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idmappingsamplefunctionstoddmotioncompcallbacksspanspan-idmappingsamplefunctionstoddmotioncompcallbacksspanspan-idmappingsamplefunctionstoddmotioncompcallbacksspanmapping-sample-functions-to-ddmotioncompcallbacks"></a><span id="Mapping_Sample_Functions_to_DD_MOTIONCOMPCALLBACKS"></span><span id="mapping_sample_functions_to_dd_motioncompcallbacks"></span><span id="MAPPING_SAMPLE_FUNCTIONS_TO_DD_MOTIONCOMPCALLBACKS"></span>DD にサンプル関数のマップ\_MOTIONCOMPCALLBACKS

COPP IOCTL を使用して次のように、モーション補正のコールバック関数にマップするこのセクションのサンプル関数各関数のサンプルが、それぞれの COPP IOCTL 内と呼ばれに渡される各 COPP IOCTL、 [ **EngDeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeviceiocontrol)それぞれの動き補正コールバック内で関数関数。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">IOCTL</th>
<th align="left">DD_MOTIONCOMPCALLBACKS メンバー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppopenvideosession" data-raw-source="[&lt;em&gt;COPPOpenVideoSession&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppopenvideosession)"><em>COPPOpenVideoSession</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/" data-raw-source="[&lt;strong&gt;IOCTL_COPP_OpenDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/)"><strong>IOCTL_COPP_OpenDevice</strong></a></p></td>
<td align="left"><p><strong>CreateMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppgetcertificatelength" data-raw-source="[&lt;em&gt;COPPGetCertificateLength&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppgetcertificatelength)"><em>COPPGetCertificateLength</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-getcertificatelength" data-raw-source="[&lt;strong&gt;IOCTL_COPP_GetCertificateLength&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-getcertificatelength)"><strong>IOCTL_COPP_GetCertificateLength</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppkeyexchange" data-raw-source="[&lt;em&gt;COPPKeyExchange&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppkeyexchange)"><em>COPPKeyExchange</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-keyexchange" data-raw-source="[&lt;strong&gt;IOCTL_COPP_KeyExchange&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-keyexchange)"><strong>IOCTL_COPP_KeyExchange</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppsequencestart" data-raw-source="[&lt;em&gt;COPPSequenceStart&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppsequencestart)"><em>COPPSequenceStart</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-startsequence" data-raw-source="[&lt;strong&gt;IOCTL_COPP_StartSequence&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-startsequence)"><strong>IOCTL_COPP_StartSequence</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand" data-raw-source="[&lt;em&gt;COPPCommand&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)"><em>COPPCommand</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-command" data-raw-source="[&lt;strong&gt;IOCTL_COPP_Command&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-command)"><strong>IOCTL_COPP_Command</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus" data-raw-source="[&lt;em&gt;COPPQueryStatus&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)"><em>COPPQueryStatus</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-status" data-raw-source="[&lt;strong&gt;IOCTL_COPP_Status&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/ioctl-copp-status)"><strong>IOCTL_COPP_Status</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/coppclosevideosession" data-raw-source="[&lt;em&gt;COPPCloseVideoSession&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/coppclosevideosession)"><em>COPPCloseVideoSession</em></a></p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/display/" data-raw-source="[&lt;strong&gt;IOCTL_COPP_CloseDevice&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/display/)"><strong>IOCTL_COPP_CloseDevice</strong></a></p></td>
<td align="left"><p><strong>DestroyMoComp</strong></p></td>
</tr>
</tbody>
</table>

 

 

 





