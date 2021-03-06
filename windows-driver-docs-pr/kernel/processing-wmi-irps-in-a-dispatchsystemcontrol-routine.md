---
title: DispatchSystemControl ルーチンでの WMI IRP の処理
description: DispatchSystemControl ルーチンでの WMI IRP の処理
ms.assetid: 9f1fc209-ee32-4270-87e5-e360ca5eca17
keywords:
- WMI の WDK カーネルでは、要求
- WDK の WMI の要求
- Irp WDK WMI
- DispatchSystemControl ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 94e6c988e4ea5272eeb8f5df88948309cc0cb03a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378794"
---
# <a name="processing-wmi-irps-in-a-dispatchsystemcontrol-routine"></a>DispatchSystemControl ルーチンでの WMI IRP の処理





WMI Irp を処理するドライバー、 [ *DispatchSystemControl* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)ルーチン処理など、IRP 場合にのみデバイス オブジェクトのポインターにする必要があります**Parameters.WMI.ProviderId**呼び出しで、ドライバーによって渡されたポインターと一致する[ **IoWMIRegistrationControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iowmiregistrationcontrol)します。 それ以外の場合、ドライバーは、[次へ] の下位のドライバーに IRP を転送する必要があります。

ドライバーは、要求を処理する場合が必要です。

GUID を確認してください**Parameters.WMI.DataPath** 、ドライバーでサポートされるデータ ブロックを表すかどうかを把握し、ない場合は、失敗のステータスの IRP\_WMI\_GUID\_いない\_。見つかりました。

ドライバーは、入力をチェックする必要があります**れた WNODE\_* XXX*** で構造体**Parameters.WMI.Buffer**もその次の要求を処理するときにインスタンス名。

[**IRP\_MN\_クエリ\_単一\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)
[**IRP\_MN\_変更\_1 つ\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-instance)
[**IRP\_MN\_変更\_単一\_項目**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-item) 
 [ **IRP\_MN\_EXECUTE\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)ドライバーが次のようにインスタンス名を確認する必要があります。

- 場合れた WNODE\_フラグ\_静的\_インスタンス\_で名前が設定されて**WnodeHeader.Flags**を使用して、 **InstanceIndex**のドライバーの一覧へのインデックスとしてそのブロックの静的インスタンス名です。

- 場合れた WNODE\_フラグ\_静的\_インスタンス\_名が明確では**WnodeHeader.Flags**を使用して、 **OffsetInstanceName**インスタンスへのオフセットとして名前を入力に文字列**れた WNODE\_* XXX*** 構造体。 **OffsetInstanceName**文字列自体の後に存在する場合の NUL 終端文字を含むバイト (しない文字) でインスタンス名の文字列の長さを示す USHORT に構造体の先頭からのバイト オフセット内Unicode。

ドライバーがで指定されたインスタンスを見つけられない場合**InstanceIndex**または**OffsetInstanceName**、ステータスの IRP が失敗する必要があります\_WMI\_インスタンス\_されません\_が見つかりました。

[ **IRP\_MN\_EXECUTE\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)要求チェック**メソッド Id**入力に[ **れた WNODE\_メソッド\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_method_item)メソッドがデータ ブロックに対して有効でない場合に状態 IRP が失敗して、\_WMI\_ITEMID\_いない\_が見つかりました。

ドライバーが、バッファーのサイズを確認する必要があります、要求は、出力を生成する場合**Parameters.WMI.BufferSize**もその次の要求を処理する場合。

[**IRP\_MN\_クエリ\_すべて\_データ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data)
[**IRP\_MN\_クエリ\_単一\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)
[**IRP\_MN\_EXECUTE\_メソッド**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)場合、バッファー小さすぎて、出力が表示されますが、少なくとも**sizeof**(**れた WNODE\_すぎます\_小さな**)、ドライバーは IRP を成功し、書き込みを[ **れた WNODE\_すぎます\_小さな**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_too_small)構造体にバッファーを**Parameters.WMI.Buffer**します。 バッファーがより小さい場合**sizeof**(**れた WNODE\_すぎます\_小さな**)、ドライバーが失敗状態の NTSTATUS コードで IRP\_バッファー\_が多すぎます\_小さい。

要求には、出力が生成されますバッファー サイズが十分な場合は、書き込み、次の出力バッファーを**Parameters.WMI.Buffer**:。
-   **IRP\_MN\_クエリ\_すべて\_データ**要求、ドライバーの書き込み、 [**れた WNODE\_すべて\_データ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_all_data)指定されたデータ ブロックのすべてのインスタンスのデータを含む構造体。
-   **IRP\_MN\_クエリ\_単一\_インスタンス**要求、ドライバーの書き込み、 [**れた WNODE\_単一\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_single_instance)データ ブロックの指定したインスタンスのデータを含む構造体。
-   **IRP\_MN\_EXECUTE\_メソッド**ドライバーが次の入力ドライバーにより決定された形式で出力メソッドを書き込みます、メソッドは、出力を生成する場合[ **れた WNODE\_メソッド\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-tagwnode_method_item) (存在する場合は、入力データを上書きする) バッファーにします。

設定**Irp -&gt;IoStatus.Information** 、バッファーに書き込まれたバイト数に**Parameters.WMI.Buffer**と**Irp-&gt;IoStatus.Status**ステータス\_成功します。

呼び出す[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest) IRP を完了します。

詳細については、次を参照してください。 [WMI れた WNODE\_*XXX*構造](wmi-wnode-xxx-structures.md)します。

 

 




