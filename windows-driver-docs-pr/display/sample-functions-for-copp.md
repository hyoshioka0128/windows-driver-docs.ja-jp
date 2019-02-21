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
ms.openlocfilehash: 362261cffbe55b6d591c10dffc2c0059c7268d40
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550605"
---
# <a name="sample-functions-for-copp"></a>COPP のサンプル関数


## <span id="ddk_sample_functions_for_copp_gg"></span><span id="DDK_SAMPLE_FUNCTIONS_FOR_COPP_GG"></span>


**このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。**

サンプルの COPP 関数は、COPP 処理機能を実装する方法を示します。 これらのサンプル関数にマップ、[補正コールバック関数のモーション](motion-compensation-callbacks.md)で定義されている、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551660)構造体。 各関数のサンプルと、対応する COPP I/O 制御 (IOCTL) 要求を実装し、実装の完成に動き補正コード テンプレートとビデオのミニポート ドライバー テンプレートを使用できます。 詳細については、次を参照してください。 [DirectX VA デバイス用のコード例](example-code-for-directx-va-devices.md)します。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff539650" data-raw-source="[&lt;em&gt;COPPOpenVideoSession&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539650)"><em>COPPOpenVideoSession</em></a></p></td>
<td align="left"><p>現在のビデオ セッションに使用される COPP デバイスを初期化します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff539644" data-raw-source="[&lt;em&gt;COPPGetCertificateLength&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539644)"><em>COPPGetCertificateLength</em></a></p></td>
<td align="left"><p>グラフィックス ハードウェアで使用される証明書のバイト単位のサイズを取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff539646" data-raw-source="[&lt;em&gt;COPPKeyExchange&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539646)"><em>COPPKeyExchange</em></a></p></td>
<td align="left"><p>グラフィックス ハードウェアで使用されるデジタル証明書を取得します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540421" data-raw-source="[&lt;em&gt;COPPSequenceStart&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540421)"><em>COPPSequenceStart</em></a></p></td>
<td align="left"><p>現在のビデオ セッションを保護モードに設定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff539642" data-raw-source="[&lt;em&gt;COPPCommand&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539642)"><em>COPPCommand</em></a></p></td>
<td align="left"><p>COPP デバイスに関連付けられた物理コネクタには、保護レベルを設定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff539652" data-raw-source="[&lt;em&gt;COPPQueryStatus&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539652)"><em>COPPQueryStatus</em></a></p></td>
<td align="left"><p>COPP デバイスに関連付けられている保護されたビデオ セッションの状態を取得します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff539638" data-raw-source="[&lt;em&gt;COPPCloseVideoSession&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539638)"><em>COPPCloseVideoSession</em></a></p></td>
<td align="left"><p>COPP デバイス オブジェクトを終了し、COPP デバイスに関連付けられたハードウェア リソースを解放するドライバーに指示します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idmappingsamplefunctionstoddmotioncompcallbacksspanspan-idmappingsamplefunctionstoddmotioncompcallbacksspanspan-idmappingsamplefunctionstoddmotioncompcallbacksspanmapping-sample-functions-to-ddmotioncompcallbacks"></a><span id="Mapping_Sample_Functions_to_DD_MOTIONCOMPCALLBACKS"></span><span id="mapping_sample_functions_to_dd_motioncompcallbacks"></span><span id="MAPPING_SAMPLE_FUNCTIONS_TO_DD_MOTIONCOMPCALLBACKS"></span>DD にサンプル関数のマップ\_MOTIONCOMPCALLBACKS

COPP IOCTL を使用して次のように、モーション補正のコールバック関数にマップするこのセクションのサンプル関数各関数のサンプルが、それぞれの COPP IOCTL 内と呼ばれに渡される各 COPP IOCTL、 [ **EngDeviceIoControl** ](https://msdn.microsoft.com/library/windows/hardware/ff564838)それぞれの動き補正コールバック内で関数関数。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff539650" data-raw-source="[&lt;em&gt;COPPOpenVideoSession&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539650)"><em>COPPOpenVideoSession</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567768" data-raw-source="[&lt;strong&gt;IOCTL_COPP_OpenDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567768)"><strong>IOCTL_COPP_OpenDevice</strong></a></p></td>
<td align="left"><p><strong>CreateMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff539644" data-raw-source="[&lt;em&gt;COPPGetCertificateLength&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539644)"><em>COPPGetCertificateLength</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567765" data-raw-source="[&lt;strong&gt;IOCTL_COPP_GetCertificateLength&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567765)"><strong>IOCTL_COPP_GetCertificateLength</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff539646" data-raw-source="[&lt;em&gt;COPPKeyExchange&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539646)"><em>COPPKeyExchange</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567766" data-raw-source="[&lt;strong&gt;IOCTL_COPP_KeyExchange&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567766)"><strong>IOCTL_COPP_KeyExchange</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff540421" data-raw-source="[&lt;em&gt;COPPSequenceStart&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff540421)"><em>COPPSequenceStart</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567781" data-raw-source="[&lt;strong&gt;IOCTL_COPP_StartSequence&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567781)"><strong>IOCTL_COPP_StartSequence</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff539642" data-raw-source="[&lt;em&gt;COPPCommand&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539642)"><em>COPPCommand</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567762" data-raw-source="[&lt;strong&gt;IOCTL_COPP_Command&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567762)"><strong>IOCTL_COPP_Command</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff539652" data-raw-source="[&lt;em&gt;COPPQueryStatus&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539652)"><em>COPPQueryStatus</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567783" data-raw-source="[&lt;strong&gt;IOCTL_COPP_Status&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567783)"><strong>IOCTL_COPP_Status</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff539638" data-raw-source="[&lt;em&gt;COPPCloseVideoSession&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539638)"><em>COPPCloseVideoSession</em></a></p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff567759" data-raw-source="[&lt;strong&gt;IOCTL_COPP_CloseDevice&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567759)"><strong>IOCTL_COPP_CloseDevice</strong></a></p></td>
<td align="left"><p><strong>DestroyMoComp</strong></p></td>
</tr>
</tbody>
</table>

 

 

 





