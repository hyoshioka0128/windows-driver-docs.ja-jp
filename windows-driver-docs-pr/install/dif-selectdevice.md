---
title: DIF_SELECTDEVICE
description: DIF_SELECTDEVICE
ms.assetid: c1266182-b88f-406a-876c-e0f15050fdf3
keywords:
- DIF_SELECTDEVICE デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- DIF_SELECTDEVICE
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a0e76a73484167adf1f17d9a027bd694430dc6d8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574812"
---
# <a name="difselectdevice"></a>DIF_SELECTDEVICE


DIF_SELECTDEVICE 要求は、インストーラーへの参加のデバイス ドライバーを選択できます。

### <a name="when-sent"></a>送信時

ときに、新しく列挙されたデバイスのドライバーまたは既存のデバイス (ドライバーの変更) 用の新しいドライバーを選択します。 たとえば、ユーザー選択ハードウェアの追加/削除し、モデム クラスを選択します。 または、ユーザーが PnP デバイスを挿入し、新しいハードウェアの検出ウィザードで「を選択して、ドライバーから、一覧に」を選択します。

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
<td align="left"><p>処理しません</p></td>
</tr>
<tr class="odd">
<td align="left"><p>クラスのインストーラー</p></td>
<td align="left"><p>処理できます。</p></td>
</tr>
</tbody>
</table>

 

### <a name="installer-input"></a>インストーラーの入力

