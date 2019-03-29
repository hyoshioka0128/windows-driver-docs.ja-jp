---
title: WIA\_DPC\_アップロード\_URL
description: WIA\_DPC\_アップロード\_URL プロパティには、標準のインターネット URL がについて説明します。
ms.assetid: 5fc36640-32e3-4e51-845f-dabaecd39472
keywords:
- WIA_DPC_UPLOAD_URL イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPC_UPLOAD_URL
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64803dd2ad6fbb3e113fde4c2f852b1f7449aefd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573968"
---
# <a name="wiadpcuploadurl"></a>WIA\_DPC\_アップロード\_URL


WIA\_DPC\_アップロード\_URL プロパティには、標準のインターネット URL がについて説明します。

## <span id="ddk_wia_dpc_upload_url_si"></span><span id="DDK_WIA_DPC_UPLOAD_URL_SI"></span>


プロパティの種類:VT\_BSTR

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り/書き込み

<a name="remarks"></a>コメント
-------

WIA\_DPC\_アップロード\_URL プロパティには、イメージや、デバイスから取得した後、オブジェクトは、次のシナリオのいずれかにアップロードできる URL がについて説明します。

-   WIA アプリケーションを読み取り WIA\_DPC\_アップロード\_URL、ユーザーは、URL を自動的にイメージをアップロードします。

-   アプリケーション、URL を設定して、他のデバイス (キオスクなど) を使用して、WIA\_DPC\_アップロード\_URL。

Microsoft Windows オペレーティング システム イメージをアップロードしません。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Windows Vista 以降のオペレーティング システムで古いものであり使用できなくする必要があります。 ただし、アプリケーションやデバイス向けの Windows Server 2003、Windows XP、および Windows の以前のバージョンと互換性のこのプロパティが現在も Windows Vista で定義します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





