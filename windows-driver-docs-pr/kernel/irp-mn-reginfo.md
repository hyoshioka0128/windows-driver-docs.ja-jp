---
title: IRP_MN_REGINFO
description: Microsoft Windows 98 と Microsoft Windows 2000 で WMI をサポートするドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: db93b64b-a2e4-429d-850e-921fb438467c
keywords:
- IRP_MN_REGINFO Kernel-Mode Driver Architecture
ms.localizationpriority: medium
ms.openlocfilehash: 527b317615dcd032d0b8eab3652c0de4c39927e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528912"
---
# <a name="irpmnreginfo"></a>IRP\_MN\_REGINFO


Microsoft Windows 98 と Microsoft Windows 2000 で WMI をサポートするドライバーは、この IRP を処理する必要があります。 (Windows XP をもサポートするドライバーを処理する必要がありますも、 [ **IRP\_MN\_REGINFO\_EX** ](irp-mn-reginfo-ex.md) IRP)。ドライバーを処理できる WMI Irp を呼び出すか[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)または」の説明に従って、IRP を処理することによって[WMI 要求の処理](https://msdn.microsoft.com/library/windows/hardware/ff546968)します。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)送信されるときに
---------

WMI では、Windows 98 および Windows 2000 では、クエリまたはドライバーが呼び出された後に、ドライバーの登録情報を更新するには、この IRP が送信[ **IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)します。 Windows xp 以降、WMI の送信、 **IRP\_MN\_REGINFO\_EX**代わりに要求します。

WMI IRQL でこの IRP の送信 = パッシブ\_システム スレッドのコンテキスト内のレベル。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.WMI.ProviderId**要求に応答する必要がありますドライバーのデバイス オブジェクトを指します。 このポインターは、ドライバーの IRP で I/O スタックの場所にあります。

**Parameters.WMI.DataPath**に設定されている**WMIREGISTER**登録情報のクエリまたは**WMIUPDATE**に更新します。

**Parameters.WMI.BufferSize** nonpaged、バッファーの最大サイズを示す**Parameters.WMI.Buffer**します。 サイズが合計以上にする必要があります (**sizeof**(**WMIREGINFO**) + (*GuidCount* \* **sizeof**(**WMIREGGUID**)) という*GuidCount*データ ブロックの数は、イベントが存在する場合は、ドライバーと静的インスタンスの名前の領域によって登録されているをブロックします。

## <a name="output-parameters"></a>出力パラメーター


ドライバーが呼び出すことによって WMI Irp を処理する場合[ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)、WMI を呼び出してドライバーのデータ ブロックの登録情報の取得、 [ *DpWmiQueryReginfo*](https://msdn.microsoft.com/library/windows/hardware/ff544097)ルーチン。

それ以外の場合、ドライバーを設定、 [ **WMIREGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff565832)で構造体**Parameters.WMI.Buffer**次のようにします。

-   セット**BufferSize**のバイト単位のサイズを**WMIREGINFO**プラス構造体には、登録データが関連付けられています。

-   ドライバーは、別のドライバーの代わりに WMI 要求を処理する場合は、設定**NextWmiRegInfo**これの先頭からバイトのオフセットに**WMIREGINFO**別の先頭に**WMIREGINFO**他のドライバーからの登録情報を含む構造体。

-   セット**RegistryPath**ドライバーに渡されたレジストリ パスに[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)ルーチン。

-   場合**Parameters.WMI.Datapath**に設定されている**WMIREGISTER**、設定**MofResourceName**これの先頭からのオフセットを**WMIREGINFO**をイメージ ファイルで、ドライバーの MOF リソースの名前を含むカウントされた Unicode 文字列にします。

-   セット**GuidCount**イベント ブロックを登録または更新、データ ブロックの数。

-   配列を書き込みます[ **WMIREGGUID** ](https://msdn.microsoft.com/library/windows/hardware/ff565827)構造、各データ ブロックに、ドライバーによって公開されるイベントのブロックの 1 つ**WmiRegGuid**します。

ドライバーは、それぞれが**WMIREGGUID**次のように構造体します。

-   セット**Guid**ブロックを識別する guid。

-   セット**フラグ**インスタンス名と、ブロックの他の特性に関する情報を提供します。 たとえば、静的なインスタンスの名前を持つ、ブロックが登録されている場合、ドライバーが設定します**フラグ**で適切な WMIREG\_フラグ\_インスタンス\_*XXX*フラグ.

場合は、ブロックは、静的なインスタンス名、ドライバーに登録しています。

-   セット**InstanceCount**インスタンス数にします。

-   ブロックの静的インスタンスの名前のデータをバイト単位でのオフセットを次のメンバーのいずれかを設定します。
    -   ドライバーが設定されている場合**フラグ**WMIREG で\_フラグ\_インスタンス\_設定一覧で、 **InstanceNameList**静的インスタンス名の文字列のリストへのオフセットにします。 WMI は、このリストにインデックスを使用して後続の要求でのインスタンスを指定します。
    -   ドライバーが設定されている場合**フラグ**WMIREG で\_フラグ\_インスタンス\_設定 BASENAME、 **BaseNameOffset**基本名文字列へのオフセットにします。 WMI では、この文字列を使用して、ブロックの静的インスタンス名を生成します。
    -   ドライバーが設定されている場合**フラグ**WMIREG で\_フラグ\_インスタンス\_設定 PDO、 **Pdo** PDO へのポインターをオフセットするドライバーに渡す[*AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)ルーチン。 WMI では、ブロックの静的インスタンス名を生成するのに、PDO のデバイスのインスタンスのパスを使用します。
-   インスタンス名の文字列、基本名の文字列またはポインターによって示されるオフセット PDO に書き込む**InstanceNameList**、 **BaseName**、または**Pdo**、それぞれします。

他のドライバーの登録情報を別の WMIREGINFO 構造体に格納し、書き込みますで、ドライバーは、(miniclass またはミニポート ドライバー) などの別のドライバーに代わって WMI 登録を処理する場合**NextWmiRegInfo**以前の構造。

場合、バッファー **Parameters.WMI.Buffer**が小さすぎてすべてのデータを受信するドライバー、必要なサイズ (バイト単位) として書き込む ULONG **Parameters.WMI.Buffer** IRP が失敗して、のステータスを返します\_バッファー\_すぎます\_小さい。

## <a name="io-status-block"></a>I/O ステータス ブロック


呼び出すことによって、ドライバーが IRP を処理する場合[ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)、WMI セット**Irp -&gt;IoStatus.Status**と**Irp-&gt;IoStatus.Information**状態の I/O ブロックにします。

それ以外の場合、ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功または適切なエラーの状態、次のように。

ステータス\_バッファー\_すぎます\_小さな

成功した場合、ドライバーの設定**Irp -&gt;IoStatus.Information** 、バッファーに書き込まれたバイト数に**Parameters.WMI.Buffer**します。

<a name="operation"></a>操作
---------

ドライバーを処理できる WMI Irp を呼び出すか[ **WmiSystemControl** ](https://msdn.microsoft.com/library/windows/hardware/ff565834)または」の説明に従って、IRP を処理することによって[WMI 要求の処理](https://msdn.microsoft.com/library/windows/hardware/ff546968)します。

ドライバーを呼び出して WMI Irp の処理する場合[ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)、ドライバーが、ルーチンを呼び出す[ *DpWmiQueryReginfo* ](https://msdn.microsoft.com/library/windows/hardware/ff544097)ルーチン。

ドライバーが処理する場合、 **IRP\_MN\_REGINFO**要求自体には、その方がよい場合にのみ**Parameters.WMI.ProviderId**ポインターと同じデバイス オブジェクトをポイントする、渡されるドライバー [ **IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)します。 それ以外の場合、ドライバーでは、次の下位のドライバーに要求を転送する必要があります。

要求を処理する前に、ドライバーを確認する必要があります**Parameters.WMI.DataPath** WMI が登録情報を照会しているかどうかを判断する (**WMIREGISTER**) または更新を要求する (**WMIUPDATE**)。

ドライバーを呼び出してから、WMI が WMIREGISTER では、この IRP を送信します**IoWMIRegistrationControl** WMIREG で\_アクション\_登録または WMIREG\_アクション\_を再登録します。 応答として、バッファー内のドライバーの塗りつぶし**Parameters.WMI.Buffer**次。

-   A [ **WMIREGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff565832)ドライバーのレジストリ パス、名前の MOF リソースの登録をブロックの数を示す構造体。

-   1 つ[**WMIREGGUID** ](https://msdn.microsoft.com/library/windows/hardware/ff565827)を登録するには、各ブロックの構造体。 ドライバーが適切な WMIREG を設定する場合は、ブロックは、静的なインスタンス名を登録することは、\_フラグ\_インスタンス\_*XXX*フラグ、 **WMIREGGUID**そのブロックの構造体。

-   任意の文字列 WMI は、静的なインスタンス名を生成する必要があります。

WMI では、この IRP の送信**WMIUPDATE**ドライバーを呼び出してから**IoWmiRegistrationControl** WMIREG で\_アクション\_UPDATE\_GUID。 応答として、バッファー内のドライバーの塗りつぶし**Parameters.WMI.Buffer** WMIREGINFO で次のように構造体します。

-   ドライバーが WMIREG を設定するブロックを削除する\_フラグ\_削除\_で GUID の**WMIREGGUID**構造体。

-   WMIREG をクリアするドライバーを追加または更新 (たとえば、その静的インスタンスの名前を変更する場合) ブロックを\_フラグ\_削除\_GUID と、ブロックの新しいまたは更新された登録値を提供します。

-   ドライバーの適切な WMIREG の設定に静的なインスタンスの名前を新規または既存のブロックを登録する\_フラグ\_インスタンス\_*XXX*し、WMI は、静的インスタンスを生成する必要がある任意の文字列を提供します。名前。

ドライバーを使用して同じ**WMIREGINFO**構造を削除するには、追加、または、最初にすべてのフラグとデータを更新するブロックのみを変更する、そのブロックを登録するために使用されるブロックを更新します。 場合、 **WMIREGGUID**などで、 **WMIREGINFO**構造と正確に一致する、 **WMIREGGUID**ドライバーによって渡されるとそのブロックを最初に登録されているときに、WMI は、処理はスキップしますブロックの更新に関与します。

WMI は送信しません、 **IRP\_MN\_REGINFO**ドライバーを呼び出してからの要求[ **IoWMIRegistrationControl** ](https://msdn.microsoft.com/library/windows/hardware/ff550480) WMIREG で\_アクション\_WMI には、ドライバーからさらに情報は必要ありませんので、登録解除します。 ドライバーの通常のブロックへの応答で登録を解除する[ **IRP\_MN\_削除\_デバイス**](irp-mn-remove-device.md)要求。

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


[*DpWmiQueryReginfo*](https://msdn.microsoft.com/library/windows/hardware/ff544097)

[**IoWMIRegistrationControl**](https://msdn.microsoft.com/library/windows/hardware/ff550480)

[**WMILIB\_CONTEXT**](https://msdn.microsoft.com/library/windows/hardware/ff565813)

[**WMIREGGUID**](https://msdn.microsoft.com/library/windows/hardware/ff565827)

[**WMIREGINFO**](https://msdn.microsoft.com/library/windows/hardware/ff565832)

[**WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)

[**IRP\_MN\_REGINFO\_EX**](irp-mn-reginfo-ex.md)

 

 




