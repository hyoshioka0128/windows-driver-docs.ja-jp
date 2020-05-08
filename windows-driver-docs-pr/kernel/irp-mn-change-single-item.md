---
title: IRP_MN_CHANGE_SINGLE_ITEM
description: WMI をサポートするすべてのドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: 9839ebb2-31a9-4cb0-adbf-1882583849fc
keywords:
- IRP_MN_CHANGE_SINGLE_ITEM カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: da52243f8566825b2f695f638eff3d0cd34c3a31
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922507"
---
# <a name="irp_mn_change_single_item"></a>IRP\_の\_全\_変更\_の1つの項目


WMI をサポートするすべてのドライバーは、この IRP を処理する必要があります。 ドライバーは、wmi Irp を処理できます。詳細につい[**ては、**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバーが WMI[**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出して、IRP **\_によって\_変更\_さ\_れた1つの項目**の要求を処理する場合、WMI はそのドライバーの \n 呼び出し[*setdataitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_dataitem_callback)ルーチンを呼び出します。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)

<a name="when-sent"></a>送信時
---------

WMI は、データブロックの1つのインスタンス内の単一のデータ項目を変更するために、この IRP を送信します。

WMI は、任意のスレッドコンテキストで\_この IRP を IRQL = パッシブレベルで送信します。

## <a name="input-parameters"></a>入力パラメーター


**Parameters. WMI. ProviderId**は、要求に応答する必要があるドライバーのデバイスオブジェクトを指します。 このポインターは、IRP 内のドライバーの i/o スタックの場所にあります。

**データパス**は、設定するデータブロックを識別する GUID を指します。

**パラメーター** . Wmi. BufferSize は、非ページバッファーのサイズを示し**ます。**

**パラメーター。 WMI**は、データブロックのインスタンス、設定する項目の ID、および新しいデータ値を識別する[**\_\_wnode 単一項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)構造体を指します。

## <a name="output-parameters"></a>出力パラメーター


ありません。

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーが、wmi[**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出すことによって irp を処理する場合、WMI は、i/o 状態ブロック内の**irp-&gt;Iostatus. status**と**irp-&gt;iostatus. 情報**を設定します。

それ以外の場合は、ドライバーによって、 **Irp-&gt;Iostatus. STATUS**が正常状態\_に設定されるか、次のような適切なエラー状態に設定されます。

状態\_WMI\_インスタンス\_が\_見つかりません

状態\_WMI\_ITEMID\_が\_見つかりません

状態\_WMI\_GUID\_が\_見つかりません

ステータス\_WMI\_読み取り\_専用

ステータス\_WMI\_の\_設定エラー

成功した場合、ドライバーは**Irp&gt;-Iostatus. 情報**をゼロに設定します。

<a name="operation"></a>Operation
---------

ドライバーが WMI Irp を処理するとき[**に、この**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)[*ルーチンは*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_dataitem_callback)、このルーチンを呼び出して、そのルーチンを呼び出します。また\_、\_ドライバー\_がルーチンを定義していない場合は、状態 WMI 読み取りのみを返します。

ドライバーが**IRP\_によって\_変更\_さ\_れた1つの項目**だけを処理する場合は、パラメーターを指定した場合にのみ、ドライバーが[**iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)に渡すポインターと同じデバイスオブジェクトを指すようにする必要があり**ます。** それ以外の場合、ドライバーは、要求を次の下位のドライバーに転送する必要があります。

システムによって提供されるユーザーモードコンポーネントがこの機能を必要としていることが確実でない限り、 **IRP\_\_が\_変化する単一\_の項目**のサポートを実装しないでください。

要求を処理する前に、ドライバーは、**データパス**がドライバーでサポートされている GUID を指しているかどうかを判断する必要があります。 そうでない場合は、ドライバーが IRP を失敗させ、\_ステータス\_WMI\_GUID\_が見つからないことを返します。

ドライバーがデータブロックをサポートしている場合は、次のように、パラメーターによって入力[**Wnode\_single\_ITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)構造を確認する必要があり**ます。**

-   \_Wnode\_フラグの静的\_インスタンス\_名が**wnodeheader. Flags**に設定されている場合、ドライバーは、そのブロックの静的インスタンス名のドライバーリストへのインデックスとして**instanceindex**を使用します。 WMI は、ブロックの登録時にドライバーによって提供された登録データからインデックスを取得します。

-   \_\_\_\_ **Wnodeheader. Flags**で wnode フラグの静的インスタンス名がクリアされている場合、ドライバーは**OffsetInstanceName**のオフセットを使用して、入力[**wnode\_SINGLE\_ITEM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)構造体内のインスタンス名の文字列を検索します。 **OffsetInstanceName**は、構造体の先頭からのバイト単位のオフセットであり、インスタンス名の文字列の USHORT サイズの長さをバイト単位で指定します (文字数ではありません)。 この長さには NULL 終端文字が含まれ、その後に Unicode でインスタンス名文字列が続きます。

ドライバーは、すべての入力値の検証を担当します。 具体的には、ドライバーが IRP 要求自体を処理する場合は、次の操作を行う必要があります。

-   静的名の場合は、WNODE\_SINGLE\_ITEM 構造体の**instanceindex**メンバーが、データブロックのドライバーでサポートされているインスタンスインデックスの範囲内にあることを確認します。

-   動的名の場合は、ドライバーでサポートされているデータブロックインスタンスがインスタンス名の文字列によって識別されていることを確認します。

-   [**Wnode\_\_単一項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)構造の**ItemId**メンバーが、データブロックのドライバーでサポートされている項目識別子の範囲内にあることを確認します。

-   **Wnode\_SINGLE\_ITEM**構造体のデータマイニング**オフセット**および**sizedataitem**メンバーで、有効なサイズのデータブロックが記述されていること、およびバッファーの内容がデータ項目に対して有効であることを確認します。

-   指定されたデータ項目が、ドライバーが呼び出し元によって開始された変更を許可しているものであることを確認します。 つまり、ドライバーでは、読み取り専用として意図したデータ項目を変更できないようにする必要があります。

スレッドコンテキストが、開始側のユーザーモードアプリケーションのコンテキストであることを前提としていません。これは、上位レベルのドライバーによって変更されている可能性があります。

指定されたインスタンスがドライバーで見つからない場合は、IRP が失敗し\_、\_WMI\_インスタンス\_が見つからないことを返す必要があります。 動的なインスタンス名を持つインスタンスの場合、この状態はドライバーがインスタンスをサポートしていないことを示します。 そのため、他のプロバイダーがインスタンスを検出しても、他の何らかの理由で要求を処理できない場合、WMI は他のデータプロバイダーのクエリを続行し、適切なエラーをデータコンシューマーに返すことができます。

ドライバーがインスタンスを検索し、要求を処理できる場合、インスタンスのデータ項目は[**Wnode\_single\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)の値に設定されます。 データ項目が読み取り専用の場合、ドライバーは項目を変更せずに残し、IRP を失敗させ\_、\_ステータス\_WMI 読み取り専用を返します。

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


[*\N この Setdataitem*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_set_dataitem_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**WMB\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**Wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE\_SINGLE\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_item)

 

 




