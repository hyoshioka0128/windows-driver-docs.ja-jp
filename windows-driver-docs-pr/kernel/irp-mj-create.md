---
title: IRP_MJ_CREATE
description: すべてのカーネル モード ドライバーでは、DispatchCreate または DispatchCreateClose ルーチンで irp_mj_create 用の要求を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 2947f8dc-2e7d-401e-8014-6140cac6905f
keywords:
- IRP_MJ_CREATE Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 954c4a47fc9003f4aac13be33e0ba2a190ebfad4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558440"
---
# <a name="irpmjcreate"></a>IRP\_MJ\_を作成します。


すべてのカーネル モード ドライバーを処理する必要があります**IRP\_MJ\_作成**で要求を[ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)コールバック関数。

<a name="when-sent"></a>送信時
---------

オペレーティング システムの送信、 **IRP\_MJ\_作成**ファイル オブジェクトまたはデバイス オブジェクトを識別するハンドルを開く要求。 たとえば、ドライバーを呼び出すと[ **ZwCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff566424)、オペレーティング システムの送信、 **IRP\_MJ\_作成**実際の実行を要求操作を開きます。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.Create.SecurityContext**へのポインター、 [ **IO\_セキュリティ\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff550613)セキュリティを記述する構造体要求のコンテキスト。 **Parameters.Create.SecurityContext -&gt;DesiredAccess**メンバーは、呼び出し元が要求されているアクセス権を指定するアクセス マスク。

**Parameters.Create.Options**メンバーがハンドルを開くときに使用されるオプションについて説明する ULONG 値。 値に対応している上位の 8 ビット、 *CreateDisposition*パラメーターの**ZwCreateFile**、低 24 ビットの値に対応し、 *CreateOptions*パラメーターの**ZwCreateFile**します。

**Parameters.Create.ShareAccess**メンバーが共有へのアクセスの種類を記述する USHORT 値。 この値の値に対応、 *ShareAccess*パラメーターの**ZwCreateFile**します。

**Parameters.Create.FileAttributes**と**Parameters.Create.EaLength**メンバーはファイル システムで使用するために予約されている、ファイル システム フィルター ドライバー。 詳細については、次を参照してください。、 [ **IRP\_MJ\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff548630)インストール可能なファイル システム (IFS) ドキュメントのトピックです。

## <a name="output-parameters"></a>出力パラメーター


なし

<a name="operation"></a>操作
---------

ほとんどのデバイスとドライバーの中間状態を設定します\_が I/O のステータスに成功 IRP のブロックと、作成要求を完了、ドライバーを使用できます必要に応じて、 [ *DRIVER_DISPATCH* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch) 。そのハンドルの後続の I/O 要求のリソースを占有するコールバック関数。 たとえば、システム シリアル ドライバーは、ページ アウト コードをマップし、入力と出力のデバイスを開こうとした場合は、ユーザー モードのスレッドの後続の I/O 要求を処理するために必要なすべてのリソースを割り当てます。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h など)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[*DispatchCreateClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[**IO\_セキュリティ\_コンテキスト**](https://msdn.microsoft.com/library/windows/hardware/ff550613)

[**ZwCreateFile**](https://msdn.microsoft.com/library/windows/hardware/ff566424)

 

 




