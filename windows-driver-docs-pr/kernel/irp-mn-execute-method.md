---
title: IRP_MN_EXECUTE_METHOD
description: データ ブロック内のメソッドをサポートするすべてのドライバーでは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: cc42340e-4a7c-475c-b44d-2127e8a0d7dc
keywords:
- IRP_MN_EXECUTE_METHOD カーネル モード ドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: bbc089c4d3fc154e223a3981a5d094a7454a8090
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353357"
---
# <a name="irpmnexecutemethod"></a>IRP\_MN\_EXECUTE\_メソッド


データ ブロック内のメソッドをサポートするすべてのドライバーでは、この IRP を処理する必要があります。 ドライバーを処理できる WMI Irp を呼び出すか[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)または」の説明に従って、IRP を処理することによって[WMI 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)します。

ドライバーを呼び出す場合[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)処理するために、 **IRP\_MN\_EXECUTE\_メソッド**WMI がさらに呼び出しを要求します。ドライバーの[ *DpWmiExecuteMethod* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_execute_method_callback)ルーチン。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)送信されるときに
---------

WMI では、データ ブロックに関連付けられているメソッドを実行するには、この IRP を送信します。

WMI IRQL でこの IRP の送信 = パッシブ\_任意のスレッド コンテキストでします。

WMI を送り、 [ **IRP\_MN\_クエリ\_単一\_インスタンス**](irp-mn-query-single-instance.md)送信する前に、 **IRP\_MN\_EXECUTE\_メソッド**します。 ドライバーをサポートしている場合**IRP\_MN\_EXECUTE\_メソッド**必要があります、 **IRP\_MN\_クエリ\_単一\_インスタンス**メソッドが実行されている同じデータ ブロックのハンドラー。

## <a name="input-parameters"></a>入力パラメーター


**Parameters.WMI.ProviderId**要求に応答する必要がありますドライバーのデバイス オブジェクトを指します。 このポインターは、ドライバーの IRP で I/O スタックの場所にあります。

**Parameters.WMI.DataPath**に実行するメソッドに関連付けられているデータ ブロックを識別する GUID をポイントします。

**Parameters.WMI.BufferSize** nonpaged、バッファーのサイズを示します**Parameters.WMI.Buffer**対象&gt; =  **sizeof**(**れた WNODE\_メソッド\_項目**) と、任意のサイズは、メソッドのデータを出力します。

**Parameters.WMI.Buffer**を指す、 [**れた WNODE\_メソッド\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_method_item)構造の**メソッド Id**を示します、実行するメソッドの識別子と**DataBlockOffset**存在する場合、入力データの最初のバイトを構造体の先頭からのバイト オフセットを示します。 **Parameters.WMI.Buffer -&gt;SizeDataBlock**入力のバイト単位のサイズを示す**れた WNODE\_メソッド\_項目**入力データを含むまたは入力がない場合は 0。

## <a name="output-parameters"></a>出力パラメーター


ドライバーを呼び出して WMI Irp の処理する場合[ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)、WMI を入力、 [**れた WNODE\_メソッド\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_method_item)ドライバーのによって返されるデータで[ *DpWmiExecuteMethod* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_execute_method_callback)ルーチン。

それ以外の場合、ドライバーの設定、**れた WNODE\_メソッド\_項目**構造体**Parameters.WMI.Buffer**次のように指します。

-   更新プログラム**WnodeHeader.BufferSize**出力のサイズと**れた WNODE\_メソッド\_項目**、出力データを含むいずれか。

-   更新プログラム**SizeDataBlock**出力データが存在しない場合は 0 個、出力データのサイズ。

-   チェック**Parameters.WMI.Buffersize**バッファーが出力を受信するのに十分な大きさかどうかを判断する**れた WNODE\_メソッド\_項目**出力データを含むいずれか。 ドライバーで必要なサイズ設定、バッファーが十分ない場合、 [**れた WNODE\_すぎます\_小さな**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_too_small)によって示される構造**Parameters.WMI.Buffer**. バッファーがより小さい場合**sizeof**(**れた WNODE\_すぎます\_小さな**)、ドライバーは IRP が失敗し、ステータスを返します\_バッファー\_すぎます\_小さい。

-   入力データを開始位置として経由では、存在する場合、出力データを書き込みます**DataBlockOffset**します。 ドライバーは、入力値を変更する必要があります**DataBlockOffset**します。

## <a name="io-status-block"></a>I/O ステータス ブロック


呼び出すことによって、ドライバーが IRP を処理する場合[ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)、WMI セット**Irp -&gt;IoStatus.Status**と**Irp-&gt;IoStatus.Information**状態の I/O ブロックにします。

それ以外の場合、ドライバーの設定**Irp -&gt;IoStatus.Status**ステータス\_成功または適切なエラーの状態、次のように。

ステータス\_バッファー\_すぎます\_小さな

ステータス\_WMI\_GUID\_いない\_が見つかりました

ステータス\_WMI\_インスタンス\_いない\_が見つかりました

ステータス\_WMI\_ITEMID\_いない\_が見つかりました

成功した場合、ドライバーの設定**Irp -&gt;IoStatus.Information** 、バッファーに書き込まれたバイト数に**Parameters.WMI.Buffer**します。

<a name="operation"></a>操作
---------

ドライバーを処理できる WMI Irp を呼び出すか[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)または」の説明に従って、IRP を処理することによって[WMI 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)します。

ドライバーを呼び出して WMI Irp の処理する場合[ **WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)、ドライバーが、ルーチンを呼び出す[ *DpWmiExecuteMethod* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_execute_method_callback)ルーチン、またはステータスを返します\_無効な\_デバイス\_ドライバーが、ルーチンを定義していないかどうかに要求します。

