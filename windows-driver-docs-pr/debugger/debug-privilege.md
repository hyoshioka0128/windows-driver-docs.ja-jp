---
title: デバッグ特権
description: デバッグ特権には、他のユーザーへのアクセスも済む、それ以外の場合のプロセスのデバッグができます。
ms.assetid: f3ea9065-6d04-4629-88ed-85428f7915ca
keywords:
- 特権をデバッグします。
- 特権のデバッグの概要
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c2ddfbf7f2d0e75b47727a6250402de47bd5c6e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359554"
---
# <a name="debug-privilege"></a>デバッグ特権


デバッグ特権には、他のユーザーへのアクセスも済む、それ以外の場合のプロセスのデバッグができます。 たとえば、そのトークンを有効になっているデバッグ権限を持つユーザーとして実行中のプロセスでは、ローカル システムとして実行されているサービスをデバッグできます。

## <span id="ddk_reading_and_writing_registers_and_flags_dbg"></span><span id="DDK_READING_AND_WRITING_REGISTERS_AND_FLAGS_DBG"></span>


デバッグ特権は、プロセスまたはカーネル デバッガーをアタッチするユーザーを許可するセキュリティ ポリシー設定です。 管理者は、ユーザーのグループに含める、またはこの機能を削除するセキュリティ ポリシーを変更できます。 独自のアプリケーションをデバッグする開発者では、このユーザーの特権は必要ありません。 システム コンポーネントをデバッグする、またはリモート コンポーネントをデバッグする開発者は、このユーザーの特権を必要があります。 このユーザーの特権は、重要なオペレーティング システム コンポーネントへの完全なアクセスを提供します。 既定では、管理者権限を持つユーザーに対してこのプロパティを有効にします。 管理者特権を持つユーザーには、他のユーザー グループに対してこのプロパティが有効にすることができます。

### <a name="span-idmodifyingdebugprivilegeforaprocessspanspan-idmodifyingdebugprivilegeforaprocessspanmodifying-debug-privilege-for-a-process"></a><span id="modifying_debug_privilege_for_a_process"></span><span id="MODIFYING_DEBUG_PRIVILEGE_FOR_A_PROCESS"></span>プロセスのデバッグ特権を変更します。

次のコード例では、プロセスのデバッグ特権を有効にする方法を示します。 これにより、他のプロセスへのアクセスをそれ以外の場合必要はありませんをデバッグすることができます。

```cpp
//
//  SetPrivilege enables/disables process token privilege.
//
BOOL SetPrivilege(HANDLE hToken, LPCTSTR lpszPrivilege, BOOL bEnablePrivilege)
{
    LUID luid;
    BOOL bRet=FALSE;

    if (LookupPrivilegeValue(NULL, lpszPrivilege, &luid))
    {
        TOKEN_PRIVILEGE tp;

        tp.PrivilegeCount=1;
        tp.Privileges[0].Luid=luid;
        tp.Privileges[0].Attributes=(bEnablePrivilege) ? SE_PRIVILEGE_ENABLED: 0;
        //
        //  Enable the privilege or disable all privileges.
        //
        if (AdjustTokenPrivileges(hToken, FALSE, &tp, NULL, (PTOKEN_PRIVILEGES)NULL, (PDWORD)NULL))
        {
            //
            //  Check to see if you have proper access.
            //  You may get "ERROR_NOT_ALL_ASSIGNED".
            //
            bRet=(GetLastError() == ERROR_SUCCESS);
        }
    }
    return bRet;
}
```

次の例では、この関数を使用する方法を示します。

```cpp
HANDLE hProcess=GetCurrentProcess();
HANDLE hToken;

if (OpenProcessToken(hProcess, TOKEN_ADJUST_PRIVILEGES, &hToken))
{
    SetPrivilege(hToken, SE_DEBUG_NAME, TRUE);
    CloseHandle(hToken);
}
```

 

 





