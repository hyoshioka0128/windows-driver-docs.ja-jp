---
title: 通知の処理
description: 通知の処理
ms.assetid: ace7f59d-fe9f-4810-91db-2cf20c9591cf
keywords:
- レジストリのフィルター選択 WDK カーネル、通知オプション
- レジストリフィルタリングドライバー WDK カーネル、通知オプション
- 通知 WDK フィルタのレジストリ呼び出し
- レジストリのフィルター選択 WDK カーネル、監視の呼び出し
- レジストリフィルタリングドライバー WDK カーネル、監視通話
- レジストリのフィルター選択 WDK カーネル、ブロック呼び出し
- レジストリフィルタリングドライバー WDK カーネル、ブロック呼び出し
- レジストリのフィルター選択 WDK カーネル、呼び出しの変更
- レジストリフィルタリングドライバー WDK カーネル、呼び出しの変更
- ブロック呼び出し WDK フィルターレジストリ呼び出し
- レジストリ呼び出しの監視
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: b431cb06a25fc8841f81a4e3efc014917ec9c44c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836489"
---
# <a name="handling-notifications"></a>通知の処理


[*Registrycallback*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-ex_callback_function)ルーチンは、実行されているレジストリ操作に関する情報を含む**REG\_*XXX*\_KEY\_情報**構造体へのポインターを受け取ります。

*Registrycallback*ルーチンは、レジストリ操作の監視、ブロック、または変更を行うことができます。

### <a name="monitoring-registry-calls"></a>レジストリ呼び出しの監視

レジストリフィルタリングドライバーがレジストリ操作を監視している場合、その*Registrycallback*ルーチンは、カウンターを更新したり、他のブックの操作を実行したりして、状態\_SUCCESS を返すことができます。 *Registrycallback*ルーチンは、STATUS\_SUCCESS を返すたびに、レジストリ操作の実行を続行します。

Windows XP 以降のバージョンの Windows では、レジストリ呼び出しの監視がサポートされています。

### <a name="blocking-registry-calls"></a>ブロッキング (レジストリ呼び出しを)

レジストリフィルタリングドライバーは、 *Registrycallback*ルーチンが、 [NT\_success](using-ntstatus-values.md)(*状態*) が**FALSE** (つまり、成功しない NTSTATUS 値) と等しい状態値を返す場合に、レジストリ操作をブロックできます。 構成マネージャーは、成功しなかった戻り値を受け取ると、ドライバーが指定した状態の値を持つ呼び出し元のスレッドに直ちに戻ります。 したがって、レジストリフィルタリングドライバーは、事前通知を使用して、レジストリ操作が処理されないようにすることができます。

*Registrycallback*ルーチンが、事前通知について NT\_SUCCESS (*状態*) が**FALSE**である状態値を返す場合、操作の通知後コールバックは発生しません。

Windows XP 以降のバージョンの Windows では、レジストリの呼び出しをブロックすることがサポートされています。 Windows Vista 以降では、ドライバーは、レジストリ操作が呼び出し元のスレッドに返す値を変更できます。 これらの値は、Windows Vista 以降の**REG\_*XXX*\_キー\_情報**構造体に含まれています。

### <a name="modifying-registry-calls"></a>レジストリ呼び出しの変更

レジストリフィルタリングドライバーは、レジストリ操作の出力パラメーターまたは戻り値を変更できます。 さらに、レジストリが操作を処理できるようにする代わりに、ドライバーはレジストリ操作を完全に処理できます。

レジストリフィルタリングドライバーの*Registrycallback*ルーチンが通知を受け取ると、次のことが可能になります。

-   **REG\_*XXX*\_KEY\_INFORMATION**構造体に含まれている出力パラメーターを変更して、成功\_状態を返します。 構成マネージャーは、変更された出力パラメーターを呼び出し元のスレッドに返します。

    Windows Vista 以降では、出力パラメーターの変更がサポートされています。

-   レジストリ操作の戻り値を変更するには、 [**REG\_POST\_操作\_情報**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_reg_post_operation_information)構造体の**returnstatus**メンバーの状態値を指定し、status\_CALLBACK を返し\_通過. 構成マネージャーは、呼び出し元のスレッドに指定された戻り値を返します。

    **メモ** ドライバーがステータスコードを成功から失敗に変更した場合、configuration manager によって割り当てられたオブジェクトの割り当てを解除することが必要になる場合があります。 または、ドライバーがステータスコードを "失敗" から "成功" に変更した場合は、適切な出力パラメーターを指定しなければならないことがあります。




戻り値の変更は、Windows Vista 以降でサポートされています。


レジストリフィルタリングドライバーの*Registrycallback*ルーチンが事前通知を受け取ると、ルーチンはレジストリ操作自体を処理し、ステータス\_コールバック\_バイパスを返すことができます。 レジストリがステータス\_コールバックを受信したときに、ドライバーからの\_をバイパスした場合は、呼び出し元のスレッドの状態\_成功だけを返し、操作は処理されません。 ドライバーはレジストリ操作をプリエンプションし、完全に処理する必要があります。また、ドライバーは、 **REG\_*XXX*\_キー\_情報**構造体の有効な出力値を返すように注意する必要があります。

ドライバーは、Windows Vista 以降でレジストリ操作をプリエンプトできます。

*Registrycallback*ルーチンが、事前通知\_の状態\_コールバックを返す場合、操作の通知後コールバックは発生しません。

**メモ** いくつかのレジストリシステムコールは、あまり使用されないため、ドキュメントには記載されていません。通常、レジストリには、一般的ではない結果が得られます。 これらの呼び出しによって実行される操作の変更は困難であり、エラーが発生しやすくなります。 ドライバーの開発者は、次のレジストリシステムの呼び出しを変更しないようにすることをお勧めします。
-   **NtRestoreKey**
-   **NtSaveKey**
-   **NtSaveKeyEx**
-   **NtLoadKeyEx**
-   **NtUnloadKey2**
-   **NtUnloadKeyEx**
-   **NtReplaceKey**
-   **NtRenameKey**
-   **NtSetInformationKey**










