---
title: IRP_MN_CHANGE_SINGLE_ITEM
description: WMI をサポートするすべてのドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 9839ebb2-31a9-4cb0-adbf-1882583849fc
keywords:
- IRP_MN_CHANGE_SINGLE_ITEM カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: b441da63c6f388f8541c7f77249c05dfb485df1a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838591"
---
# <a name="irp_mn_change_single_item"></a>IRP\_\_1 つの\_項目\_変更


WMI をサポートするすべてのドライバーは、この IRP を処理する必要があります。 ドライバーは、wmi Irp を処理できます。詳細につい[**ては、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバーが、 **1 つの\_項目の要求\_\_変更**された IRP\_を処理するように呼び出した場合は、WMI によってそのドライバーの \N 呼び出し[*setdataitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_dataitem_callback)ルーチン[**が呼び出され**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)ます。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)送信時
---------

WMI は、データブロックの1つのインスタンス内の単一のデータ項目を変更するために、この IRP を送信します。

WMI は、任意のスレッドコンテキストで、IRQL = パッシブ\_レベルでこの IRP を送信します。

## <a name="input-parameters"></a>入力パラメーター


**Parameters. WMI. ProviderId**は、要求に応答する必要があるドライバーのデバイスオブジェクトを指します。 このポインターは、IRP 内のドライバーの i/o スタックの場所にあります。

**データパス**は、設定するデータブロックを識別する GUID を指します。

**パラメーター** . Wmi. BufferSize は、非ページバッファーのサイズを示し**ます。**

**パラメーター**は、wnode\_、データブロックのインスタンス、設定する項目の ID、および新しいデータ値を識別する[**1 つの\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)構造体を指します。

## <a name="output-parameters"></a>出力パラメーター


なし。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーが、wmi[**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出すことによって irp を処理する場合、WMI は、i/o 状態ブロック内の**irp&gt;Iostatus. Status**と**Irp&gt;iostatus. 情報**を設定します。

それ以外の場合、ドライバーは**Irp&gt;iostatus. status**を STATUS\_SUCCESS に、または次のような適切なエラー状態に設定します。

ステータス\_WMI\_インスタンス\_見つかりませ\_んでした

ステータス\_WMI\_ITEMID\_見つかりませ\_んでした

ステータス\_WMI\_GUID\_見つかりませんでした\_

ステータス\_WMI\_読み取り\_のみ

ステータス\_WMI\_設定\_エラー

成功した場合、ドライバーは**Irp&gt;IoStatus. 情報**をゼロに設定します。

<a name="operation"></a>操作
---------

ドライバー[**が、この**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)ルーチンを呼び出して wmi irp を処理する場合、そのルーチンは、[*ドライバーの設定*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_dataitem_callback)を呼び出します。または、ドライバーがルーチンを定義していない場合にのみ、ステータス\_WMI\_読み取り\_を返します。

ドライバーが IRP\_を処理し、 **1 つの\_項目の要求自体\_変更\_** 場合は、パラメーターを指定した場合にのみ、ドライバーが渡さ [**れたポインターと同じデバイスオブジェクトを指すようにする必要があります。IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)。 それ以外の場合、ドライバーは、要求を次の下位のドライバーに転送する必要があります。

システムによって提供されるユーザーモードコンポーネントがこの機能を必要としていることが確実である場合を除き、 **1 つの\_項目\_\_の IRP\_** のサポートを実装しないでください。

要求を処理する前に、ドライバーは、**データパス**がドライバーでサポートされている GUID を指しているかどうかを判断する必要があります。 そうでない場合は、ドライバーが IRP を失敗させてステータスを返す必要があります\_WMI\_GUID\_見つかりませ\_んでした。

ドライバーがデータブロックをサポートしている場合は、次のように、入力[**Wnode\_単一の\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)構造を確認する必要があり**ます。** この場合、パラメーターはインスタンス名を指します。

-   WNODE\_フラグ\_静的\_インスタンス\_名前が**Wnodeheader. Flags**に設定されている場合、ドライバーは、そのブロックのドライバーの静的インスタンス名の一覧へのインデックスとして**instanceindex**を使用します。 WMI は、ブロックの登録時にドライバーによって提供された登録データからインデックスを取得します。

-   WNODE\_フラグ\_静的\_インスタンス\_名前が**Wnodeheader. Flags**で明確である場合、ドライバーは**OffsetInstanceName**のオフセットを使用して、入力 wnode\_SINGLE のインスタンス名の文字列を検索し[ **\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)の構造。 **OffsetInstanceName**は、構造体の先頭からのバイト単位のオフセットであり、インスタンス名の文字列の USHORT サイズの長さをバイト単位で指定します (文字数ではありません)。 この長さには NULL 終端文字が含まれ、その後に Unicode でインスタンス名文字列が続きます。

ドライバーは、すべての入力値の検証を担当します。 具体的には、ドライバーが IRP 要求自体を処理する場合は、次の操作を行う必要があります。

-   静的な名前の場合は、WNODE\_SINGLE\_ITEM 構造体の**Instanceindex**メンバーが、データブロックのドライバーでサポートされているインスタンスインデックスの範囲内であることを確認します。

-   動的名の場合は、ドライバーでサポートされているデータブロックインスタンスがインスタンス名の文字列によって識別されていることを確認します。

-   [**Wnode\_SINGLE\_item**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)構造体の**ItemId**メンバーが、データブロックのドライバーでサポートされている項目識別子の範囲内であることを確認します。

-   **Wnode\_SINGLE\_ITEM**構造体**に、有効**なサイズのデータブロックが記述されていること、およびバッファーの内容がデータ項目に対して有効であることを**確認します**。

-   指定されたデータ項目が、ドライバーが呼び出し元によって開始された変更を許可しているものであることを確認します。 つまり、ドライバーでは、読み取り専用として意図したデータ項目を変更できないようにする必要があります。

スレッドコンテキストが、開始側のユーザーモードアプリケーションのコンテキストであることを前提としていません。これは、上位レベルのドライバーによって変更されている可能性があります。

ドライバーは、指定されたインスタンスを見つけることができない場合、IRP を失敗させ、ステータス\_WMI\_インスタンス\_見つから\_ないことを確認します。 動的なインスタンス名を持つインスタンスの場合、この状態はドライバーがインスタンスをサポートしていないことを示します。 そのため、他のプロバイダーがインスタンスを検出しても、他の何らかの理由で要求を処理できない場合、WMI は他のデータプロバイダーのクエリを続行し、適切なエラーをデータコンシューマーに返すことができます。

ドライバーがインスタンスを見つけて要求を処理できる場合、インスタンスのデータ項目は[**Wnode\_single\_item**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)の値に設定されます。 データ項目が読み取り専用の場合、ドライバーは項目を変更せずに残し、IRP を失敗させ、ステータス\_WMI\_読み取り\_のみを返します。

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


[ *\N この Setdataitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_dataitem_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**WMB\_のコンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**Wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE\_SINGLE\_ITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)

 

 




