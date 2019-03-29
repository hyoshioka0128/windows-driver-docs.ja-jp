---
title: 鍵\_AudioEndpoint\_既定\_VolumeInDb
description: Windows 10 バージョン 1605 以降で、鍵\_AudioEndpoint\_既定\_VolumeInDb プロパティ キー (dB) でソフトウェアのボリュームのノードの既定のボリュームを構成します。
ms.assetid: 9BC8E0D1-F4F3-4FB4-A50F-E4C79317EC30
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca015eef0f924bb780b7f8f2dfac97429384a688
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581770"
---
# <a name="pkeyaudioendpointdefaultvolumeindb"></a>鍵\_AudioEndpoint\_既定\_VolumeInDb


Windows 10 バージョン 1605 以降では、**鍵\_AudioEndpoint\_既定\_VolumeInDb**プロパティのキー (dB) でソフトウェアのボリュームのノードの既定のボリュームを構成します。 ドライバー開発者は、設定を既定 dB 値を指定する必要があります。

オーディオ ドライバーは、エンドポイントのハードウェア ボリューム ノードを実装していない場合、OS はそのエンドポイント上のボリュームを制御するソフトウェアのボリュームのノードを挿入します。 ボリュームの既定値が小さすぎる場合があります。 この INF キーは、適切な利益または減衰がオーディオ信号に適用されるときに、ユーザーのエクスペリエンスを向上させるを提供します。

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>注釈


Ihv と Oem は、鍵を設定して、エンドポイントの既定のソフトウェアのボリューム値を上書きできます\_AudioEndpoint\_既定\_VolumeInDb ドライバーの INF ファイルを使用してフィルターをトポロジにします。 キーによって指定された値は、dB 単位です。

このキーは、両方のレンダリングに使用して、エンドポイントをキャプチャします。

エンドポイントには、ハードウェアのボリュームのノードが実装されている場合、このキーは無視されます。

任意の値を設定することができます、OS しますが、最小および最大値の設定内では、値を確認します。 たとえば、指定した値が最大値よりも大きい場合は、OS は既定値ボリュームの最大値に設定します。

データは、16.16 固定小数点値として格納されます。 値の整数の上位 16 ビットを使用し、値の小数部の下位 16 ビットを使用します。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>サンプルの INF ファイル


```inf
; The following line overrides the default volume (in dB) for an endpoint. 
; It is only applicable when hardware volume is not implemented. 
; Decimal value expressed in fixed point 16.16 format and stored as a DWORD. 

PKEY_AudioEndpoint_Default_VolumeInDb        = "{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},9" 

; 10 dB 
HKR,EP\0,%PKEY_AudioEndpoint_Default_VolumeInDb%,0x00010001,0xA0000 

;-10 dB 
;HKR,EP\0,%PKEY_AudioEndpoint_Default_VolumeInDb%,0x00010001,0xFFF60000
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Media クラス INF の拡張機能](media-class-inf-extensions.md)

 

 






