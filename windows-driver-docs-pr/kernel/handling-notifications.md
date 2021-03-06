---
title: 通知の処理
description: 通知の処理
ms.assetid: ace7f59d-fe9f-4810-91db-2cf20c9591cf
keywords:
- レジストリの呼び出しの WDK カーネル、通知オプションをフィルター処理
- レジストリのドライバー WDK カーネルでは、通知オプションをフィルター処理
- WDK の通知がレジストリの呼び出しをフィルター処理します。
- 呼び出しの監視、レジストリ呼び出し WDK カーネルをフィルター処理
- レジストリの呼び出しの監視、ドライバー WDK カーネルをフィルター処理
- レジストリの呼び出しの WDK カーネル、ブロックされた呼び出しをフィルター処理
- レジストリのドライバー WDK カーネルをフィルター処理、ブロックされた呼び出し数
- 呼び出しを変更するレジストリの呼び出しの WDK カーネルをフィルター処理
- フィルター ドライバー WDK カーネル、呼び出しを変更するレジストリ
- WDK のブロッキング呼び出しがレジストリの呼び出しをフィルター処理します。
- レジストリの呼び出しの監視
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e98ef23feda0dfffa68483d511bcbca3569c7de
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385622"
---
# <a name="handling-notifications"></a>通知の処理


[ *RegistryCallback* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-ex_callback_function)ルーチンへのポインターを受け取る、 **REG\_*XXX*\_キー\_情報**発生しているレジストリの操作に関する情報を含む構造体。

*RegistryCallback*ルーチンは、監視、ブロック、またはレジストリの操作を変更します。

### <a name="monitoring-registry-calls"></a>レジストリの呼び出しの監視

ドライバーがレジストリの操作を監視して、レジストリのフィルター処理する場合、 *RegistryCallback*カウンターを更新またはその他のブックキーピング操作を実行して状態を返すことができますルーチン\_成功します。 たびに、 *RegistryCallback*ルーチンがステータスを返します\_レジストリ操作の実行は引き続き成功すると、configuration manager。

Windows XP および Windows の以降のバージョンでは、レジストリ呼び出しの監視がサポートされています。

### <a name="blocking-registry-calls"></a>レジストリの呼び出しをブロック

場合、ドライバーをフィルタ リング レジストリはレジストリの操作をブロックできますその*RegistryCallback*ルーチンは、対象の状態値を返します[NT\_成功](using-ntstatus-values.md)(*状態*) に等しい**FALSE** (つまり、非成功 NTSTATUS 値)。 構成マネージャー受け取る成功以外の戻り値と、ステータスのドライバーが指定した値を持つ呼び出し元のスレッドをすぐに返します。 そのため、レジストリのフィルター ドライバーは処理されないレジストリの操作を防ぐために事前通知を使用できます。

場合、 *RegistryCallback*ルーチンでは、どの NT のステータス値を返します\_成功 (*状態*) と等しい**FALSE**事前通知の場合、操作の後の通知のコールバックは発生しません。

レジストリの呼び出しをブロックすると、Windows XP および Windows の以降のバージョンでサポートされます。 Windows Vista 以降、ドライバーは、レジストリ操作が呼び出し元のスレッドに返す値を変更できます。 これらの値に含まれる、 **REG\_*XXX*\_キー\_情報**Windows Vista 以降の構造体。

### <a name="modifying-registry-calls"></a>レジストリの呼び出しを変更します。

ドライバーをフィルタ リング レジストリが戻り値またはレジストリ操作の出力パラメーターを変更できます。 さらに、ドライバーは、操作を処理するためにレジストリではなくレジストリ操作を完全に処理できます。

フィルター ドライバーのレジストリと*RegistryCallback*ルーチンは、後の通知を受信、そのことができます。

-   出力パラメーターを変更するその**REG\_*XXX*\_キー\_情報**構造が含まれています、状態を返します\_成功します。 Configuration manager では、呼び出し元のスレッドに変更後の出力パラメーターを返します。

    Windows Vista 以降、出力パラメーターの変更はサポートされています。

-   ステータスの値を提供することで、レジストリの操作の戻り値を変更、 **ReturnStatus**のメンバー、 [ **REG\_POST\_操作\_情報** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_reg_post_operation_information)構造と、状態を返す\_コールバック\_バイパスします。 Configuration manager では、呼び出し元のスレッドを指定の戻り値を返します。

    **注**構成マネージャーが割り当てられているオブジェクトの割り当てを解除する必要があるドライバーには、障害成功から状態コードが変更された場合、。 または、ドライバーには、成功を障害からのステータス コードが変更された、適切な出力パラメーターを指定することがあります。




Windows Vista 以降、戻り値の変更はサポートされています。


フィルター ドライバーのレジストリと*RegistryCallback*ルーチンが事前通知を受け取る、ルーチンは、レジストリ操作自体を処理し、状態を返します\_コールバック\_バイパスします。 レジストリがステータスを受信すると\_コールバック\_バイパスの状態を返すだけ、ドライバーから\_呼び出し元のスレッドに成功し、操作を処理しません。 ドライバーで有効な出力値を返す必要があり、ドライバーのレジストリの操作に横取りされし、完全に処理され、する必要があります、 **REG\_*XXX*\_キー\_情報**構造体。

ドライバーは、Windows Vista 以降のレジストリの操作を切断できます。

場合、 *RegistryCallback*ルーチンがステータスを返します\_コールバック\_事前通知の場合、操作の後の通知のコールバックは発生しませんをバイパスします。

**注**のため、使用頻度と、レジストリのいくつかの集まりの結果を実現するためには、通常は、使用している場合、いくつかのレジストリのシステム呼び出しが記載されていません。 エラーが発生しやすいは難しくは、これらの呼び出しによって実行される操作を変更します。 ドライバー開発者向けでは、次のレジストリのシステム呼び出しを変更しようとしています。 推奨されません。
-   **NtRestoreKey**
-   **NtSaveKey**
-   **NtSaveKeyEx**
-   **NtLoadKeyEx**
-   **NtUnloadKey2**
-   **NtUnloadKeyEx**
-   **NtReplaceKey**
-   **NtRenameKey**
-   **NtSetInformationKey**










