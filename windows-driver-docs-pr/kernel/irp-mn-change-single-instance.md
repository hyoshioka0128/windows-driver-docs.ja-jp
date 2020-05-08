---
title: IRP_MN_CHANGE_SINGLE_INSTANCE
description: WMI をサポートするすべてのドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 180d40a4-b300-4801-b9da-9239500ca15f
keywords:
- IRP_MN_CHANGE_SINGLE_INSTANCE カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 165ece0d12abd69f431bf154646435362021b654
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922565"
---
# <a name="irp_mn_change_single_instance"></a>IRP\_の\_全\_変更\_の単一インスタンス


WMI をサポートするすべてのドライバーは、この IRP を処理する必要があります。 ドライバーは、wmi Irp を処理できます。詳細につい[**ては、**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバーが WMI[**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出して、 **IRP\_\_の変化\_する単一\_インスタンス**の要求を処理する場合、WMI はその[*ドライバーの設定*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_datablock_callback)されたインスタンスを呼び出します。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)

<a name="when-sent"></a>送信時
---------

WMI は、データブロックの単一インスタンス内のすべてのデータ項目を変更するために、この IRP を送信します。

WMI は、任意のスレッドコンテキストで\_この IRP を IRQL = パッシブレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


**Parameters. WMI. ProviderId**は、要求に応答する必要があるドライバーのデバイスオブジェクトを指します。 このポインターは、IRP 内のドライバーの i/o スタックの場所にあります。

**データパス**は、変更するインスタンスに関連付けられているデータブロックを識別する GUID を指します。

**パラメーター** . Wmi. BufferSize は、非ページバッファーのサイズを示し**ます。**

**パラメーター。 WMI**は、インスタンスを識別し、新しいデータ値を指定する[**\_\_wnode 単一インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)構造をポイントします。

## <a name="output-parameters"></a>出力パラメーター


ありません。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーが、wmi[**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出すことによって irp を処理する場合、WMI は、i/o 状態ブロック内の**irp-&gt;Iostatus. status**と**irp-&gt;iostatus. 情報**を設定します。

それ以外の場合は、ドライバーによって、 **Irp-&gt;Iostatus. STATUS**が正常状態\_に設定されるか、次のような適切なエラー状態に設定されます。

状態\_WMI\_インスタンス\_が\_見つかりません

状態\_WMI\_GUID\_が\_見つかりません

ステータス\_WMI\_読み取り\_専用

ステータス\_WMI\_の\_設定エラー

成功した場合、ドライバーは**Irp&gt;-Iostatus. 情報**をゼロに設定します。

<a name="operation"></a>Operation
---------

ドライバーが WMI Irp を処理するとき[**に、この**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)ルーチンは、このルーチンを呼び出して、[*ドライバーの状態*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_datablock_callback)を呼び出します。また\_は\_、\_ドライバーがルーチンを定義していない場合にのみ、ステータス WMI を読み取ります。

ドライバーが**IRP\_\_\_\_** を完全に変更した単一インスタンスの要求を処理する場合は、**パラメーター**のデバイスオブジェクトポインターが、 [**iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)の呼び出しでドライバーによって渡されたポインターと一致する場合にのみ、この処理が行われます。 それ以外の場合、ドライバーは、要求を次の下位のドライバーに転送する必要があります。

ドライバーが要求を処理する場合、ドライバーでサポートされているデータブロックを識別するかどうかを判断するために、まず**データパス**の GUID を確認する必要があります。 一致していない場合は、ドライバーが IRP を\_失敗\_さ\_せ\_、ステータス WMI GUID が見つからないことを返します。

ドライバーでデータブロックがサポートされている場合は、次のように、受信した[**Wnode\_の\_単一インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)構造をインスタンス名の**パラメーター**で確認する必要があります。

-   \_Wnode\_フラグの静的\_インスタンス\_名が**wnodeheader. Flags**に設定されている場合、ドライバーは、そのブロックの静的インスタンス名のドライバーリストへのインデックスとして**instanceindex**を使用します。 WMI は、ブロックの登録時にドライバーによって提供された登録データからインデックスを取得します。

-   \_\_\_\_ **Wnodeheader. Flags**で wnode フラグの静的インスタンス名がクリアされている場合、ドライバーは**OffsetInstanceName**のオフセットを使用して、入力[**wnode\_SINGLE\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)内のインスタンス名の文字列を検索します。 **OffsetInstanceName**は、構造体の先頭から、インスタンス名の文字列の USHORT サイズの長さまでのバイト単位のオフセットです (文字数ではなく、終端の null が存在する場合)。その後に、Unicode のインスタンス名の文字列が続きます。

ドライバーは、すべての入力値の検証を担当します。 具体的には、ドライバーが IRP 要求自体を処理する場合は、次の操作を行う必要があります。

-   静的な名前の場合は、 [**Wnode\_の単一\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)構造の**instanceindex**メンバーが、データブロックのドライバーでサポートされているインスタンスインデックスの範囲内であることを確認します。

-   動的名の場合は、ドライバーでサポートされているデータブロックインスタンスがインスタンス名の文字列によって識別されていることを確認します。

-   **Wnode\_の単一\_インスタンス**構造のデータ**オブジェクトが、** データ項目間に存在する埋め込みを含む有効なサイズのデータブロックを**記述し、** バッファーの内容がデータブロックに対して有効であることを確認します。

-   指定されたデータブロックが、ドライバーが呼び出し元によって開始された変更を許可するものであることを確認してください。 つまり、ドライバーは、読み取り専用であることを意図したデータブロックを変更できないようにする必要があります。

スレッドコンテキストが、開始側のユーザーモードアプリケーションのコンテキストであることを前提としていません。これは、上位レベルのドライバーによって変更されている可能性があります。

指定されたインスタンスがドライバーで見つからない場合は、IRP が失敗し\_、\_WMI\_インスタンス\_が見つからないことを返す必要があります。 インスタンスに動的なインスタンス名が含まれている場合、この状態はドライバーがインスタンスをサポートしていないことを示します。 そのため、他のプロバイダーがインスタンスを検出しても、他の何らかの理由で要求を処理できない場合、WMI は他のデータプロバイダーのクエリを続行し、適切なエラーをデータコンシューマーに返すことができます。

ドライバーがインスタンスを検索し、要求を処理できる場合、インスタンス内の書き込み可能なデータ項目を[**\_wnode の単一\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)構造の値に設定し、読み取り専用の項目を変更せずに残します。 データブロック全体が読み取り専用の場合、ドライバーは IRP を失敗させ、ステータス\_WMI\_読み取り\_専用を返します。

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


[*このようにしてください。*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_datablock_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**WMB\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**Wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE\_単一\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)

 

 




