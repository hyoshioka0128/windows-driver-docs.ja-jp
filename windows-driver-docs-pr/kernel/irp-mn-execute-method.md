---
title: IRP_MN_EXECUTE_METHOD
description: データブロック内のメソッドをサポートするすべてのドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: cc42340e-4a7c-475c-b44d-2127e8a0d7dc
keywords:
- IRP_MN_EXECUTE_METHOD カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 16258bc05ecd45e5292c40c2c4d4ce2cfcff5057
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828057"
---
# <a name="irp_mn_execute_method"></a>IRP\_\_メソッドを実行\_


データブロック内のメソッドをサポートするすべてのドライバーは、この IRP を処理する必要があります。 ドライバーは、wmi Irp を処理できます。詳細につい[**ては、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバーが、 **\_メソッド要求を実行\_IRP\_** を[**処理するよう**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)に呼び出した場合、WMI はその[*ドライバーの設定*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_execute_method_callback)された設定を呼び出します。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)送信時
---------

WMI は、データブロックに関連付けられたメソッドを実行するために、この IRP を送信します。

WMI は、任意のスレッドコンテキストで、IRQL = パッシブ\_レベルでこの IRP を送信します。

WMI は、irp\_を送信する前に[ **\_1 つの\_インスタンスに、irp\_\_クエリ**](irp-mn-query-single-instance.md)を送信して **\_メソッドを実行**します。\_ ドライバーで Irp\_がサポートされていて **\_メソッドを実行\_** 場合、メソッドが実行されているのと同じデータブロックに対して、 **1 つの\_インスタンス**ハンドラーを使用する必要\_があります。\_\_

## <a name="input-parameters"></a>入力パラメーター


**Parameters. WMI. ProviderId**は、要求に応答する必要があるドライバーのデバイスオブジェクトを指します。 このポインターは、IRP 内のドライバーの i/o スタックの場所にあります。

**データパス**は、実行するメソッドに関連付けられたデータブロックを識別する GUID を指します。

**パラメーター** 。 Wmi. BufferSize は、非ページバッファーのサイズを示します。このバッファーは、= **sizeof**(**WNODE\_METHOD\_ITEM**) と、の出力データのサイズを &gt;する必要があり**ます**。b.

MethodID は[**Wnode\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)を指します **。** この\_メソッドは、が実行するメソッドの識別子を示し、データ型は、構造体の先頭から入力データの最初のバイトまでのオフセット (バイト単位)**を示します**。 **&gt;パラメーター**を指定すると、入力データを含む **\_メソッド\_項目の入力 wnode**のサイズをバイト数で示します。入力がない場合は0を示します。

## <a name="output-parameters"></a>出力パラメーター


ドライバーが、の WMI Irp を処理するときには、wmi によって WMI Irp が処理される[**場合、wmi**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)は、 [**WNODE\_メソッド\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)を入力します。 [](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_execute_method_callback)

それ以外の場合、ドライバーは**Wnode\_メソッド\_項目**構造体に入力**します。** これにより、パラメーターは次のようになります。

-   出力データを含む**Wnodeheader. BufferSize**を出力**WNODE\_メソッド\_ITEM**のサイズで更新します。

-   出力データのサイズを使用して**Sizedata lock**を更新します。出力データがない場合は0になります。

-   **パラメーター**をチェックして、出力データを含む出力**WNODE\_メソッド\_項目**を受け取るのに十分な大きさのバッファーであるかどうかを確認します。 バッファーのサイズが十分ではない場合、ドライバーは Wnode に必要なサイズを入力するだけでなく、**パラメーター**によって示される[**小さな構造\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_too_small)ます。 バッファーが**sizeof**(**wnode\_が\_小さい**) より小さい場合、ドライバーは IRP に失敗し、ステータス\_バッファー\_\_小さすぎることを返します。