<a href="" id="deviceinfoset"></a>*DeviceInfoSet*  
識別するハンドルを提供、[デバイス情報設定されている](https://msdn.microsoft.com/library/windows/hardware/ff541247)ドライバーを選択するデバイスを格納しています。 [デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)に関連付けられている、 *DeviceInfoSet*します。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
必要に応じてへのポインターを提供、 [ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)デバイス情報のセット内のデバイスを識別する構造体。

場合*DeviceInfoData*は**NULL**、この要求がのドライバーを選択するには、[デバイス セットアップ クラス](https://msdn.microsoft.com/library/windows/hardware/ff541509)に関連付けられている、 *DeviceInfoSet*します。

<a href="" id="device-installation-parameters-"></a>デバイスのインストール パラメーター   
場合*DeviceInfoData*ない**NULL**、デバイスのインストールのパラメーターがある ([**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)) に関連付けられている、*DeviceInfoData*します。 場合*DeviceInfoData*は**NULL**、インストールのパラメーターに関連付けられているデバイスがある、 *DeviceInfoSet*します。

特に興味深いは、 **DriverPath**ドライバーの一覧の構築に使用する INF(s) の場所が含まれています。

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
[ **SP_SELECTDEVICE_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff553326)構造が関連付けられている、 *DeviceInfoData*場合*DeviceInfoData*ない**NULL**します。 それ以外の場合、クラスのインストール パラメーターは、セット全体のデバイス情報に関連付けられています。

### <a name="installer-output"></a>インストーラーの出力

<a href="" id="device-installation-parameters"></a>デバイスのインストール パラメーター  
インストーラーでは、デバイスのインストール パラメーターを変更できます。 これは変更しないでください、ただし、 **DriverPath**フィールド。

<a href="" id="class-installation-parameters"></a>インストール パラメーターをクラスします。  
インストーラーを変更できる、 [ **SP_SELECTDEVICE_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff553326)します。 たとえば、インストーラーは可能性があります、タイトルや Windows でドライバーを選択するユーザーを確認するダイアログ ボックスを使用するための手順に指定します。

インストーラーは、前のインストーラーによって設定されるパラメーターを変更すると、新しい デバイス パラメーターを設定する場合、インストーラーは、フィールドを設定しませんを 0 する必要があります。

### <a name="installer-return-value"></a>インストーラーの戻り値

この差分コードの何も共同インストーラー場合は、前処理のパスから NO_ERROR を返します。 共同インストーラーは、この差分コードを処理する場合する必要があるためプリプロセスで渡す行い NO_ERROR または Win32 エラー コードを返します。 処理後の共同インストーラーが呼び出されるまでに、ドライバーは既に選択されています。

クラスのインストーラーが正常にこの要求を処理する場合と[ **SetupDiCallClassInstaller** ](https://msdn.microsoft.com/library/windows/hardware/ff550922)既定のハンドラーを呼び出す必要があります、その後、クラスのインストーラーが ERROR_DI_DO_DEFAULT を返します。

クラスのインストーラーが正常に既定のハンドラーを直接呼び出しなど、この要求を処理する場合、クラスのインストーラーは NO_ERROR を返す必要がありますと**SetupDiCallClassInstaller**既定ハンドラーその呼び出しはもう一度です。

**注**  クラスのインストーラーは、既定のハンドラーを直接呼び出すことができますが、既定のハンドラーの操作を優先するクラスのインストーラーはいけません。

 

既定のハンドラーを呼び出す方法の詳細については、[既定 DIF コード ハンドラーを呼び出す](https://msdn.microsoft.com/library/windows/hardware/ff537868)を参照してください。

クラスのインストーラーには、エラーが発生すると、インストーラーが適切な Win32 エラー コードを返す必要がありますと**SetupDiCallClassInstaller**既定ハンドラーその呼び出しは。

場合、クラスのインストーラーが ERROR_DI_BAD_PATH を返します、 **DriverPath**の対応するメンバー [ **SP_DEVINSTALL_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff552346)構造体が等しくない**NULL**が、指定したパスの場所で有効なドライバーがないです。 これは、パスの場所でドライバーがない場合、またはドライバーがある場合に発生することができますが、**フラグ**のメンバー、 [ **SP_DRVINSTALL_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff553290)各ドライバーの構造の設定DN_BAD_DRIVER フラグ。 このエラー コードに対しては、Windows には、ユーザーにエラーが表示されます。

### <a name="default-dif-code-handler"></a>既定の差分コード ハンドラー

[**SetupDiSelectDevice**](https://msdn.microsoft.com/library/windows/hardware/ff552115)

### <a name="installer-operation"></a>インストーラーの操作

DIF_SELECTDEVICE 要求に応答してでは、インストーラーは、そのデバイスまたは既定のハンドラーの動作だけでなく、デバイス クラスに必要なすべての選択操作を実行します。 インストーラーには、通常、次の方法のいずれかでこの差分要求に応答しています。

-   何もしない。

    インストーラーには、特別な選択の要件がなければ、この差分コードへの応答には何もしません。 クラスのインストーラーは ERROR_DI_DO_DEFAULT を返し、共同インストーラーには NO_ERROR が返されます。

-   Windows 選択 UI に表示される select 文字列を指定します。

    インストーラーは、クラスのインストール パラメータで select 文字列を指定できます ([**SP_SELECTDEVICE_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff553326))。 たとえば、インストーラーを変更できます、**指示**またはウィンドウのヘッダー**タイトル**します。

    クラスのインストーラー共同インストーラーに select 文字列が既に提供されている場合 select 文字列を指定する必要があります。 共同インストーラーには、おそらく、関連性の高い情報がいます。

    インストーラーを変更する場合、 [ **SP_SELECTDEVICE_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff553326)、インストーラーで DI_USECI_SELECTSTRINGS フラグを設定する必要がありますも、 [ **SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346).

    インストーラーが正常に select 文字列を提供している場合 Windows はまだ既定のハンドラーを呼び出します。 そのため、ここでは、共同インストーラーには NO_ERROR が返され、クラスのインストーラーが ERROR_DI_DO_DEFAULT を返します。

-   デバイスのインストール パラメーターを変更します。

    インストーラーは、デバイスのインストール パラメーターを変更できます ([**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346))。 たとえば、インストーラーが Windows 表示 DI_SHOWOEM フラグを設定可能性があります、**ディスク**ボタンをクリックします。

    クラスのインストーラーは、デバイスのインストール パラメーターを正常に変更、クラスのインストーラーは ERROR_DI_DO_DEFAULT を返します。

-   ユーザーが選択できるドライバーの一覧を変更します。

    このアクションは、以下が一般的で、可能な限りです。 ドライバーを変更するインストーラーが、ボックスの一覧またはそうでない可能性がありますも select 文字列を指定します。

    通常、ドライバーの一覧を変更するインストーラーは、デバイスには不適切なドライバーをマークします。 インストーラーでは、このようなドライバー DNF_BAD_DRIVER フラグでをマークします。 Windows では、ユーザーに表示されます、一覧からこれらのドライバーを省略します。

    インストーラーでは、次の手順で不適切なドライバーをマークします。

    1.  ドライバーの一覧を呼び出すことによってビルド[ **SetupDiBuildDriverInfoList** ](https://msdn.microsoft.com/library/windows/hardware/ff550917)で、 *DriverType* SPDIT_CLASSDRIVER の。
    2.  呼び出すことによってリスト内の最初のドライバーに関する情報を取得[ **SetupDiEnumDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff551018)と[ **SetupDiGetDriverInstallParams** ](https://msdn.microsoft.com/library/windows/hardware/ff551978). ドライバーがデバイスに適切でない場合 DNF_BAD_DRIVER フラグを設定、**フラグ**パラメーターのフィールド。 呼び出すことによって、パラメーターに変更を適用[ **SetupDiSetDriverInstallParams**](https://msdn.microsoft.com/library/windows/hardware/ff552172)します。
    3.  リスト内のすべてのドライバーが処理するまでは、前の手順を繰り返します。 インクリメントするかどうかを確認、 *MemberIndex*パラメーターを**SetupDiEnumDriverInfo**その関数のリファレンス ページで説明されているとします。

    インストーラーはドライバーの一覧で 1 つまたは複数のドライバの DNF_BAD_DRIVER フラグを設定することがありますが、インストーラーは、そのフラグをクリアしない必要があります。

    1 つまたは複数のインストーラーは、ドライバー一覧を正常に変更する場合は、Windows はまだ既定のハンドラーを呼び出します。 そのため、ここでは、共同インストーラーには NO_ERROR が返され、クラスのインストーラーが ERROR_DI_DO_DEFAULT を返します。

-   独自のドライバーの選択ユーザー インターフェイスを表示し、選択したドライバーを設定します。

    クラスのインストーラーのみが、独自のドライバーの選択ユーザー インターフェイスを表示できます。共同インストーラーがない必要があります。 たとえば、クラスのインストーラーは、テキストのリストではなく画像を表示する可能性があります。

    クラスのインストーラーは、選択したドライバーを正常に設定、クラスのインストーラーは NO_ERROR および Windows は、既定のハンドラーを 、ため既定の選択インターフェイスに表示できないを返します。

デバイスのインストール パラメーターで DI_ENUMSINGLEINF フラグが設定されている場合、 **DriverPath**はディレクトリのパスではなく 1 つの INF ファイルのパスです。 インストーラーは、その 1 つの INF のみを使用して、ドライバーの一覧を作成する必要があります。

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
<td align="left"><p>Microsoft Windows 2000 以降のバージョンの Windows でサポートされています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Setupapi.h (Setupapi.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**DIF_NEWDEVICEWIZARD_SELECT**](dif-newdevicewizard-select.md)

[**SetupDiSelectDevice**](https://msdn.microsoft.com/library/windows/hardware/ff552115)

[**SP_DEVINFO_DATA**](https://msdn.microsoft.com/library/windows/hardware/ff552344)

[**SP_DEVINSTALL_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff552346)

[**SP_SELECTDEVICE_PARAMS**](https://msdn.microsoft.com/library/windows/hardware/ff553326)

 

 






