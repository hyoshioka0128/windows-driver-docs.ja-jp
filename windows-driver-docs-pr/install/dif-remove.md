---
title: DIF_REMOVE
description: DIF_REMOVE
ms.assetid: 14429756-c059-46d7-bd1c-0ae57d1ec8b5
keywords:
- DIF_REMOVE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DIF_REMOVE
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2c744d5160f981939c2650b0cfb88dc89d6ae69c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365849"
---
# <a name="difremove"></a>DIF_REMOVE


DIF_REMOVE 要求は、Windows がデバイスを削除しようし、インストーラーを削除するために準備する機会が与えられますインストーラーを通知します。

### <a name="when-sent"></a>送信時

ときに、ユーザーは、デバイス マネージャーでデバイスを削除します。

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
識別するハンドルを提供、[デバイス情報設定されている](https://msdn.microsoft.com/library/windows/hardware/ff541247)を削除するデバイスを格納しています。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
ポインターを提供する[ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)デバイス情報のセットでのデバイスの構造体。

<a href="" id="device-installation-parameters-"></a>デバイスのインストール パラメーター   
デバイス インストールのパラメーターがある ([**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)) に関連付けられている、 *DeviceInfoData*します。

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
[ **SP_REMOVEDEVICE_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff553323)構造が関連付けられる可能性があります、 *DeviceInfoData*します。

DI_CLASSINSTALLPARAMS フラグがオフの場合、要求のクラスのインストールのパラメーターがない、 [ **SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)します。 この場合は、ハードウェア プロファイルが指定されていないと、デバイスは、全体として、システムから削除します。

### <a name="installer-output"></a>インストーラーの出力

<a href="" id="none"></a>[なし]  

### <a name="installer-return-value"></a>インストーラーの戻り値

共同インストーラーには、NO_ERROR、ERROR_DI_POSTPROCESSING_REQUIRED、または Win32 エラー コードを返すことができます。

クラスのインストーラーが正常にこの要求を処理する場合と[ **SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922)既定のハンドラーを呼び出す必要があります、その後、クラスのインストーラーが ERROR_DI_DO_DEFAULT を返します。

クラスのインストーラーが正常に既定のハンドラーを直接呼び出しなど、この要求を処理する場合、クラスのインストーラーは NO_ERROR を返す必要がありますと**SetupDiCallClassInstaller**既定ハンドラーその呼び出しはもう一度です。

**注**  クラスのインストーラーは、既定のハンドラーを直接呼び出すことができますが、既定のハンドラーの操作を優先するクラスのインストーラーはいけません。

 

既定のハンドラーを呼び出す方法の詳細については、次を参照してください。[既定 DIF コード ハンドラーを呼び出す](https://msdn.microsoft.com/library/windows/hardware/ff537868)します。

クラスのインストーラーには、エラーが発生すると、インストーラーが適切な Win32 エラー コードを返す必要がありますと**SetupDiCallClassInstaller**既定ハンドラーその呼び出しは。

### <a name="default-dif-code-handler"></a>既定の差分コード ハンドラー

[**SetupDiRemoveDevice**](https://msdn.microsoft.com/library/windows/hardware/ff552097)

### <a name="installer-operation"></a>インストーラーの操作

DIF_REMOVE 要求に応答して、インストーラーは通常、一部のクリーンアップ操作を実行します。 この場合、共同インストーラーは NO_ERROR を返しクラスのインストーラーが ERROR_DI_DO_DEFAULT を返します。

インストーラーでは、デバイスが削除されないことを判断した場合、インストーラー Win32 エラー コードを返すことによって、差分要求は失敗します。 DI_QUIETINSTALL フラグがオフの場合は、インストーラーは、デバイスが削除されていない理由を説明するメッセージを表示する必要があります。

共同インストーラーを呼び出すことによって自分のデバイスを削除する必要がありますしない**SetupDiRemoveDevice**します。 共同インストーラーは、通常、処理後のデバイスが正常に削除された後でこの要求を処理します。

レジストリ内の情報を削除する共同インストーラーがある場合は、後処理とのみの場合に前のインストーラーは、削除要求が成功したのでなど共同インストーラーは行う必要があります。 前処理のパスで共同インストーラーはコンテキスト パラメーターにレジストリ情報を格納し、ERROR_DI_POSTPROCESSING_REQUIRED 処理後の要求を返す必要があります。 Windows では、この差分要求の処理後の共同インストーラーを呼び出し、差分の状態は NO_ERROR と、レジストリ情報を削除し、共同インストーラーをチェックする必要があります。 共同インストーラーの前処理パスでのレジストリ情報を削除し、クラスのインストーラー (または別の共同インストーラー) に、DIF_REMOVE が失敗した場合、共同インストーラーで、デバイスが、予期しない状態で残る可能性があります。

インストーラーがファイルを削除この差分要求を処理するときに、ファイルが別のデバイスによって使用されている場合に。

Windows では、PnP - クエリの削除を開始する前に、この差分要求を送信し、処理を削除します。

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


[**SetupDiRemoveDevice**](https://msdn.microsoft.com/library/windows/hardware/ff552097)

[**SP_DEVINFO_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff552344)

[**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)

[**SP_REMOVEDEVICE_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff553323)

 

 






