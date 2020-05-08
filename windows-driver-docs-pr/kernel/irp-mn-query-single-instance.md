---
title: IRP_MN_QUERY_SINGLE_INSTANCE
description: WMI をサポートするすべてのドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 104b6b3e-aa5d-437f-8236-02e4abb1ba46
keywords:
- IRP_MN_QUERY_SINGLE_INSTANCE カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: b2f153fdbac9ebf873833b577069d0246f4e270b
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922566"
---
# <a name="irp_mn_query_single_instance"></a>IRP\_の\_全\_クエリ\_の単一インスタンス


WMI をサポートするすべてのドライバーは、この IRP を処理する必要があります。 ドライバーは、wmi Irp を処理できます。詳細につい[**ては、**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバーが WMI[**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出して、 **IRP\_が1つ\_の\_単一\_インスタンス**要求を処理する場合、WMI はその[*ドライバーの設定*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)されたクエリを呼び出します。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)

<a name="when-sent"></a>送信時
---------

WMI は、特定のデータブロックの1つのインスタンスをクエリするために、この IRP を送信します。

WMI は、irp を通した[**\_\_\_EXECUTE メソッド**](irp-mn-execute-method.md)を送信する前に、 **irp\_\_が\_1 つ\_のインスタンス**を送信します。 ドライバーが**irp\_の\_実行\_メソッド**をサポートしている場合は、メソッドが実行されているのと同じデータブロックに対して、irp **\_\_が\_1 つ\_のインスタンス**ハンドラーを持つ必要があります。

WMI は、任意のスレッドコンテキストで\_この IRP を IRQL = パッシブレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


**Parameters. WMI. ProviderId**は、要求に応答する必要があるドライバーのデバイスオブジェクトを指します。 このポインターは、IRP 内のドライバーの i/o スタックの場所にあります。

**データパス**は、クエリを実行するデータブロックを識別する GUID を指します。

**パラメーター** . Wmi. BufferSize は、クエリ対象のインスタンスを識別する[**wnode\_\_単一インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)構造を**指す、非**ページバッファーの最大サイズを示します。

## <a name="output-parameters"></a>出力パラメーター


ドライバーが[*、の Wmi*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback) irp を処理するときに、wmi を処理する場合、wmi[**は、ドライバー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)のデータを使用して、 [**wnode\_の単一\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)構造を設定します。

それ以外の場合、ドライバーは**Wnode\_の\_単一インスタンス**構造を次のように**パラメーター**に設定します。

-   **Wnodeheader. BufferSize**を、出力される**\_wnode の単一\_インスタンス**構造 (インスタンスデータを含む) のサイズ (バイト単位) で更新します。 この値には、インスタンス名の長さ (インスタンスデータがクワッドワード境界で始まるように埋め込まれたもの) が含まれている必要があります。これは、登録されている静的インスタンス名をクエリするクラスとドライバーライターが、この IRP を処理するときに明示的に名前を指定していない場合でも同様です。

-   インスタンスデータの**サイズをバイト単位で設定し**ます。 静的インスタンス名が使用されている場合、この値にインスタンス名のサイズを含めることはできません。

-   インスタンスデータを、データ**バッファー**から開始して、パラメーターに**書き込みます。** ドライバーでは、の入力値を変更すること**はできません。**

**パラメーター**のバッファーが小さすぎてすべてのデータを受け取ることができない場合、ドライバーは、 [**wnode\_が小さすぎる\_**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_too_small)構造で、必要なサイズを設定します。 **Parameters.WMI.Buffer** バッファーが**sizeof**(**wnode\_が\_小さすぎる**) より小さい場合、ドライバーは IRP に失敗し、ステータス\_バッファー\_が\_小さすぎます。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーが、wmi[**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出すことによって irp を処理する場合、WMI は、i/o 状態ブロック内の**irp-&gt;Iostatus. status**と**irp-&gt;iostatus. 情報**を設定します。

それ以外の場合は、ドライバーによって、 **Irp-&gt;Iostatus. STATUS**が正常状態\_に設定されるか、次のような適切なエラー状態に設定されます。

ステータス\_バッファー\_が\_小さすぎます

状態\_WMI\_GUID\_が\_見つかりません

状態\_WMI\_インスタンス\_が\_見つかりません

成功すると、ドライバーは、 **Wnodeheader. BufferSize**に入力された値に**Irp-&gt;iostatus. 情報**を設定します。 この値には、静的インスタンス名の長さが含まれます。

<a name="operation"></a>Operation
---------

ドライバーは、wmi Irp を処理できます。詳細につい[**ては、**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバーが、の呼び出しによって WMI Irp を処理する**場合、この**ドライバーは、 [*DpWmiQueryDataBlock*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)ドライバーのシステム[**コントロールを呼び出し**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)ます。

ドライバーが**IRP\_\_\_の1つ\_のインスタンス**の要求自体を処理する場合は、パラメーターが指定されている場合にのみ、ドライバーが[**iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)の呼び出しで渡されたポインターと同じデバイスオブジェクトを指している必要があります **。** それ以外の場合、ドライバーは、デバイススタック内の次に小さいドライバーに要求を転送する必要があります。

ドライバーは、要求を処理する前に、**データパス**がドライバーでサポートされている GUID を指しているかどうかを判断する必要があります。 一致していない場合は、ドライバーが IRP を\_失敗\_さ\_せ\_、ステータス WMI GUID が見つからないことを返します。

ドライバーは、すべての入力値の検証を担当します。 具体的には、ドライバーが IRP 要求自体を処理する場合は、次の操作を行う必要があります。

-   静的な名前の場合は、 [**Wnode\_の単一\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)構造の**instanceindex**メンバーが、データブロックのドライバーでサポートされているインスタンスインデックスの範囲内であることを確認します。

-   動的名の場合は、ドライバーでサポートされているデータブロックインスタンスがインスタンス名の文字列によって識別されていることを確認します。

-   **パラメーター**で、ドライバーが返すすべてのデータを受け取るのに十分な大きさのバッファーが指定されていることを確認します。

ドライバーでデータブロックがサポートされている場合は、次のように、インスタンス**名の入力** [**wnode\_SINGLE\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)でインスタンス名を確認します。

-   \_Wnode\_フラグの静的\_インスタンス\_名が**wnodeheader. Flags**に設定されている場合、ドライバーは、そのブロックの静的インスタンス名のドライバーリストへのインデックスとして**instanceindex**を使用します。 WMI は、ブロックの登録時にドライバーによって提供された登録データからインデックスを取得します。

-   \_\_\_\_ **Wnodeheader. Flags**で wnode フラグの静的インスタンス名がクリアされている場合、ドライバーは**OffsetInstanceName**のオフセットを使用して、入力**wnode\_SINGLE\_インスタンス**内のインスタンス名の文字列を検索します。 **OffsetInstanceName**は、構造体の先頭から USHORT までのオフセット (バイト単位) です。これは、インスタンス名の文字列の長さ (バイト数ではありません) (存在する場合は終端の null を含み、その後に Unicode のインスタンス名の文字列が続きます) を示します。

指定されたインスタンスがドライバーで見つからない場合は、IRP が失敗し\_、\_WMI\_インスタンス\_が見つからないことを返す必要があります。 動的なインスタンス名を持つインスタンスの場合、この状態はドライバーがインスタンスをサポートしていないことを示します。 そのため、他のプロバイダーがインスタンスを検出しても、他の何らかの理由で要求を処理できない場合、WMI は他のデータプロバイダーのクエリを続行し、適切なエラーをデータコンシューマーに返すことができます。

ドライバーがインスタンスを検索し、要求を処理できる場合、インスタンスのデータを使用して、 **Wnode\_の\_単一インスタンス**構造をパラメーターに入力**し**ます。

インスタンスが有効であっても、ドライバーが要求を処理できない場合は、適切なエラー状態を返すことができます。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>ヘッダー</p></td>
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*すべてのクエリを*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**WMB\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**Wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE\_単一\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)

 

 




