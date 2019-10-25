---
title: IRP_MN_CHANGE_SINGLE_INSTANCE
description: WMI をサポートするすべてのドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 180d40a4-b300-4801-b9da-9239500ca15f
keywords:
- IRP_MN_CHANGE_SINGLE_INSTANCE カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: a244cb92457326df4c9ce35af7d8d5495417024f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828073"
---
# <a name="irp_mn_change_single_instance"></a>IRP\_\_1 つの\_インスタンス\_変更


WMI をサポートするすべてのドライバーは、この IRP を処理する必要があります。 ドライバーは、wmi Irp を処理できます。詳細につい[**ては、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバーが、 **1 つの\_インスタンスの要求\_\_変更**された IRP\_を処理するために、呼び出し元は、その[*ドライバーの設定*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_datablock_callback)されたインスタンス[**を呼び出します**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)送信時
---------

WMI は、データブロックの単一インスタンス内のすべてのデータ項目を変更するために、この IRP を送信します。

WMI は、任意のスレッドコンテキストで、IRQL = パッシブ\_レベルでこの IRP を送信します。

## <a name="input-parameters"></a>入力パラメーター


**Parameters. WMI. ProviderId**は、要求に応答する必要があるドライバーのデバイスオブジェクトを指します。 このポインターは、IRP 内のドライバーの i/o スタックの場所にあります。

**データパス**は、変更するインスタンスに関連付けられているデータブロックを識別する GUID を指します。

**パラメーター** . Wmi. BufferSize は、非ページバッファーのサイズを示し**ます。**

**パラメーター。 WMI**は、インスタンスを識別し、新しいデータ値を指定する、 [**WNODE\_1 つの\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)構造をポイントします。

## <a name="output-parameters"></a>出力パラメーター


なし。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーが、wmi[**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出すことによって irp を処理する場合、WMI は、i/o 状態ブロック内の**irp&gt;Iostatus. Status**と**Irp&gt;iostatus. 情報**を設定します。

それ以外の場合、ドライバーは**Irp&gt;iostatus. status**を STATUS\_SUCCESS に、または次のような適切なエラー状態に設定します。

ステータス\_WMI\_インスタンス\_見つかりませ\_んでした

ステータス\_WMI\_GUID\_見つかりませんでした\_

ステータス\_WMI\_読み取り\_のみ

ステータス\_WMI\_設定\_エラー

成功すると、ドライバーは**Irp&gt;IoStatus. 情報**をゼロに設定します。

<a name="operation"></a>操作
---------

ドライバーが、このルーチンを呼び出して WMI Irp を処理する[**場合、このルーチンは、ドライバー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)[*の設定*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_datablock_callback)を呼び出します。または、ドライバーがルーチンを定義していない場合にのみ、ステータス\_WMI\_読み取り\_を返します。

ドライバーが**IRP\_** を [**処理し、1つの\_インスタンスの要求自体\_変更\_場合は、パラメーターのデバイスオブジェクトポインターが、ドライバーによって渡されたポインターと一致します。IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)。 それ以外の場合、ドライバーは、要求を次の下位のドライバーに転送する必要があります。

ドライバーが要求を処理する場合、ドライバーでサポートされているデータブロックを識別するかどうかを判断するために、まず**データパス**の GUID を確認する必要があります。 それ以外の場合は、ドライバーが IRP を失敗させ、ステータスを返す必要があります。 WMI\_GUID\_見つかりませ\_ん\_ます。

ドライバーがデータブロックをサポートしている場合は、**次のよう**にして、受信した wnode\_インスタンス名の[**単一\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)構造を確認する必要があります。

-   WNODE\_フラグ\_静的\_インスタンス\_名前が**Wnodeheader. Flags**に設定されている場合、ドライバーは、そのブロックのドライバーの静的インスタンス名の一覧へのインデックスとして**instanceindex**を使用します。 WMI は、ブロックの登録時にドライバーによって提供された登録データからインデックスを取得します。

-   WNODE\_フラグ\_静的\_インスタンス\_名前が**Wnodeheader. Flags**で明確である場合、ドライバーは**OffsetInstanceName**のオフセットを使用して、入力 wnode\_SINGLE のインスタンス名の文字列を検索し[ **\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)。 **OffsetInstanceName**は、構造体の先頭から、インスタンス名の文字列の USHORT サイズの長さまでのバイト単位のオフセットです (文字数ではなく、終端の null が存在する場合)。その後に、Unicode のインスタンス名の文字列が続きます。

ドライバーは、すべての入力値の検証を担当します。 具体的には、ドライバーが IRP 要求自体を処理する場合は、次の操作を行う必要があります。

-   静的な名前の場合は、Wnode の**Instanceindex**メンバーが、データブロックのドライバーによってサポートされているインスタンスインデックスの範囲内にあることを確認します。この場合、 [ **\_インスタンス構造\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)ます。

-   動的名の場合は、ドライバーでサポートされているデータブロックインスタンスがインスタンス名の文字列によって識別されていることを確認します。

-   データ項目間に埋め込まれている埋め込みを含む有効なサイズのデータブロックが記述されていることを**確認します**。これは、 **1 つの WNODE\_単一\_インスタンス**構造体の**メンバーである**ことを確認します。バッファーはデータブロックに対して有効です。

-   指定されたデータブロックが、ドライバーが呼び出し元によって開始された変更を許可するものであることを確認してください。 つまり、ドライバーは、読み取り専用であることを意図したデータブロックを変更できないようにする必要があります。

スレッドコンテキストが、開始側のユーザーモードアプリケーションのコンテキストであることを前提としていません。これは、上位レベルのドライバーによって変更されている可能性があります。

ドライバーは、指定されたインスタンスを見つけることができない場合、IRP を失敗させ、ステータス\_WMI\_インスタンス\_見つから\_ないことを確認します。 インスタンスに動的なインスタンス名が含まれている場合、この状態はドライバーがインスタンスをサポートしていないことを示します。 そのため、他のプロバイダーがインスタンスを検出しても、他の何らかの理由で要求を処理できない場合、WMI は他のデータプロバイダーのクエリを続行し、適切なエラーをデータコンシューマーに返すことができます。

ドライバーがインスタンスを見つけ、要求を処理できる場合は、インスタンス内の書き込み可能なデータ項目を[**Wnode\_single\_instance**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)構造体の値に設定して、読み取り専用の項目を変更せずに残します。 データブロック全体が読み取り専用の場合、ドライバーは IRP を失敗させ、ステータス\_WMI\_読み取り\_のみを返します。

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
<td>Wdm (Wdm .h、Ntddk、または Ntifs を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[*このようにしてください。* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_datablock_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**WMB\_のコンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**Wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE\_単一\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)

 

 




