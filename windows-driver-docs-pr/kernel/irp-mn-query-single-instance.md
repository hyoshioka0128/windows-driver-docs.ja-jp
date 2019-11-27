---
title: IRP_MN_QUERY_SINGLE_INSTANCE
description: WMI をサポートするすべてのドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 104b6b3e-aa5d-437f-8236-02e4abb1ba46
keywords:
- IRP_MN_QUERY_SINGLE_INSTANCE カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 6c558f6fabc7462cc0959a26f3f2729ecf1ae5ce
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827980"
---
# <a name="irp_mn_query_single_instance"></a>IRP\_\_クエリ\_単一\_インスタンス


WMI をサポートするすべてのドライバーは、この IRP を処理する必要があります。 ドライバーは、wmi Irp を処理できます。詳細につい[**ては、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバーが、 **1 つの\_インスタンスの要求\_\_クエリ**を処理するために、呼び出し元を呼び出すように wmi[**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出すと、WMI はその[*ドライバーの*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)\_を呼び出します。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)送信時
---------

WMI は、特定のデータブロックの1つのインスタンスをクエリするために、この IRP を送信します。

WMI は、irp\_を送信する前に **\_1 つの\_インスタンスに irp\_\_クエリ**を送信し、 [ **\_メソッドを実行**](irp-mn-execute-method.md)します。\_ ドライバーが、 **\_メソッドを実行\_の irp\_** をサポートしている場合、そのメソッドが実行されている同じデータブロックに対して、 **1 つの\_インスタンス**ハンドラーに対して、irp\_の完了\_クエリを実行する必要があります。\_

WMI は、任意のスレッドコンテキストで、IRQL = パッシブ\_レベルでこの IRP を送信します。

## <a name="input-parameters"></a>入力パラメーター


**Parameters. WMI. ProviderId**は、要求に応答する必要があるドライバーのデバイスオブジェクトを指します。 このポインターは、IRP 内のドライバーの i/o スタックの場所にあります。

**データパス**は、クエリを実行するデータブロックを識別する GUID を指します。

**パラメーター** 。 Wmi. **buffer**は、非ページバッファーの最大サイズを示します。これは、クエリを実行するインスタンスを識別する[**wnode\_単一の\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)構造を指します。

## <a name="output-parameters"></a>出力パラメーター


ドライバーが、の WMI Irp を処理するときに、wmi を処理する場合、wmi[**は、ドライバー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)[*のデータ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)を使用して、 [**wnode\_1 つの\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)構造体を格納します。

それ以外の場合は、次のように、ドライバーは**Wnode\_SINGLE\_INSTANCE**構造体を**Parameters. WMI**に格納します。

-   インスタンスデータを含む、出力**Wnode\_単一\_インスタンス**構造体のサイズ (バイト単位) を使用して**wnodeheader. BufferSize**を更新します。 この値には、登録されている静的インスタンス名をクエリするクラスとドライバーライターがサービスの際に明示的に名前を指定していない場合でも、インスタンス名の長さを含める必要があります (インスタンスデータがクワッドワード境界で始まるように埋め込まれます)。この IRP。

-   インスタンスデータの**サイズをバイト単位で設定し**ます。 静的インスタンス名が使用されている場合、この値にインスタンス名のサイズを含めることはできません。

-   インスタンスデータを、データ**バッファー**から開始して、パラメーターに**書き込みます。** ドライバーでは、の入力値を変更すること**はできません。**

**パラメーター**のバッファーが小さすぎてすべてのデータを受け取ることができない場合、ドライバーは[**wnode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_too_small)に必要なサイズを入力するだけで、\_の小さな構造を\_**ます。** バッファーが**sizeof**(**wnode\_が\_小さい**) より小さい場合、ドライバーは IRP に失敗し、ステータス\_バッファー\_\_小さすぎることを返します。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーが、wmi[**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出すことによって irp を処理する場合、WMI は、i/o 状態ブロック内の**irp&gt;Iostatus. Status**と**Irp&gt;iostatus. 情報**を設定します。

それ以外の場合、ドライバーは**Irp&gt;iostatus. status**を STATUS\_SUCCESS に、または次のような適切なエラー状態に設定します。

状態\_バッファー\_\_小さすぎます

ステータス\_WMI\_GUID\_見つかりませんでした\_

ステータス\_WMI\_インスタンス\_見つかりませ\_んでした

成功すると、ドライバーは**Irp&gt;IoStatus. 情報**を、 **Wnodeheader. BufferSize**に入力された値に設定します。 この値には、静的インスタンス名の長さが含まれます。

<a name="operation"></a>操作
---------

ドライバーは、wmi Irp を処理できます。詳細につい[**ては、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバーが、の呼び出しによって WMI Irp を処理する**場合、この**ドライバーは、 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)ドライバーのシステム[**コントロールを呼び出し**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)ます。

ドライバーが IRP\_を処理する **\_クエリ\_単一\_インスタンス**の要求自体を処理する場合は、パラメーターがの呼び出しで渡されたポインターと同じデバイスオブジェクトを指すようにする必要があり**ます。** [**Iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)。 それ以外の場合、ドライバーは、デバイススタック内の次に小さいドライバーに要求を転送する必要があります。

ドライバーは、要求を処理する前に、**データパス**がドライバーでサポートされている GUID を指しているかどうかを判断する必要があります。 それ以外の場合は、ドライバーが IRP を失敗させ、ステータスを返す必要があります。 WMI\_GUID\_見つかりませ\_ん\_ます。

ドライバーは、すべての入力値の検証を担当します。 具体的には、ドライバーが IRP 要求自体を処理する場合は、次の操作を行う必要があります。

-   静的な名前の場合は、Wnode の**Instanceindex**メンバーが、データブロックのドライバーによってサポートされているインスタンスインデックスの範囲内にあることを確認します。この場合、 [ **\_インスタンス構造\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)ます。

-   動的名の場合は、ドライバーでサポートされているデータブロックインスタンスがインスタンス名の文字列によって識別されていることを確認します。

-   **パラメーター**で、ドライバーが返すすべてのデータを受け取るのに十分な大きさのバッファーが指定されていることを確認します。

ドライバーがデータブロックをサポートしている場合は、次のように、インスタンス名の入力[**Wnode\_単一の\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)**を使用し**てインスタンス名を確認します。

-   WNODE\_フラグ\_静的\_インスタンス\_名前が**Wnodeheader. Flags**に設定されている場合、ドライバーは、そのブロックのドライバーの静的インスタンス名の一覧へのインデックスとして**instanceindex**を使用します。 WMI は、ブロックの登録時にドライバーによって提供された登録データからインデックスを取得します。

-   WNODE\_フラグ\_静的\_インスタンス\_名前が**Wnodeheader. Flags**で明確である場合、ドライバーは**OffsetInstanceName**のオフセットを使用して、入力 wnode\_SINGLE のインスタンス名の文字列を検索し **\_インスタンス**。 **OffsetInstanceName**は、構造体の先頭から USHORT までのオフセット (バイト単位) です。これは、インスタンス名の文字列の長さ (バイト数ではありません) (存在する場合は終端の null を含み、その後にのインスタンス名の文字列) です。対応.

ドライバーは、指定されたインスタンスを見つけることができない場合、IRP を失敗させ、ステータス\_WMI\_インスタンス\_見つから\_ないことを確認します。 動的なインスタンス名を持つインスタンスの場合、この状態はドライバーがインスタンスをサポートしていないことを示します。 そのため、他のプロバイダーがインスタンスを検出しても、他の何らかの理由で要求を処理できない場合、WMI は他のデータプロバイダーのクエリを続行し、適切なエラーをデータコンシューマーに返すことができます。

ドライバーがインスタンスを検索し、要求を処理できる場合、Wnode は、インスタンスのデータを使用して、 **Wnode\_単一の\_インスタンス**構造に格納**します。**

インスタンスが有効であっても、ドライバーが要求を処理できない場合は、適切なエラー状態を返すことができます。

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
<td>Wdm.h (Wdm.h、Ntddk.h、Ntifs.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*すべてのクエリを*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_datablock_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**WMB\_のコンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**Wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE\_単一\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)

 

 




