---
title: ProcAmp コントロールのためのサンプル関数
description: ProcAmp コントロールのためのサンプル関数
ms.assetid: d158216e-9a34-48a4-adca-e3c20b5e4487
keywords:
- ProcAmp の WDK DirectX va なので、サンプル関数
- WDK ProcAmp 範囲
- WDK ProcAmp プロパティ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ff345419e8acf59320e7cc4466083c967297b86
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559602"
---
# <a name="sample-functions-for-procamp-control"></a>ProcAmp コントロールのためのサンプル関数


## <span id="ddk_sample_functions_for_procamp_control_gg"></span><span id="DDK_SAMPLE_FUNCTIONS_FOR_PROCAMP_CONTROL_GG"></span>


このセクションのサンプル ProcAmp 関数は、ProcAmp コントロール機能を実装する方法を示します。 これらのサンプル関数にマップ、[補正コールバック関数のモーション](motion-compensation-callbacks.md)で定義されている、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551660)構造体。 各サンプル関数を実装し、実装の完成に動き補正コード テンプレートを使用できます。 詳細については、次を参照してください。 [DirectX VA デバイス用のコード例](example-code-for-directx-va-devices.md)します。

### <a name="span-iddeinterlacecontainerdeviceclasssamplefunctionsspanspan-iddeinterlacecontainerdeviceclasssamplefunctionsspanspan-iddeinterlacecontainerdeviceclasssamplefunctionsspandeinterlace-container-device-class-sample-functions"></a><span id="Deinterlace_Container_Device_Class_Sample_Functions"></span><span id="deinterlace_container_device_class_sample_functions"></span><span id="DEINTERLACE_CONTAINER_DEVICE_CLASS_SAMPLE_FUNCTIONS"></span>コンテナーのデバイス クラスのサンプル関数のインター レースを解除します。

次の表にサンプル ProcAmp 制御関数には、メンバー関数の*DXVA\_DeinterlaceContainerDeviceClass* (つまり、呼び出されるインター コンテナーのデバイスを使用して)。 詳細については、次を参照してください。[インター レースを解除するコンテナー デバイス クラスを定義する](defining-the-deinterlace-container-device-class.md)と[ProcAmp コントロールを実行すると操作のデインター レース](performing-procamp-control-and-deinterlacing-operations.md)します。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563949" data-raw-source="[&lt;strong&gt;ProcAmpControlQueryCaps&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563949)"><strong>ProcAmpControlQueryCaps</strong></a></p></td>
<td align="left"><p>ProcAmp コントロール デバイスの入力の要件を決定するドライバーを照会します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563950" data-raw-source="[&lt;strong&gt;ProcAmpControlQueryRange&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563950)"><strong>ProcAmpControlQueryRange</strong></a></p></td>
<td align="left"><p>最小値、最大値、ステップのサイズ、および各 ProcAmp プロパティの既定値を決定するドライバーを照会します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idprocampcontroldeviceclasssamplefunctionsspanspan-idprocampcontroldeviceclasssamplefunctionsspanspan-idprocampcontroldeviceclasssamplefunctionsspanprocamp-control-device-class-sample-functions"></a><span id="ProcAmp_Control_Device_Class_Sample_Functions"></span><span id="procamp_control_device_class_sample_functions"></span><span id="PROCAMP_CONTROL_DEVICE_CLASS_SAMPLE_FUNCTIONS"></span>ProcAmp コントロール デバイス クラスのサンプル関数

次の表にサンプル ProcAmp 制御関数には、メンバー関数の*DXVA\_ProcAmpControlDeviceClass* (つまり、呼び出される ProcAmp コントロール デバイスを使用して)。 詳細については、次を参照してください。 [ProcAmp コントロール デバイス クラスを定義する](defining-the-procamp-control-device-class.md)します。

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564026" data-raw-source="[&lt;strong&gt;ProcAmpControlOpenStream&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564026)"><strong>ProcAmpControlOpenStream</strong></a></p></td>
<td align="left"><p>ProcAmp ストリーム オブジェクトを作成します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564022" data-raw-source="[&lt;strong&gt;ProcAmpControlBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564022)"><strong>ProcAmpControlBlt</strong></a></p></td>
<td align="left"><p>宛先表面に、出力を書き込むことによって、ProcAmp 調整操作を実行します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564025" data-raw-source="[&lt;strong&gt;ProcAmpControlCloseStream&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564025)"><strong>ProcAmpControlCloseStream</strong></a></p></td>
<td align="left"><p>ProcAmp ストリーム オブジェクトを終了し、ストリームに関連付けられたハードウェア リソースを解放するデバイス ドライバーに指示します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idmappingsamplefunctionstoddmotioncompcallbacksspanspan-idmappingsamplefunctionstoddmotioncompcallbacksspanspan-idmappingsamplefunctionstoddmotioncompcallbacksspanmapping-sample-functions-to-ddmotioncompcallbacks"></a><span id="Mapping_Sample_Functions_to_DD_MOTIONCOMPCALLBACKS"></span><span id="mapping_sample_functions_to_dd_motioncompcallbacks"></span><span id="MAPPING_SAMPLE_FUNCTIONS_TO_DD_MOTIONCOMPCALLBACKS"></span>DD にサンプル関数のマップ\_MOTIONCOMPCALLBACKS

このセクションのサンプル関数は、よう動き補正のコールバック関数にマップします。 つまり、各関数のサンプルは、それぞれの動き補正コールバック内で呼び出されます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">関数</th>
<th align="left">DD_MOTIONCOMPCALLBACKS メンバー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563949" data-raw-source="[&lt;strong&gt;ProcAmpControlQueryCaps&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563949)"><strong>ProcAmpControlQueryCaps</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff563950" data-raw-source="[&lt;strong&gt;ProcAmpControlQueryRange&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff563950)"><strong>ProcAmpControlQueryRange</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564026" data-raw-source="[&lt;strong&gt;ProcAmpControlOpenStream&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564026)"><strong>ProcAmpControlOpenStream</strong></a></p></td>
<td align="left"><p><strong>CreateMoComp</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564022" data-raw-source="[&lt;strong&gt;ProcAmpControlBlt&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564022)"><strong>ProcAmpControlBlt</strong></a></p></td>
<td align="left"><p><strong>RenderMoComp</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564025" data-raw-source="[&lt;strong&gt;ProcAmpControlCloseStream&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564025)"><strong>ProcAmpControlCloseStream</strong></a></p></td>
<td align="left"><p><strong>DestroyMoComp</strong></p></td>
</tr>
</tbody>
</table>

 

 

 





