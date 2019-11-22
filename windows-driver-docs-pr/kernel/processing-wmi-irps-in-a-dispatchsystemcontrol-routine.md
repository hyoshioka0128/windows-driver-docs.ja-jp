---
title: DispatchSystemControl ルーチンでの WMI IRP の処理
description: DispatchSystemControl ルーチンでの WMI IRP の処理
ms.assetid: 9f1fc209-ee32-4270-87e5-e360ca5eca17
keywords:
- WMI WDK カーネル、要求
- WDK WMI を要求する
- Irp WDK WMI
- DispatchSystemControl ルーチン
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f4aa0d0d368a36a5a52c265406c82b2493c410d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72827586"
---
# <a name="processing-wmi-irps-in-a-dispatchsystemcontrol-routine"></a>DispatchSystemControl ルーチンでの WMI IRP の処理





[*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)ルーチンで wmi irp を処理するドライバーは、**パラメーター**にあるデバイスオブジェクトポインターが、 [**iowmiregistrationcontrol**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiregistrationcontrol)の呼び出しでドライバーによって渡されたポインターと一致する場合にのみ、このような irp を処理する必要があります。 それ以外の場合、ドライバーは IRP を次の下位のドライバーに転送する必要があります。

ドライバーが要求を処理する場合、次のことを行う必要があります。

**データパス**の guid を調べて、ドライバーがサポートしているデータブロックを表しているかどうかを判断します。そうでない場合は、WMI\_GUID\_見つから\_ないことを示す\_状態で IRP を失敗させます。

ドライバーは、次のいずれかの要求を処理するときに、インスタンス**名の入力** **wnode\_* XXX*** 構造を確認する必要があります。

[**Irp\_\_クエリ\_単一\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)
[**IRP\_\_変更\_1\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-instance)
[**irp\_\_変更\_1 つ\_ITEM**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-change-single-item)
[**IRP\_、\_メソッドを実行\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method) 、次のように、ドライバーがインスタンス名を確認する必要があります。

- WNODE\_フラグ\_静的\_インスタンス\_名前が**Wnodeheader. Flags**に設定されている場合は、そのブロックの静的インスタンス名のドライバーリストへのインデックスとして**instanceindex**を使用します。

- WNODE\_フラグ\_静的\_インスタンス\_名前が**Wnodeheader. Flags**で明確である場合、入力**WNODE\_* XXX*** 構造のインスタンス名の文字列へのオフセットとして**OffsetInstanceName**を使用します。 **OffsetInstanceName**は、構造体の先頭から、インスタンス名の文字列の長さ (文字ではない) を示す USHORT までのオフセット (バイト単位) (存在する場合は NUL 終端文字、Unicode の場合は文字列自体)。

**Instanceindex**または**OffsetInstanceName**によって指定されたインスタンスがドライバーで見つからない場合は、状態\_WMI\_インスタンス\_見つかり\_ませんでした。

[ **\_メソッド要求を実行\_\_irp**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)の場合は、入力[**WNODE\_メソッドの\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)で**MethodID**を確認し、そのデータブロックに対してメソッドが有効でない場合は、状態\_WMI で IRP を失敗させ\_ITEMID\_\_見つかりませんでした。

要求で出力が生成される場合、ドライバーは、次のいずれかの要求を処理するときに、**パラメーター**でバッファーのサイズを確認する必要があります。

[**Irp\_\_クエリ\_すべての\_データ**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-all-data)
[**irp\_完了\_クエリ\_単一\_インスタンス**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-single-instance)
[**irp\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-execute-method)完了\_バッファーが小さすぎて出力を受信することはありませんが、少なくとも**sizeof**(**wnode\_** \_小さ) の場合、ドライバーは irp を正常に実行し、 [**wnode\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_too_small)を書き込みます **。パラメーター。 WMI. Buffer**.\_\_ バッファーが**sizeof**(**wnode\_が小さすぎる\_** ) より小さい場合、ドライバーは、\_バッファー\_\_小さすぎる状態の NTSTATUS コードを使用して IRP を失敗させることになります。

要求によって出力が生成され、バッファーサイズが適切である場合は、次の出力を**パラメーター**でバッファーに書き込みます。
-   すべての **\_データ要求を\_する IRP\_\_クエリ**の場合、ドライバーは、指定されたデータブロックのすべてのインスタンスのデータを含む[**すべての\_データ構造を\_の wnode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_all_data)を書き込みます。
-   **IRP\_\_クエリ\_単一\_インスタンス**要求の場合、ドライバーは、データブロックの指定されたインスタンスのデータを含む[**WNODE\_1 つのインスタンス**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_single_instance)構造に書き込みます。\_
-   IRP\_、メソッドが出力を生成する場合に **\_メソッドを実行\_** には、ドライバーが指定した形式で、バッファーの入力[**wnode\_メソッド\_項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-tagwnode_method_item)の後にメソッドの出力を書き込みます (を上書きします。入力データ (存在する場合)。

**Irp-&gt;iostatus. 情報**を、**パラメーター**に設定されているバッファーに書き込むバイト数に設定します。また、 **Irp&gt;iostatus. status**から status\_SUCCESS に設定されます。

[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)を呼び出して、IRP を完了します。

詳細については、「 [WMI WNODE\_*XXX*構造体](wmi-wnode-xxx-structures.md)」を参照してください。

 

 




