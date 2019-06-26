---
title: KSPROPERTY\_オーディオ\_WAVERT\_現在\_書き込み\_LASTBUFFER\_位置
description: KSPROPERTY\_オーディオ\_WAVERT\_現在\_書き込み\_LASTBUFFER\_位置プロパティは、オーディオのバッファー内の最後の有効なバイトを示すために使用します。
ms.assetid: 01EC2F29-D30A-4017-841F-8443D7C4BCF6
keywords:
- KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_LASTBUFFER_POSITION オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_LASTBUFFER_POSITION
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2dcd5e64408dc015b12e7d5f7f4076689b0757f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358876"
---
# <a name="kspropertyaudiowavertcurrentwritelastbufferposition"></a>KSPROPERTY\_オーディオ\_WAVERT\_現在\_書き込み\_LASTBUFFER\_位置


KSPROPERTY\_オーディオ\_WAVERT\_現在\_書き込み\_LASTBUFFER\_位置プロパティは、オーディオのバッファー内の最後の有効なバイトを示すために使用します。

### <a name="span-idusagesummarytablespanspan-idusagesummarytablespanspan-idusagesummarytablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">取得</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>X</p></td>
<td align="left"><p>〇</p></td>
<td align="left"><p>暗証番号 (pin) のインスタンスを使用してノード</p></td>
<td align="left"><p>KSP_NODE</p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値は ULONG 型であり、WaveRT の音声バッファー内の最後の有効なバイトを表します。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_オーディオ\_WAVERT\_現在\_書き込み\_LASTBUFFER\_位置プロパティ要求がステータスを返します\_が完了したことを示す成功正常にします。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

クライアント アプリが、KSPROPERTY を使用している場合\_型\_、KSPROPERTY を送信するときに、BASICSUPPORT フラグ\_オーディオ\_WAVERT\_現在\_書き込み\_LASTBUFFER\_オーディオ ドライバーとステータスに位置プロパティ要求\_成功が返され、ドライバーが新しく追加された KSPROPERTY をサポートすることが確認されます\_オーディオ\_WAVERT\_現在\_書き込み\_LASTBUFFER\_POSITION プロパティ。

オーディオ ドライバーを呼び出すクライアント アプリでは、オフロードされたストリームのオーディオ ドライバーによって処理されるオーディオのバッファーに非常に最後の書き込み操作を実行するときに、 [ **SetStreamCurrentWritePositionForLastBuffer** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportstreamaudioenginenode2-setstreamcurrentwritepositionforlastbuffer)メソッド。 **SetStreamCurrentWritePositionForLastBuffer**メソッドは、"書き込み"の最後のバッファー ストリーム内の位置を示します。 この最後のバッファーを部分的にのみ満たさことに注意してください。

オーディオ ポート クラス ドライバー (Portcls) で動作するようになっていないオーディオ ドライバーを開発するかどうかは、このプロパティのハンドラーを実装する必要がある新しい KS プロパティ。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>サポートされている最小のクライアント</p></td>
<td align="left"><p>Windows 8.1</p></td>
</tr>
<tr class="even">
<td align="left"><p>サポートされている最小のサーバー</p></td>
<td align="left"><p>Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**SetStreamCurrentWritePositionForLastBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportstreamaudioenginenode2-setstreamcurrentwritepositionforlastbuffer)

 

 






