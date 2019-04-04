---
title: DIF_TROUBLESHOOTER
description: DIF_TROUBLESHOOTER
ms.assetid: e8477d4d-cc81-48aa-9d51-9f37c3cce0cb
keywords:
- DIF_TROUBLESHOOTER デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DIF_TROUBLESHOOTER
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a8e26cffb01fc59273548eaf3f455b4b0e8fd368
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579338"
---
# <a name="diftroubleshooter"></a>DIF_TROUBLESHOOTER


DIF_TROUBLESHOOTER 要求は、インストーラーまたはを返す CHM ファイルと HTM トラブルシューティング ファイルを起動する Windows のデバイスのトラブルシューティングを開始できます。

**注**  この差分コードは、Windows Server 2003、Windows XP、および Microsoft Windows 2000 でのみサポートされます。

 

### <a name="when-sent"></a>送信時

ユーザーがデバイス マネージャーでデバイスの「トラブルシューティング」ボタンをクリックするとします。

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
識別するハンドルを提供、[デバイス情報設定されている](https://msdn.microsoft.com/library/windows/hardware/ff541247)デバイスを格納しています。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
ポインターを提供する[ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)デバイス情報のセット内のデバイスを識別する構造体。

<a href="" id="device-installation-parameters-"></a>デバイスのインストール パラメーター   
デバイス インストールのパラメーターがある ([**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)) に関連付けられている、 *DeviceInfoData*します。

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
[ **SP_TROUBLESHOOTER_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff553341)構造が関連付けられている、 *DeviceInfoData*します。

### <a name="installer-output"></a>インストーラーの出力

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
インストーラーによって変更、 [ **SP_TROUBLESHOOTER_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff553341)、CHM または HTML ファイルを設定します。

### <a name="installer-return-value"></a>インストーラーの戻り値

共同インストーラーがこの要求を処理しない場合は、前処理のパスから NO_ERROR を返します。

共同インストーラーは、この要求を処理する場合の処理後のパスでは。 共同インストーラー CHM および HTML ファイルを提供している場合は、(おそらく ERROR_DI_DO_DEFAULT) を受信した状態を伝達します。 共同インストーラーは、トラブルシューティングを実行すると、問題を修正、共同インストーラーは NO_ERROR を返します。 共同インストーラーがトラブルシューティングを実行し、問題が解決しない場合は、(ERROR_DI_DO_DEFAULT) を受信した状態が反映されます。

クラスのインストーラーは、CHM ファイルと HTML ファイルでは、提供、またはクラスのインストーラーは、トラブルシューティング ツールを実行しますが、問題が解決しない、クラスのインストーラーは ERROR_DI_DO_DEFAULT を返します。 Windows は、その後、既定のハンドラーを呼び出します。

クラスのインストーラーは、独自のトラブルシューティング ツールを起動して、問題を修正する場合、クラスのインストーラーは NO_ERROR を返します。 その後、Windows では、既定のハンドラーを呼び出すはされません。

クラスのインストーラーには、エラーが発生すると、インストーラーは、適切な Win32 エラー コードを返します。 その後、Windows では、既定のハンドラーを呼び出すはされません。

### <a name="default-dif-code-handler"></a>既定の差分コード ハンドラー

なし

DIF_TROUBLESHOOTER の既定のハンドラーはありませんが、オペレーティング システム インストーラーが指定したトラブルシューティング ツールがない場合、デバイスの問題を解決しようとする既定のトラブルシューティング ツールを提供します。

### <a name="installer-operation"></a>インストーラーの操作

インストーラーを呼び出す[ **CM_Get_DevNode_Status** ](https://msdn.microsoft.com/library/windows/hardware/ff538514)デバイスの状態と CM 問題のコードを取得します。 問題によってインストーラーは、トラブルシューティング、ヘルプ ファイル、または何も提供可能性があります。 トラブルシューティングでは、デバイスに問題を解決できる可能性があります。 トラブルシューティングで問題が解決される場合を呼び出す必要が**SetupDiCallClassInstaller**型 DICS_PROPCHANGE の DIF_PROPERTYCHANGE 要求を送信します。 問題解決のヘルプ ファイルを指定のインストーラーがデバイスのトラブルシューティング ツールを指定しない場合、ユーザーのための推奨事項。

インストーラーがない独自のトラブルシューティング ツールを実行する場合、Windows はユーザーに情報を表示する HTML ヘルプを実行します。 インストーラーには、クラスのインストール パラメーターで CHM ファイルが提供されている、Windows はそのファイルを表示します。 それ以外の場合、Windows では、システム提供のトラブルシューティング情報が表示されます。

クラスのインストール パラメーターでは、1 つだけ含めることが**ChmFile**と**HtmlTroubleShooter**ペア。 1 つ以上のインストーラーは、これらの値を指定する場合、Windows は、差分の要求を処理した最後のインストーラーによって設定された値を使用します。

差分のコードの詳細については、[DIF コードの処理](https://msdn.microsoft.com/library/windows/hardware/ff546094)を参照してください。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>Windows Server 2003、Windows XP、および Microsoft Windows 2000 でサポートされています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Setupapi.h (Setupapi.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**CM_Get_DevNode_Status**](https://msdn.microsoft.com/library/windows/hardware/ff538514)

[**SP_DEVINFO_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff552344)

[**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)

[**SP_TROUBLESHOOTER_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff553341)

 

 






