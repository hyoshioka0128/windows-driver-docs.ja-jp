---
title: IRP_MN_EXECUTE_METHOD
description: データブロック内のメソッドをサポートするすべてのドライバーは、この IRP を処理する必要があります。
ms.date: 08/12/2017
ms.assetid: cc42340e-4a7c-475c-b44d-2127e8a0d7dc
keywords:
- IRP_MN_EXECUTE_METHOD カーネルモードドライバーのアーキテクチャ
ms.localizationpriority: medium
ms.openlocfilehash: 16ce2bb0b176eedfbcb35f1980320d0ae72d8758
ms.sourcegitcommit: 7681ac46c42782602bd3449d61f7ed4870ef3ba7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922571"
---
# <a name="irp_mn_execute_method"></a>IRP\_を\_実行\_するメソッド


データブロック内のメソッドをサポートするすべてのドライバーは、この IRP を処理する必要があります。 ドライバーは、wmi Irp を処理できます。詳細につい[**ては、**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバーがの呼び出しを**\_\_\_実行**するために、wmi[**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出すことによって、IRP を実行するメソッド[*の要求*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_execute_method_callback)を処理します。

<a name="major-code"></a>主要コード
----------

[**IRP\_MJ\_システム\_コントロール**](irp-mj-system-control.md)

<a name="when-sent"></a>送信時
---------

WMI は、データブロックに関連付けられたメソッドを実行するために、この IRP を送信します。

WMI は、任意のスレッドコンテキストで\_この IRP を IRQL = パッシブレベルで送信します。

WMI は、irp を通した**\_\_EXECUTE\_メソッド**を送信する前に、irp [**\_の全\_クエリ\_の単一\_インスタンス**](irp-mn-query-single-instance.md)を送信します。 ドライバーが**irp\_を使用し\_た\_EXECUTE メソッド**をサポートしている場合は、メソッドが実行されているのと同じデータブロックに対して、 **\_irp\_が\_1 つ\_のインスタンス**ハンドラーを持つ必要があります。

## <a name="input-parameters"></a>入力パラメーター


**Parameters. WMI. ProviderId**は、要求に応答する必要があるドライバーのデバイスオブジェクトを指します。 このポインターは、IRP 内のドライバーの i/o スタックの場所にあります。

**データパス**は、実行するメソッドに関連付けられたデータブロックを識別する GUID を指します。

**パラメーター** 。 wmi. BufferSize は、非ページバッファーのサイズを指定**します。このバッファー**は&gt; =  **sizeof**(**wnode\_\_メソッド項目**) に、メソッドの出力データのサイズを加えたものである必要があります。

**MethodID**は、 [**wnode\_メソッド\_の項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)構造を指し**ます。** この構造体は、実行するメソッドの識別子を示し、データ型は、構造体の先頭から入力データの最初のバイトまでのオフセット (バイト単位) を示します。 **DataBlockOffset** **パラメーター&gt;** は、入力データを含む入力**wnode\_メソッド\_の項目**のサイズをバイト単位で示します。入力がない場合は0を示します。

## <a name="output-parameters"></a>出力パラメーター


ドライバーが、の WMI Irp を処理する場合には、wmi は、 [**wmi に**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) [*DpWmiExecuteMethod*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_execute_method_callback) [**\_\_**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)よって返されるデータを指定します。

それ以外の場合、ドライバーは**Wnode\_メソッド\_の項目**構造を入力します。これは、次のように**なります。**

-   出力データを含む**Wnode\_メソッド\_** の出力項目のサイズを使用して、 **wnodeheader. BufferSize**を更新します。

-   出力データのサイズを使用して**Sizedata lock**を更新します。出力データがない場合は0になります。

-   **パラメーター**をチェックして、出力データを含む**wnode\_メソッド\_** の出力データを受け取るのに十分な大きさのバッファーであるかどうかを確認します。 バッファーのサイズが十分でない場合、ドライバーは、**パラメーター**によって示されている小さ[**\_すぎる\_**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_too_small)構造体に必要なサイズを入力します。 バッファーが**sizeof**(**wnode\_が\_小さすぎる**) より小さい場合、ドライバーは IRP に失敗し、ステータス\_バッファー\_が\_小さすぎます。

-   データがある場合は、データを入力**データに書き込みます。** ドライバーでは、の入力値を変更すること**はできません。**

## <a name="io-status-block"></a>I/O ステータス ブロック


ドライバーが、wmi[**コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)を呼び出すことによって irp を処理する場合、WMI は、i/o 状態ブロック内の**irp-&gt;Iostatus. status**と**irp-&gt;iostatus. 情報**を設定します。

それ以外の場合は、ドライバーによって、 **Irp-&gt;Iostatus. STATUS**が正常状態\_に設定されるか、次のような適切なエラー状態に設定されます。

ステータス\_バッファー\_が\_小さすぎます

状態\_WMI\_GUID\_が\_見つかりません

状態\_WMI\_インスタンス\_が\_見つかりません

状態\_WMI\_ITEMID\_が\_見つかりません

成功した場合、ドライバーは、 **Irp-&gt;iostatus**を設定します。これは、**パラメーター**によってバッファーに書き込まれたバイト数になります。

<a name="operation"></a>Operation
---------

ドライバーは、wmi Irp を処理できます。詳細につい[**ては、**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 「 [Wmi 要求の処理](https://docs.microsoft.com/windows-hardware/drivers/kernel/handling-wmi-requests)」を参照してください。

ドライバーが、このルーチンを呼び出して WMI Irp を処理する[**場合、その**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)ルーチンは、[*ドライバーの状態*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_execute_method_callback)を呼び出します。または\_、\_ドライバーがルーチンを定義していない場合は、"無効なデバイス\_要求" ステータスを返します。

ドライバーが**IRP\_\_\_** によって実行されるメソッドの要求自体を処理する場合は、パラメーターが指定されている場合にのみ、ドライバーが[**iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)に渡すポインターと同じデバイスオブジェクトを指すようにする必要があります **。** それ以外の場合、ドライバーは、要求を次の下位のドライバーに転送する必要があります。

ドライバーは、すべての入力値の検証を担当します。 具体的には、ドライバーが IRP 要求自体を処理する場合は、次の操作を行う必要があります。

-   静的な名前の場合は、 [**Wnode\_メソッド\_の項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)構造の**instanceindex**メンバーが、データブロックのドライバーでサポートされているインスタンスインデックスの範囲内であることを確認します。

-   動的名の場合は、ドライバーでサポートされているデータブロックインスタンスがインスタンス名の文字列によって識別されていることを確認します。

-   [**Wnode\_\_メソッドの項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)構造体の**MethodId**メンバーが、データブロックのドライバーでサポートされているメソッド識別子の範囲内であること、および呼び出し元がメソッドを実行できることを確認します。

-   [**Wnode\_メソッド\_の項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)構造のデータオブジェクトと**sizedatablock**メンバーと**sizelock**メンバーが、指定されたメソッドのパラメーターを格納するのに十分な大きさのバッファーを記述していること、およびパラメーターがメソッドに対して有効であることを確認します。

-   パラメーターが、出力データで更新された後に**Wnode\_\_メソッドの項目**構造を受け取るのに十分な大きさのバッファーを指定し**ます**。

スレッドコンテキストが、開始側のユーザーモードアプリケーションのコンテキストであることを前提としていません。これは、上位レベルのドライバーによって変更されている可能性があります。

ドライバーは、要求を処理する前に、**データパス**がドライバーでサポートされている GUID を指しているかどうかを判断する必要があります。 一致していない場合は、ドライバーが IRP を\_失敗\_さ\_せ\_、ステータス WMI GUID が見つからないことを返します。

ドライバーがデータブロックをサポートしている場合は、次のように、インスタンス**名の入力** [**wnode\_メソッド\_の項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)を確認します。

-   \_Wnode\_フラグの静的\_インスタンス\_名が**wnodeheader. Flags**に設定されている場合、ドライバーは、そのブロックの静的インスタンス名のドライバーリストへのインデックスとして**instanceindex**を使用します。 WMI は、ブロックの登録時にドライバーによって提供された登録データからインデックスを取得します。

-   \_\_\_\_ **Wnodeheader. Flags**で wnode フラグの静的インスタンス名がクリアされている場合、ドライバーは**OffsetInstanceName**のオフセットを使用して、input **wnode\_メソッド\_項目**内のインスタンス名の文字列を検索します。 **OffsetInstanceName**は、構造体の先頭からのオフセット (バイト単位) から USHORT までのオフセットです。これは、(文字ではなく) インスタンス名の文字列の長さ (バイト単位) です (存在する場合は終端の null を含み、その後に Unicode のインスタンス名の文字列が続きます)。

指定されたインスタンスがドライバーで見つからない場合は、IRP が失敗し\_、\_WMI\_インスタンス\_が見つからないことを返す必要があります。 動的なインスタンス名を持つインスタンスの場合、この状態はドライバーがインスタンスをサポートしていないことを示します。 そのため、他のプロバイダーがインスタンスを検出しても、他の何らかの理由で要求を処理できない場合、WMI は他のデータプロバイダーのクエリを続行し、適切なエラーをデータコンシューマーに返すことができます。

次に、入力**Wnode\_メソッド\_項目**のメソッド ID を調べて、そのデータブロックに対して有効なメソッドであるかどうかを判断します。 それ以外の場合、ドライバーは IRP を失敗さ\_せ\_、\_ステータス\_WMI ITEMID が見つからないことを返します。

メソッドによって出力が生成される場合、ドライバーは、副作用がある可能性がある操作または2回実行してはならない操作を実行する前に、**パラメーター**の出力バッファーのサイズを確認する必要があります。 たとえば、メソッドがカウンターのグループの値を返し、カウンターをリセットした場合、ドライバーはカウンターをリセットする前に、バッファーサイズを確認し (バッファーが小さすぎる場合は IRP を失敗させる) 必要があります。 これにより、WMI はより大きなバッファーで要求を安全に再送信できます。

インスタンスとメソッド ID が有効で、バッファーのサイズが十分である場合、ドライバーはメソッドを実行します。 入力**Wnode\_メソッド\_項目**の**sizedatablock**が0以外の場合、ドライバーは、メソッドの入力**とし**てデータを使用します。

メソッドによって出力が生成された場合、ドライバーは、出力データをデータバッファーに格納します。これは、データを**格納します。また、** 出力**wnode\_\_メソッドの項目**には、出力データのバイト数を設定します。 **SizeDataBlock** メソッドに出力データが含まれていない場合、ドライバーは**sizesets lock**を0に設定します。 ドライバーでは、の入力値を変更すること**はできません。**

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


[*このようにしてください。*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_execute_method_callback)

[**IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)

[**WMB\_コンテキスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmilib_context)

[**Wmi コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)

[**WNODE\_メソッド\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)

 

 




