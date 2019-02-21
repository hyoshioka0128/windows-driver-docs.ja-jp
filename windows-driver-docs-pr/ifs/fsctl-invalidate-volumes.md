---
title: FSCTL_INVALIDATE_VOLUMES 制御コード
description: FSCTL\_INVALIDATE\_ボリューム コントロールのコードは、検索して、指定されたファイル オブジェクトまたはハンドルによって表されるデバイスでマウントされているすべてのボリュームを削除します。
ms.assetid: 26B7EBA2-F3A9-4E5A-961C-C1857AA4FF33
keywords:
- FSCTL_INVALIDATE_VOLUMES は、ファイル システム ドライバーがインストール可能なコードを制御します。
topic_type:
- apiref
api_name:
- FSCTL_INVALIDATE_VOLUMES
api_location:
- Ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ffb8ee3a4b4ba5d60aa66d23f1e33701df0bd41
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532230"
---
# <a name="fsctlinvalidatevolumes-control-code"></a>FSCTL\_INVALIDATE\_ボリューム制御コード


**FSCTL\_INVALIDATE\_ボリューム**制御コードは、検索して、指定されたファイル オブジェクトまたはハンドルによって表されるデバイスでマウントされているすべてのボリュームを削除します。

ミニフィルター ドライバーの呼び出しは、この操作を実行する[ **FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)、およびファイル システム リダイレクターを従来のファイル システム フィルター ドライバー呼び出し[ **ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)、次のパラメーターを使用します。

**パラメーター**

<a href="" id="fileobject"></a>*FileObject*  
デバイスへのハンドルします。 デバイス ハンドルを取得する呼び出し、 [ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)関数。

<a href="" id="filehandle"></a>*FileHandle*  
デバイスへのハンドルします。 デバイス ハンドルを取得する呼び出し、 [ **CreateFile** ](https://msdn.microsoft.com/library/windows/desktop/aa363858)関数。

<a href="" id="fscontrolcode"></a>*FsControlCode*  
操作のコードを制御します。 使用**FSCTL\_INVALIDATE\_ボリューム**この操作にします。

<a href="" id="inputbuffer"></a>*InputBuffer*  
この操作では使用されません。設定**NULL**します。

<a href="" id="inputbufferlength"></a>*InputBufferLength*  
この操作では使用されません。0 に設定します。

<a href="" id="outputbuffer"></a>*OutputBuffer*  
この操作では使用されません。設定**NULL**します。

<a href="" id="outputbufferlength"></a>*OutputBufferLength*  
この操作では使用されません。0 に設定します。

<a name="status-block"></a>ステータス ブロック
------------

[**FltFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff542988)と[ **ZwFsControlFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566462)状態を返す\_操作が成功した場合の成功または適切な NTSTATUS 値。

<a name="remarks"></a>注釈
-------

FSCTL\_INVALIDATE\_ボリュームが (という名前)、ファイル システムのコントロールに送信されたデバイス オブジェクトは、ボリューム デバイス オブジェクトにありません。 コントロールのデバイス オブジェクトの詳細については、次を参照してください。[制御デバイス オブジェクトを作成する](https://msdn.microsoft.com/library/windows/hardware/ff540060)します。

FAT と NTFS ファイル システムが突然削除を処理 IRP に応答して\_MJ\_PNP IRP/\_MN\_突然\_削除します。

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

## <a name="see-also"></a>関連項目


[**FltFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff542988)

[**ZwFsControlFile**](https://msdn.microsoft.com/library/windows/hardware/ff566462)

 

 






