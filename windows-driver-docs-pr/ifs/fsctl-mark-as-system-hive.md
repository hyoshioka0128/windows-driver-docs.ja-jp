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
ms.openlocfilehash: d16ea1ac491224e49086f55d49a05a42f29edc5c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560519"
---
# <a name="fsctlmarkassystemhive-control-code"></a>FSCTL\_マーク\_AS\_システム\_HIVE 制御コード


**FSCTL\_マーク\_AS\_システム\_HIVE**制御コードは、レジストリのシステム ハイブには指定したファイルが含まれているをファイル システムに通知します。 ファイル システムは、システムの hive データを適切なモーメント デッドロックを回避し、データの整合性を確保するだけでディスクにフラッシュする必要があります。 すべてのファイル、レジストリのシステム ハイブを格納しているファイル以外でこのファイル システムの制御コードを使わないでください。 この制御コードは、ディレクトリまたはボリュームのハンドルでは機能しません。 リモート コンピューター上のファイルにアクセスするファイル システム リダイレクターは、no-op としてこの制御コードを処理します。

カーネル レベルのコンポーネントだけでは、このファイル システムの制御コードを使用できます。

この操作を実行するには、呼び出す[ **FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)次のパラメーターを使用します。

**パラメーター**

<a href="" id="fileobject"></a>*FileObject*  
[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)のみです。 ユーザー ファイルのファイル オブジェクト ポインター。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="filehandle"></a>*FileHandle*  
[**ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)のみです。 ユーザー ファイルのハンドル。 このパラメーターが必要とすることはできません**NULL**します。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作の制御コード。 使用**FSCTL\_マーク\_AS\_システム\_HIVE**この操作にします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
使用されません。 値を割り当てる**NULL**このパラメーターにします。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
使用されません。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
使用されません。 値を割り当てる**NULL**このパラメーターにします。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
使用されません。

<a name="status-block"></a>ステータス ブロック
------------

[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)または[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)ステータスを返します\_操作が成功した場合は成功します。 それ以外の場合、適切な関数は、適切な NTSTATUS エラー コードを返します。

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
<td align="left">Ntifs.h (Ntifs.h を含む)</td>
</tr>
</tbody>
</table>

 

 





