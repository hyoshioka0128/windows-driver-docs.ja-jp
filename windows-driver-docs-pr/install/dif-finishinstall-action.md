---
title: DIF_FINISHINSTALL_ACTION
description: DIF_FINISHINSTALL_ACTION
ms.assetid: 76eba79b-7a8a-478e-aaea-8b36eee51846
keywords:
- DIF_FINISHINSTALL_ACTION デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DIF_FINISHINSTALL_ACTION
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 482bdcc0d44a6b63efd41e16aa5b6c80c885a75e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362572"
---
# <a name="diffinishinstallaction"></a>DIF_FINISHINSTALL_ACTION


DIF_FINISHINSTALL_ACTION 要求、インストーラーを実行する完了インストール アクション、対話型の管理者コンテキストですべての操作が完了した他のデバイスのインストールを許可します。

### <a name="when-sent"></a>送信時

Windows 8 およびそれ以降のバージョンには、デバイスのインストールの一部として自動的に実行アクションの実行を完了インストールします。 デバイスのインストールが完了操作を完了するには、は、ユーザーは必要がありますインストールの完了にアクション センターの [デバイスのソフトウェアのインストールの完了] をクリックします。

詳細については、次を参照してください。 [- インストールが完了操作を実行している](https://msdn.microsoft.com/library/windows/hardware/ff550700)します。

Windows 7、完了-インストール プロセスは、以下のいずれかの管理者の資格情報を持つユーザーのコンテキストでのみ実行します。

-   デバイスがアタッチされている間、管理者の資格情報を持つユーザーがログオンする次の時間。
-   ときに、デバイスを再接続します。
-   ユーザーがデバイス マネージャーでのハードウェア変更のスキャンを選択するとします。

ユーザーが管理者特権なし署名されている場合、Windows には、ユーザーの同意と、管理者コンテキストで、完了-インストール アクションを実行する資格情報が求められます。

### <a name="who-handles"></a>処理します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>クラスの共同インストーラー</p></td>
<td align="left"><p>処理できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>デバイスの共同インストーラー</p></td>
<td align="left"><p>処理できます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>クラスのインストーラー</p></td>
<td align="left"><p>処理できます。</p></td>
</tr>
</tbody>
</table>

 

### <a name="installer-input"></a>インストーラーの入力

<a href="" id="deviceinfoset"></a>*DeviceInfoSet*  
ハンドル、[デバイス情報設定されている](https://msdn.microsoft.com/library/windows/hardware/ff541247)インストールされているデバイスを格納しています。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
ポインター、 [ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)インストールされているデバイスを表す構造体です。

<a href="" id="device-installation-parameters-"></a>デバイスのインストール パラメーター   
デバイス インストールのパラメーターがある (、 [ **SP_DEVINSTALL_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff552346)構造) に関連付けられている*DeviceInfoData*します。

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
なし

### <a name="installer-output"></a>インストーラーの出力

<a href="" id="device-installation-parameters-"></a>デバイスのインストール パラメーター   
インストーラーは、システムの再起動が完了-インストール アクションの完了に必要な場合に、DI_NEEDREBOOT フラグを設定します。

### <a name="installer-return-value"></a>インストーラーの戻り値

インストーラーでは、次の表に記載されている値のいずれかを返します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">戻り値</th>
<th align="left">意味</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ERROR_DI_DO_DEFAULT</p></td>
<td align="left"><p>クラスのインストーラー:インストーラーは、完了インストール アクションを持たない、完了インストールの操作が正常に完了または終了インストール アクションをこれまで正常に完了できないことに決めました。 デバイスのインストールには、既定の要求の処理を実行する必要があります。</p>
<p>共同インストーラー:共同インストーラーは、このエラー コードを返すしない必要があります。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NO_ERROR</p></td>
<td align="left"><p>クラスのインストーラー:クラスのインストーラーには、このエラー コードは返しません。 クラスのインストーラーには、このエラー コードが返された場合、デバイスのインストールは、既定の要求の処理を実行しません。</p>
<p>共同インストーラー:インストーラーは、完了インストール アクションを持たない、完了インストールの操作が正常に完了または終了インストール アクションをこれまで正常に完了できないことに決めました。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Win32 エラー コード</p></td>
<td align="left"><p>クラスのインストーラーや共同インストーラー:完了インストール アクションの処理中にエラーが発生して、デバイスのインストールが完了-インストール操作を完了するには、次回デバイスが、管理者のコンテキストで列挙を試行します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="default-dif-code-handler"></a>既定の差分コード ハンドラー

Windows 7 では、 [ **SetupDiFinishInstallAction**](https://msdn.microsoft.com/library/windows/hardware/ff551022)します。

既定では、Windows 8 およびそれ以降のバージョンの差分コード ハンドラーがないと[ **SetupDiFinishInstallAction** ](https://msdn.microsoft.com/library/windows/hardware/ff551022)が削除されました。

### <a name="comments"></a>コメント

デバイスのインストールが ERROR_DI_DO_DEFAULT のリターン コードを判別することはできませんか、完了-インストール アクションが実際に成功したかどうかを NO_ERROR リターン コード、インストーラーのインストーラーが完了操作の状態をユーザーに通知する必要があります。

完了-インストール アクションの詳細については、次を参照してください。[インストール プロセスをデバイス方法-インストールが完了アクション](https://msdn.microsoft.com/library/windows/hardware/ff546216)と[完了インストール アクションの実装](https://msdn.microsoft.com/library/windows/hardware/ff546302)します。

差分コードについては、次を参照してください。 [DIF コードの処理](https://msdn.microsoft.com/library/windows/hardware/ff546094)と[既定 DIF コード ハンドラーを呼び出す](https://msdn.microsoft.com/library/windows/hardware/ff537868)します。

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
<td align="left"><p>Windows 7 から Windows Vista でサポートされています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Setupapi.h (Setupapi.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**SetupDiFinishInstallAction**](https://msdn.microsoft.com/library/windows/hardware/ff551022)

 

 






