---
title: KSPROPERTY\_SYSAUDIO\_デバイス\_数
description: KSPROPERTY\_SYSAUDIO\_デバイス\_COUNT プロパティが、DirectSound アプリケーション プログラムがから選択する必要があります仮想のオーディオ デバイスの数を指定する数を取得します。
ms.assetid: c70b6b5e-78fc-4f03-99cf-892297e592be
keywords:
- KSPROPERTY_SYSAUDIO_DEVICE_COUNT オーディオ デバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_SYSAUDIO_DEVICE_COUNT
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 236fc2fe7e9d81780665dbcc0683c6b60adbb6f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539154"
---
# <a name="kspropertysysaudiodevicecount"></a>KSPROPERTY\_SYSAUDIO\_デバイス\_数


KSPROPERTY\_SYSAUDIO\_デバイス\_COUNT プロパティが、DirectSound アプリケーション プログラムがから選択する必要があります仮想のオーディオ デバイスの数を指定する数を取得します。

## <span id="ddk_ksproperty_sysaudio_device_count_ks"></span><span id="DDK_KSPROPERTY_SYSAUDIO_DEVICE_COUNT_KS"></span>


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
<td align="left"><p>〇</p></td>
<td align="left"><p>X</p></td>
<td align="left"><p>フィルター</p></td>
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564262" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564262)"><strong>KSPROPERTY</strong></a></p></td>
<td align="left"><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、SysAudio から選択する仮想のオーディオ デバイスの数を指定する数の書き込み先 ULONG 変数です。 SysAudio 列挙する場合*n*仮想のオーディオ デバイス、これらのデバイスでデバイス Id 0 で識別されます*n*-1。

### <a name="span-idreturnvaluespanspan-idreturnvaluespanspan-idreturnvaluespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

KSPROPERTY\_SYSAUDIO\_デバイス\_プロパティ要求の数が状態を返します\_を正常に完了したことを示すために成功します。 それ以外の場合、要求は、適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

SysAudio は、wave レンダリングを実行するシステムで有効になっているハードウェア デバイスごとに一意仮想オーディオ デバイスを列挙します。 ハードウェア デバイスの各インスタンスで仮想のオーディオ デバイスがで構成される、 [KMixer システム ドライバー](https://msdn.microsoft.com/library/windows/hardware/ff537039#kmixer-system-driver)、およびその他のオーディオのコンポーネント。 DirectSound アプリケーション プログラムは、ハードウェア デバイスが組み込まれた仮想のオーディオ デバイスを選択して、特定のハードウェア デバイスを選択します。

たとえば、3 つのオーディオ カードが、システム バスに接続されている各に WaveCyclic または WavePci ミニポート ドライバーを使用して wave レンダリング デバイスが含まれている場合は、SysAudio デバイス Id が 0、1、および 2 と 3 つの仮想オーディオ デバイスを列挙します。

SysAudio KSCATEGORY カテゴリの下のシステム レジストリ内の仮想のオーディオ デバイスのリストを保持して\_オーディオ\_デバイス。 このカテゴリは、SysAudio 専用として予約されています。 DirectSound が、システム レジストリからの仮想のオーディオ デバイスに関する情報を直接にアクセスしません。 代わりに、仮想のオーディオ デバイスのプロパティの SysAudio を照会します。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h (Ksmedia.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**KSPROPERTY**](https://msdn.microsoft.com/library/windows/hardware/ff564262)

 

 






