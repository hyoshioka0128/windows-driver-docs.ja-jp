---
title: KSK プロパティ\_AUDIO\_WALAST\_現在の\_\_LASTBUFFER\_POSITION の書き込み
description: KSK プロパティ\_AUDIO\_WALAST\_現在の\_書き込み\_LASTBUFFER\_POSITION プロパティは、オーディオバッファー内の最後の有効なバイトを示すために使用されます。
ms.assetid: 01EC2F29-D30A-4017-841F-8443D7C4BCF6
keywords:
- KSPROPERTY_AUDIO_WAVERT_CURRENT_WRITE_LASTBUFFER_POSITION オーディオデバイス
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
ms.openlocfilehash: 078f02f46d898dcfc12d3a1a9a1742d3a2de27e3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830927"
---
# <a name="ksproperty_audio_wavert_current_write_lastbuffer_position"></a>KSK プロパティ\_AUDIO\_WALAST\_現在の\_\_LASTBUFFER\_POSITION の書き込み


KSK プロパティ\_AUDIO\_WALAST\_現在の\_書き込み\_LASTBUFFER\_POSITION プロパティは、オーディオバッファー内の最後の有効なバイトを示すために使用されます。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

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
<th align="left">[購入]</th>
<th align="left">設定</th>
<th align="left">対象</th>
<th align="left">プロパティ記述子の型</th>
<th align="left">プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>必須ではない</p></td>
<td align="left"><p>[はい]</p></td>
<td align="left"><p>ピンのインスタンスによるノード</p></td>
<td align="left"><p>KSP_NODE</p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティ値の型は ULONG で、WaveRT オーディオバッファー内の最後の有効なバイトを表します。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSK プロパティ\_AUDIO\_WALAST\_現在の\_書き込み\_LASTBUFFER\_POSITION プロパティ要求は、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

クライアントアプリで KSK プロパティを使用している場合\_\_\_KSK プロパティを送信するときに\_BASICSUPPORT フラグを入力します。これにより、現在\_\_LASTBUFFER\_POSITION プロパティ要求をオーディオドライバーとステータスに書き込みます。\_成功が返された場合は、ドライバーが新しく追加された KSK プロパティ\_オーディオ\_WALAST\_現在\_LASTBUFFER\_POSITION プロパティを書き込むことができることを確認します。

クライアントアプリが、オフロードストリームのオーディオドライバーによってオーディオバッファーに対して最後に実行された書き込み操作を実行すると、オーディオドライバーは[**Setstreamcurrentwritepositionforlastbuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportstreamaudioenginenode2-setstreamcurrentwritepositionforlastbuffer)メソッドを呼び出します。 **Setstreamcurrentwritepositionforlastbuffer**メソッドは、ストリーム内の最後のバッファーの "書き込み位置" を示します。 この最後のバッファーは部分的にしか入力できない可能性があることに注意してください。

オーディオポートクラスドライバー (Portcls) で動作するように設計されていないオーディオドライバーを開発する場合は、この新しい KS プロパティ用に独自のプロパティハンドラーを実装する必要があります。

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

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**SetStreamCurrentWritePositionForLastBuffer**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportstreamaudioenginenode2-setstreamcurrentwritepositionforlastbuffer)

 

 






