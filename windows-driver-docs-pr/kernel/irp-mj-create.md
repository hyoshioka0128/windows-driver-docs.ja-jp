---
title: IRP_MJ_CREATE
description: すべてのカーネルモードドライバーは、DispatchCreate または DispatchCreateClose ルーチンで IRP_MJ_CREATE 要求を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 2947f8dc-2e7d-401e-8014-6140cac6905f
keywords:
- IRP_MJ_CREATE カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 66c9f4346fd7c5fae0e8107e2e216f5c7f88015a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828125"
---
# <a name="irp_mj_create"></a>IRP\_MJ\_CREATE


すべてのカーネルモードドライバーは、 [*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)コールバック関数で要求を**作成\_IRP\_MJ**を処理する必要があります。

<a name="when-sent"></a>送信時
---------

オペレーティングシステムは、 **IRP\_MJ\_CREATE**要求を送信して、ファイルオブジェクトまたはデバイスオブジェクトへのハンドルを開きます。 たとえば、ドライバーが[**Zwcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)を呼び出すと、オペレーティングシステムは、実際に開く操作を実行するための**IRP\_MJ\_CREATE**要求を送信します。

## <a name="input-parameters"></a>入力パラメーター


**SecurityContext**メンバーは、要求のセキュリティコンテキストを記述する[**IO\_セキュリティ\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_security_context)構造を指します。 **SecurityContext-&gt;DesiredAccess**メンバーは、呼び出し元によって要求されているアクセス権を指定するアクセスマスクです。

**Parameters. Create. Options**メンバーは、ハンドルを開くときに使用されるオプションを示す ULONG 値です。 上位8ビットは**Zwcreatefile**の*CreateDisposition*パラメーターの値に対応し、下位24ビットは**Zwcreatefile**の*createoptions*パラメーターの値に対応します。

これらの**パラメーター**は、共有アクセスの種類を記述する USHORT 値です。 この値は、 **Zwcreatefile**の/の*アクセス*パラメーターの値に対応します。

**EaLength**メンバー**は、ファイル**システムおよびファイルシステムフィルタードライバーによって使用されるように予約されています。 詳細については、「インストール可能ファイルシステム (IFS)」ドキュメントの「 [**IRP\_MJ\_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create) 」を参照してください。

## <a name="output-parameters"></a>出力パラメーター


なし

<a name="operation"></a>操作
---------

ほとんどのデバイスと中間のドライバーは、IRP の i/o 状態ブロックの状態\_SUCCESS に設定し、作成要求を完了しますが、ドライバーは[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) callback 関数を使用して後続の i/o のためにリソースを予約できます。そのハンドルに対する要求。 たとえば、システムのシリアルドライバーは、ページアウトされたコードをマップし、入力と出力のためにデバイスを開こうとしているユーザーモードスレッドに対する後続の i/o 要求を処理するために必要なリソースを割り当てます。

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
<td>Wdm (Wdm .h、Ntddk、または Ntifs を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*DRIVER_DISPATCH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[*DispatchCreateClose*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[**IO\_セキュリティ\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_security_context)

[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)

 

 




