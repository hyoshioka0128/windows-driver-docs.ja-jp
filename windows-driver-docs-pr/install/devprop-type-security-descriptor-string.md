---
title: DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING
description: Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING 識別子はデータ型がセキュリティ記述子を含む NULL で終わる Unicode 文字列であることを示す基本データ型識別子を表します、。セキュリティ記述子定義言語 (SDDL) 形式です。
ms.assetid: 2d791816-bb0e-4275-953f-1492886e9545
keywords:
- DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING
api_location:
- Devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: df63ac424df81aff23a53206fd340b702858bf02
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528481"
---
# <a name="devproptypesecuritydescriptorstring"></a>DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING


Windows Vista および Windows の以降のバージョンでは、DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING 識別子はデータ型がセキュリティ記述子を含む NULL で終わる Unicode 文字列であることを示す基本データ型識別子を表します、。セキュリティ記述子定義言語 (SDDL) 形式です。

<a name="remarks"></a>注釈
-------

DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING は、のみと組み合わせることができます、 [ **DEVPROP_TYPEMOD_LIST** ](devprop-typemod-list.md)プロパティ データ型の修飾子。

### <a name="setting-a-property-of-this-type"></a>このプロパティの種類の設定

基本データ型は DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING プロパティを設定する呼び出し、対応する**SetupDiSet * Xxx*** プロパティ関数と set 関数は、次のようにパラメーターを入力します。

-   設定、 *PropertyType* DEVPROP_TYPE_SECURITY_DESCRIPTOR_STRING、パラメーターの設定、 *PropertyBuffer*パラメーターを NULL で終わるセキュリティ記述子文字列を含むバッファーへのポインター、し、設定、 *PropertyBufferSize*パラメーターを NULL ターミネータを含めた、セキュリティ記述子文字列のバイト単位のサイズ。

-   プロパティを設定する、必要に応じて、他の関数の入力パラメーターを設定します。

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
<td align="left">Devpropdef.h (Devpropdef.h を含む)</td>
</tr>
</tbody>
</table>

 

 





