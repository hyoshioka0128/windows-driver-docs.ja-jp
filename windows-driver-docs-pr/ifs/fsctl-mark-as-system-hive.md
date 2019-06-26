---
title: FSCTL_MARK_AS_SYSTEM_HIVE 制御コード
description: FSCTL\_マーク\_AS\_システム\_HIVE 制御コードは、レジストリのシステム ハイブには指定したファイルが含まれているをファイル システムに通知します。
ms.assetid: de3cb340-2485-4bc5-bc2a-3c34cee2d6b3
keywords:
- FSCTL_MARK_AS_SYSTEM_HIVE 制御コード インストール可能なファイル システム ドライバー
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
ms.openlocfilehash: d826674ac0fdee5ffebb1ce7da70f72cb0e42061
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380130"
---
# <a name="fsctlmarkassystemhive-control-code"></a>FSCTL\_マーク\_AS\_システム\_HIVE 制御コード


**FSCTL\_マーク\_AS\_システム\_HIVE**制御コードは、レジストリのシステム ハイブには指定したファイルが含まれているをファイル システムに通知します。 ファイル システムは、システムの hive データを適切なモーメント デッドロックを回避し、データの整合性を確保するだけでディスクにフラッシュする必要があります。 すべてのファイル、レジストリのシステム ハイブを格納しているファイル以外でこのファイル システムの制御コードを使わないでください。 この制御コードは、ディレクトリまたはボリュームのハンドルでは機能しません。 リモート コンピューター上のファイルにアクセスするファイル システム リダイレクターは、no-op としてこの制御コードを処理します。

カーネル レベルのコンポーネントだけでは、このファイル システムの制御コードを使用できます。

この操作を実行するには、呼び出す[ **FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

**Parameters**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)のみです。 ユーザー ファイルのファイル オブジェクト ポインター。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 ユーザー ファイルのハンドル。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 使用**FSCTL\_マーク\_AS\_システム\_HIVE**この操作にします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
使用されていません。 値を割り当てる**NULL**このパラメーターにします。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
使用されていません。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
使用されていません。 値を割り当てる**NULL**このパラメーターにします。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
使用されていません。

<a name="status-block"></a>ステータス ブロック
------------

[**FltFsControlFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fltkernel/nf-fltkernel-fltfscontrolfile)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)ステータスを返します\_操作が成功した場合は成功します。 それ以外の場合、適切な関数は、適切な NTSTATUS エラー コードを返します。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Header</p></td>
<td align="left">Ntifs.h (Ntifs.h を含む)</td>
</tr>
</tbody>
</table>

 

 





