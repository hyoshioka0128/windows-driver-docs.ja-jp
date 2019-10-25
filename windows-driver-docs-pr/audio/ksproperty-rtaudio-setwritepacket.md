---
title: KSK プロパティ\_RTAUDIO\_SETWRITEPACKET
description: KSK プロパティ\_RTAUDIO\_SETWRITEPACKET は、OS が有効なデータを Walastbuffer に書き込んだことをドライバーに通知します。
ms.assetid: 2827D6BC-B669-4AAC-967C-99B068DCC29B
keywords:
- KSPROPERTY_RTAUDIO_SETWRITEPACKET オーディオデバイス
topic_type:
- apiref
api_name:
- KSPROPERTY_RTAUDIO_SETWRITEPACKET
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 12/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: d514bf69465a7dafd97630c6286c12a3bebc85ee
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830593"
---
# <a name="ksproperty_rtaudio_setwritepacket"></a>KSK プロパティ\_RTAUDIO\_SETWRITEPACKET


KSK プロパティ\_RTAUDIO\_SETWRITEPACKET は、OS が有効なデータを Walastbuffer に書き込んだことをドライバーに通知します。

### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用状況の概要テーブル

|[購入]|設定|対象|プロパティ記述子の型|プロパティ値の型|
|--- |--- |--- |--- |--- |
|必須ではない|[はい]|Pin|[**KSPROPERTY**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))|[KSRTAUDIO_SETWRITEPACKET_INFO](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_setwritepacket_info)|


プロパティ記述子 (インスタンスデータ) は、 [**Ksk プロパティ**](https://docs.microsoft.com/previous-versions/ff564262(v=vs.85))構造体です。 クライアントは、要求を送信する前に、パケット番号、パケット長、およびその他の情報を含む値を使用して構造体を読み込みます。

プロパティ値は、 [**Ksrtaudio\_SETWRITEPACKET\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksrtaudio_setwritepacket_info)型の構造体です。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>戻り値

RTAUDIO\_SETWRITEPACKET プロパティ要求\_KSK プロパティは、正常に完了したことを示すステータス\_成功を返します。 それ以外の場合、要求は適切なエラー状態コードを返します。

<a name="remarks"></a>注釈
-------

この KSK プロパティがサポートされている場合、ドライバーは必要に応じて、提供された情報を使用してハードウェアの転送を最適化することができます。 たとえば、ドライバーは DMA 転送を最適化することができます。また、OS が別のパケットのドライバーに通知するためにこのルーチンを再度呼び出していない場合は、指定されたパケットの最後でのプログラムハードウェアの転送を停止することがあります。 これにより、たとえば、円形のバッファーを繰り返すのではなく、可聴ギャップを導入するなど、アンダーフローの可聴効果を軽減できます。 ただし、ドライバーは内部パケットカウンターを増やし、シグナル通知イベントを一定の時間内に増加させることになります。

OS で*Ksk ストリーム\_ヘッダー\_オプション sf\_endofstream*フラグが指定されている場合を除き、パケットサイズは、 [**KSK プロパティ\_RTAUDIO\_buffer に渡された notificationcount で割ったバッファーサイズになり\_\_通知を含む**](ksproperty-rtaudio-buffer-with-notification.md)。

ハードウェアの機能によっては、 *Ksk ストリーム\_ヘッダー\_オプション sf\_endofstream*フラグが指定されている場合、ドライバーは、ハードウェアがデータを転送するときに、EOS パケットの後にある wavert バッファーの一部に対して無音になることがあります。EOS 位置を超えています。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows 10 以降の Windows オペレーティングシステムで使用できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Ksmedia.h</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**KSK プロパティ\_RTAUDIO\_GETREADPACKET**](ksproperty-rtaudio-getreadpacket.md)

[UsePositionLock](usepositionlock.md)

 

 






