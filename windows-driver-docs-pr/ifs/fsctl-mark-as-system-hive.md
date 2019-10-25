---
title: FSCTL_MARK_AS_SYSTEM_HIVE 制御コード
description: FSCTL\_マーク\_\_システム\_HIVE コントロールコードとしてマークすると、指定したファイルにレジストリのシステムハイブが含まれていることがファイルシステムに通知されます。
ms.assetid: de3cb340-2485-4bc5-bc2a-3c34cee2d6b3
keywords:
- FSCTL_MARK_AS_SYSTEM_HIVE 制御コードのインストール可能なファイルシステムドライバー
topic_type:
- apiref
api_name:
- FSCTL_MARK_AS_SYSTEM_HIVE
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee10cec4463f52afd6cf0dbb4c50f32b86242882
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841286"
---
# <a name="fsctl_mark_as_system_hive-control-code"></a>FSCTL\_\_\_システム\_HIVE 制御コードとしてマークする


**FSCTL\_マーク\_\_システム\_HIVE コントロールコードとしてマークすると**、指定したファイルにレジストリのシステムハイブが含まれていることがファイルシステムに通知されます。 ファイルシステムは、デッドロックを回避し、データの整合性を確保するために、すぐにシステム hive データをディスクにフラッシュする必要があります。 このファイルシステム制御コードは、レジストリのシステムハイブを含むファイル以外のファイルでは使用しないでください。 この制御コードは、ディレクトリまたはボリュームハンドルでは機能しません。 リモートコンピューター上のファイルにアクセスするファイルシステムのリダイレクターは、この制御コードを操作なしとして扱います。

カーネルレベルのコンポーネントのみが、このファイルシステム制御コードを使用できます。

この操作を実行するには、次のパラメーターを使用して[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)を呼び出します。

**Parameters**

<a href="" id="fileobject"></a>*ファ*  
[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)のみ。 ユーザーファイルのファイルオブジェクトポインター。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="filehandle"></a>*FileHandle*  
[**Zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみ。 ユーザーファイルのハンドル。 このパラメーターは必須であり、 **NULL**にすることはできません。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 この操作には、 **FSCTL\_使用して\_を\_システム\_HIVE としてマークして**ください。

<a href="" id="inputbuffer"></a>*InputBuffer*  
使用しません。 このパラメーターに**NULL**値を割り当てます。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
使用しません。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
使用しません。 このパラメーターに**NULL**値を割り当てます。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
使用しません。

<a name="status-block"></a>ステータス ブロック
------------

[**Fltfscontrolfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)または[**zwfscontrolfile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)は、操作が成功した場合に STATUS\_SUCCESS を返します。 それ以外の場合、適切な関数は、適切な NTSTATUS エラーコードを返します。

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
<td align="left">Ntifs (Ntifs を含む)</td>
</tr>
</tbody>
</table>

 

 