-   データがある場合は、データを入力**データに書き込みます。** ドライバーでは、の入力値を変更すること**はできません。**

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーが、wmi[**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出すことによって irp を処理する場合、WMI は、i/o 状態ブロック内の**irp&gt;Iostatus. Status**と**Irp&gt;iostatus. 情報**を設定します。

それ以外の場合、ドライバーは**Irp&gt;iostatus. status**を STATUS\_SUCCESS に、または次のような適切なエラー状態に設定します。

状態\_バッファー\_\_小さすぎます

ステータス\_WMI\_GUID\_見つかりませんでした\_

ステータス\_WMI\_インスタンス\_見つかりませ\_んでした

ステータス\_WMI\_ITEMID\_見つかりませ\_んでした

成功した場合、ドライバーは**Irp&gt;IoStatus**を設定します。これは、**パラメーター**によってバッファーに書き込まれたバイト数になります。

<a name="operation"></a>操作
---------

ドライバーは、wmi Irp を処理できます。詳細につい[**ては、** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバー[**が、この**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)ルーチンを呼び出して WMI irp を処理する場合、このルーチンは、[*ドライバーの設定*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_execute_method_callback)を呼び出します。または、ドライバーがルーチンを定義していない場合、デバイス\_要求\_無効\_状態を返します。

ドライバーが**IRP\_** を処理し、\_メソッドの要求自体を実行\_場合は、パラメーターが指定されている場合にのみ、ドライバーが[**Iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)に渡すポインターと同じデバイスオブジェクトを指すようにする必要があります **。** それ以外の場合、ドライバーは、要求を次の下位のドライバーに転送する必要があります。

ドライバーは、すべての入力値の検証を担当します。 具体的には、ドライバーが IRP 要求自体を処理する場合は、次の操作を行う必要があります。

-   静的名の場合は、 [**Wnode\_メソッド\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)構造体の**instanceindex**メンバーが、データブロックのドライバーでサポートされているインスタンスインデックスの範囲内であることを確認します。

-   動的名の場合は、ドライバーでサポートされているデータブロックインスタンスがインスタンス名の文字列によって識別されていることを確認します。

-   [**Wnode\_メソッド\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)構造体の**MethodId**メンバーが、データブロックのドライバーでサポートされているメソッド識別子の範囲内であること、および呼び出し元がメソッドを実行できることを確認します。

-   [**Wnode\_メソッドの\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)構造体のデータマイニング**オフセット**および**sizeのロック**メンバーが、指定されたメソッドのパラメーターを格納するのに十分な大きさのバッファーを記述していること、およびパラメーターが有効であることを確認します。メソッドの。

-   **パラメーター**を確認します。これは、出力データで更新された後、 **WNODE\_メソッド\_項目**構造を受け取るのに十分な大きさのバッファーを指定します。

スレッドコンテキストが、開始側のユーザーモードアプリケーションのコンテキストであることを前提としていません。これは、上位レベルのドライバーによって変更されている可能性があります。

ドライバーは、要求を処理する前に、**データパス**がドライバーでサポートされている GUID を指しているかどうかを判断する必要があります。 それ以外の場合は、ドライバーが IRP を失敗させ、ステータスを返す必要があります。 WMI\_GUID\_見つかりませ\_ん\_ます。

ドライバーがデータブロックをサポートしている場合は、次に示すように、インスタンス**名の入力** [**WNODE\_メソッド\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)がチェックされます。

-   WNODE\_フラグ\_静的\_インスタンス\_名前が**Wnodeheader. Flags**に設定されている場合、ドライバーは、そのブロックのドライバーの静的インスタンス名の一覧へのインデックスとして**instanceindex**を使用します。 WMI は、ブロックの登録時にドライバーによって提供された登録データからインデックスを取得します。

-   WNODE\_フラグ\_静的\_インスタンス\_名前が**Wnodeheader. Flags**で明確になっている場合、ドライバーは**OffsetInstanceName**のオフセットを使用して、入力**wnode\_メソッド内のインスタンス名の文字列を検索し\_項目**。 **OffsetInstanceName**は、構造体の先頭からのオフセット (バイト単位) から USHORT までのオフセットです。これは、(文字ではなく) インスタンス名の文字列の長さ (バイト単位) です (存在する場合は終端の null を含み、その後に Unicode のインスタンス名の文字列が続きます)。

ドライバーは、指定されたインスタンスを見つけることができない場合、IRP を失敗させ、ステータス\_WMI\_インスタンス\_見つから\_ないことを確認します。 動的なインスタンス名を持つインスタンスの場合、この状態はドライバーがインスタンスをサポートしていないことを示します。 そのため、他のプロバイダーがインスタンスを検出しても、他の何らかの理由で要求を処理できない場合、WMI は他のデータプロバイダーのクエリを続行し、適切なエラーをデータコンシューマーに返すことができます。

次に、入力**Wnode\_メソッド\_項目**のメソッド ID を調べて、そのデータブロックに対して有効なメソッドであるかどうかを判断します。 それ以外の場合、ドライバーは IRP に失敗し、ステータス\_WMI\_ITEMID\_返され\_見つかりません。

メソッドによって出力が生成される場合、ドライバーは、副作用がある可能性がある操作または2回実行してはならない操作を実行する前に、**パラメーター**の出力バッファーのサイズを確認する必要があります。 たとえば、メソッドがカウンターのグループの値を返し、カウンターをリセットした場合、ドライバーはカウンターをリセットする前に、バッファーサイズを確認し (バッファーが小さすぎる場合は IRP を失敗させる) 必要があります。 これにより、WMI はより大きなバッファーで要求を安全に再送信できます。

インスタンスとメソッド ID が有効で、バッファーのサイズが十分である場合、ドライバーはメソッドを実行します。 入力**Wnode\_メソッド\_項目**が0以外の場合に**sizeの lock**が使用されている場合、ドライバーは、メソッドの**入力とし**て、データを使用します。

メソッドによって出力が生成された場合、ドライバーは、出力データを、データを格納するバッファーにデータを書き込みます。また、出力**Wnode\_メソッド\_ITEM** **に出力**データのバイト数を**設定します**。 メソッドに出力データが含まれていない場合、ドライバーは**sizesets lock**を0に設定します。 ドライバーでは、の入力値を変更すること**はできません。**

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


[*このようにしてください。* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_execute_method_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**WMB\_のコンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**Wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE\_メソッド\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)

 

 




