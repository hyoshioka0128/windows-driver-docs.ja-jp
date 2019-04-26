---
title: DIF_NEWDEVICEWIZARD_FINISHINSTALL
description: DIF_NEWDEVICEWIZARD_FINISHINSTALL
ms.assetid: 5d27316b-4e47-4e18-95fe-fd4a63a76626
keywords:
- DIF_NEWDEVICEWIZARD_FINISHINSTALL デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DIF_NEWDEVICEWIZARD_FINISHINSTALL
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f272a415e87897329478a41594780f7c6b3f7a9a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342768"
---
# <a name="difnewdevicewizardfinishinstall"></a>DIF_NEWDEVICEWIZARD_FINISHINSTALL


DIF_NEWDEVICEWIZARD_FINISHINSTALL 要求により、デバイスをインストールした後に、Windows がユーザーに表示される完了インストールのウィザード ページを指定するインストーラーが、[完了] ページに、標準に Windows が表示されます。 Windows がプラグ アンド プレイ (PnP) デバイスをインストールするとき、および管理者を使用して、この要求を送信、**ハードウェアの追加ウィザード**非 PnP デバイスをインストールします。

### <a name="when-sent"></a>送信時

Windows デバイスをインストールした後 (が正常に完了[ **DIF_INSTALLDEVICE** ](dif-installdevice.md)処理)、前に、ウィザードの [完了] ページが表示されます。

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
ハンドル、[デバイス情報設定されている](https://msdn.microsoft.com/library/windows/hardware/ff541247)デバイスを格納しています。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
ポインター、 [ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)デバイス情報のセット内のデバイスを識別する構造体。

<a href="" id="device-installation-parameters-"></a>デバイスのインストール パラメーター   
デバイス インストールのパラメーターがある ([**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)) に関連付けられている、 *DeviceInfoData*します。

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
[ **SP_NEWDEVICEWIZARD_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff553305)構造が関連付けられている、 *DeviceInfoData*します。

### <a name="installer-output"></a>インストーラーの出力

<a href="" id="device-installation-parameters"></a>デバイスのインストール パラメーター  
インストーラーでは、デバイスのインストール パラメーターでフラグを変更できます。

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
インストーラーでは、完了-インストール ウィザードのページを指定する SP_NEWDEVICEWIZARD_DATA 構造を変更できます。

### <a name="installer-return-value"></a>インストーラーの戻り値

共同インストーラーがこの差分要求を処理しない場合、共同インストーラーは、前処理のパスから NO_ERROR を返します。 共同インストーラーは、この要求を処理する場合、共同インストーラー NO_ERROR、ERROR_DI_POSTPROCESSING_REQUIRED、または Win32 エラー コードを返すことができます。

インストーラーが正常にページを提供している場合、クラスのインストーラーは NO_ERROR を返します。 それ以外の場合、クラスのインストーラーは、ERROR_DI_DO_DEFAULT または Win32 エラー コードを返します。

### <a name="default-dif-code-handler"></a>既定の差分コード ハンドラー

なし

### <a name="installer-operation"></a>インストーラーの操作

差分のコードの詳細については、次を参照してください。 [DIF コードの処理](https://msdn.microsoft.com/library/windows/hardware/ff546094)します。

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
<td align="left"><p>Microsoft Windows 2000 以降のバージョンの Windows でサポートされています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Setupapi.h (Setupapi.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**DIF_FINISHINSTALL_ACTION**](dif-finishinstall-action.md)

[**DIF_INSTALLDEVICE**](dif-installdevice.md)

[**SetupDiChangeState**](https://msdn.microsoft.com/library/windows/hardware/ff550930)

[**SP_DEVINFO_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff552344)

[**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)

[**SP_NEWDEVICEWIZARD_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff553305)

 

 






