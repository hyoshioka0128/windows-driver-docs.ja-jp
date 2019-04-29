---
title: WIA\_DIP\_ドライバー\_バージョン
description: WIA\_DIP\_ドライバー\_バージョン プロパティには、WIA ミニドライバーの現在の DLL バージョンが含まれています。 WIA サービスは、作成し、このプロパティを保持します。
ms.assetid: 708d85b0-0daa-40d9-af38-6bf69834750b
keywords:
- WIA_DIP_DRIVER_VERSION イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DIP_DRIVER_VERSION
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a27cc2cc42768583993ce8c338e7b65834b68f4d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383690"
---
# <a name="wiadipdriverversion"></a>WIA\_DIP\_ドライバー\_バージョン


WIA\_DIP\_ドライバー\_バージョン プロパティには、WIA ミニドライバーの現在の DLL バージョンが含まれています。 WIA サービスは、作成し、このプロパティを保持します。

## <span id="ddk_wia_dip_driver_version_si"></span><span id="DDK_WIA_DIP_DRIVER_VERSION_SI"></span>


プロパティの種類:VT\_BSTR

有効な値 :WIA\_PROP\_NONE

アクセス権:読み取り専用かどうか

<a name="remarks"></a>注釈
-------

WIA ミニドライバーがバージョン リソースを指定しない場合、WIA サービスは、既定値として「0.0.0.0」の値を提供します。 アプリケーションの読み取り WIA\_DIP\_ドライバー\_WIA ミニドライバー DLL のバージョンを特定のバージョン。

**注**  以降 Windows Vista では、ワイルドカードの IP アドレス 0.0.0.0 ご利用いただけません。
また、Windows Vista で始まる場合、 **IPAutoconfigurationEnabled**レジストリ キーが値を 0 に設定、IP アドレスの自動割り当てを無効にすると、および IP アドレスが割り当てられていません。 ここで、 **ipconfig**コマンド ライン ツールでは、IP アドレスは表示されません。 キーが 0 以外の値に設定されている場合は、IP アドレスが自動的に割り当てられます。 このキーはレジストリに次のパスにすることはできます。

**HKEY\_ローカル\_マシン\\システム\\現在のコントロール セット\\サービス\\Tcpip\\パラメーター\\IPAutoconfigurationEnabled**

**HKEY\_ローカル\_マシン\\システム\\現在のコントロール セット\\サービス\\Tcpip\\パラメーター\\インターフェイス\\*GUID*\\IPAutoconfigurationEnabled**

 

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Microsoft Windows XP およびそれ以降のオペレーティング システムで使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