ドライバーが処理する場合、 **IRP\_MN\_EXECUTE\_メソッド**自体、要求が行う必要がある場合にのみ**Parameters.WMI.ProviderId**として同じデバイス オブジェクトを指し示すドライバーに渡されたポインター [ **IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)します。 それ以外の場合、ドライバーでは、次の下位のドライバーに要求を転送する必要があります。

ドライバーがすべての入力値を検証する責任を負います。 具体的には、ドライバーは IRP 要求自体を処理する場合、次を実行する必要があります。

-   静的な名前のことを確認します、 **InstanceIndex**のメンバー、 [**れた WNODE\_メソッド\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_method_item)がインスタンスの範囲内に構造体データ ブロックのドライバーでサポートされるインデックス。

-   動的な名前は、インスタンス名の文字列が、ドライバーでサポートされるデータ ブロックのインスタンスを識別することを確認します。

-   いることを確認、**メソッド Id**のメンバー、 [**れた WNODE\_メソッド\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_method_item)がでサポートされているメソッドの識別子の範囲内に構造体データ ブロックのドライバー、呼び出し元がメソッドの実行に許可されているとします。

-   いることを確認、 **DataBlockOffset**と**SizeDataBlock**のメンバー、 [**れた WNODE\_メソッド\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_method_item)構造が指定されたメソッドのパラメーターを格納するのに十分な大きさであるとパラメーターは、メソッドに対して有効なバッファーについて説明します。

-   いることを確認**Parameters.WMI.Buffersize**を受信するのに十分な大きさであるバッファーを指定します、**れた WNODE\_メソッド\_項目**が出力に更新された後に構造体データ。

発信側ユーザー モード アプリケーションのスレッド コンテキストと見なさないでください: より高度なドライバー、変更がある可能性があります。

要求を処理する前に、ドライバーを決定する必要があるかどうか**Parameters.WMI.DataPath**ドライバーでサポートされている GUID を指します。 そうでない、ドライバーが IRP が失敗する必要があり、状態を返す場合\_WMI\_GUID\_いない\_が見つかりました。

ドライバーは、データ ブロックをサポートする場合、入力を確認します[**れた WNODE\_メソッド\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_method_item)で**Parameters.WMI.Buffer**インスタンス名。、次のようにします。

-   場合れた WNODE\_フラグ\_静的\_インスタンス\_で名前が設定されて**WnodeHeader.Flags**、ドライバーを使用して**InstanceIndex**へのインデックスとして、そのブロックの静的インスタンス名のドライバーの一覧。 WMI では、ブロックが登録されているときに、ドライバーによって提供された登録データからインデックスを取得します。

-   場合れた WNODE\_フラグ\_静的\_インスタンス\_名が明確では**WnodeHeader.Flags、** ドライバーは、オフセットを使用して**OffsetInstanceName**に入力内でインスタンス名の文字列を検索**れた WNODE\_メソッド\_項目**します。 **OffsetInstanceName**に存在すると、インスタンス名の文字列に続く場合は、終端の null を含むバイト (しない文字) でインスタンス名文字列の長さである USHORT 構造体の先頭からのバイト オフセットですUnicode。

ドライバーでは、指定されたインスタンスで特定できない場合は、IRP が失敗し、状態を返すする必要があります\_WMI\_インスタンス\_いない\_が見つかりました。 動的なインスタンスの名前を持つインスタンスの場合は、この状態は、ドライバーが、インスタンスをサポートしていないことを示します。 WMI は、他のデータ プロバイダーのクエリを実行し、別のプロバイダーはインスタンスを検索しますが、何らかの理由で要求を処理できない場合は、適切なエラーをデータ コンシューマーに返されます。 そのため続行できます。

ドライバーは、入力にメソッド ID を確認します**れた WNODE\_メソッド\_項目**データ ブロックに対して有効なメソッドがあるかどうかを判断します。 そうでないドライバーは IRP が失敗し、ステータスを返す場合\_WMI\_ITEMID\_いない\_が見つかりました。

ドライバーが出力バッファーのサイズを確認する必要があります、メソッドは、出力を生成する場合**Parameters.WMI.BufferSize**副作用がある可能性がありますか、2 回実行しないようにするすべての操作を実行する前にします。 やなどの場合は、メソッドは、カウンターのグループの値を返し、カウンターをリセットし、ドライバーする必要がありますバッファー サイズを確認 (バッファーが小さすぎる場合は IRP を失敗) カウンターをリセットする前にします。 これにより、WMI の場合より大きなバッファーで要求を安全に再送します。

インスタンスとメソッド ID が有効なバッファーがサイズで適切な場合は、ドライバーは、メソッドを実行します。 場合**SizeDataBlock**入力に**れた WNODE\_メソッド\_項目**が 0 以外の場合、ドライバーを使用して、データの開始位置として**DataBlockOffset**入力としてメソッド。

ドライバーが開始位置として、バッファーに出力データを書き込みます、メソッドは、出力を生成する場合**DataBlockOffset**設定と**SizeDataBlock**出力**れた WNODE\_メソッド\_項目**出力データのバイト数にします。 ドライバーの設定、メソッドには、出力データがなければ、 **SizeDataBlock**をゼロにします。 ドライバーは、入力値を変更する必要があります**DataBlockOffset**します。

インスタンスが有効では、ドライバーが要求を処理できない場合は、すべての該当するエラー状態を返すできます。

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


[*DpWmiExecuteMethod*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nc-wmilib-wmi_execute_method_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)

[**WMILIB\_CONTEXT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/ns-wmilib-_wmilib_context)

[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)

[**れた WNODE\_メソッド\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_method_item)

 

 




