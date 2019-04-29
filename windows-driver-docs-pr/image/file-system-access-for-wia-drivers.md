---
title: WIA ドライバーのファイル システム アクセス
description: WIA ドライバーのファイル システム アクセス
ms.assetid: 7bdd116e-d58f-4c2e-a5ec-c9a8196cfd62
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa59a3155f22784ff36607c8c5715ca041e50bd2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63323442"
---
# <a name="file-system-access-for-wia-drivers"></a>WIA ドライバーのファイル システム アクセス





ドライバー ファイルの転送中に、WIA サービスによって提供されるもの以外のファイルを使用する場合、ドライバーはこれらのファイルが配置されると、アクセスする方法について注意が必要である必要があります。 具体的には、ドライバー開発者は、ディレクトリとファイルを使用して、これらのアクセス許可の必要があります。 例をいくつかのドライバーが読み取りまたは書き込み、独自のファイル、ログ記録、調整が必要があり、構成を保存します。

たとえば、%*windir*%\\*System32*ディレクトリは読み取り専用に、 **LocalService**アカウント通常 WIA ドライバーは開くことができませんファイルの読み取りまたは書き込みアクセスがあります。 ほとんどのディレクトリは読み取り専用に**LocalService**アカウント、ため、問題があるほとんどのドライバーをファイルから読み取る場合にのみ必要がある場合。 ただし、ドライバーの作成や制限付きのディレクトリにファイルを作成するときに、ファイルの問題が発生する操作を行います。

ドライバーのみを使用するファイルの書き込みに安全な場所では、ユーザーのプロファイル ディレクトリにします。 ユーザーがこの場合、ドライバーをホストするプロセスが実行されているアカウントを指すことに注意してください。 は、Windows XP では、これは、 **LocalSystem**アカウント、および Microsoft Windows Server 2003 以降では、これは、 **LocalService**アカウント。 WIA をサポートしている Windows のすべてのバージョンで問題なく動作するためのドライバーで、ドライバーが、プライベート ファイルを作成する必要があります、 **%** <em>userprofile</em> **%** ディレクトリ。

次のコード例は、WIA ドライバーが、% を使用する方法を示しています。*userprofile*% ディレクトリ。

```cpp
#define MY_DRIVER_FILE_NAME_W L"%userprofile%\\MyDriverFile.ext";
HANDLE hMyDriverFile         = INVALID_HANDLE_VALUE;
WCHAR  wszFileName[MAX_PATH] = {L'\0'};
DWORD  dwMaxChars            = sizeof(wszExpandedName) /                     
                               sizeof(wszExpandedName[0]);
if (ExpandEnvironmentStringsW(MY_DRIVER_FILE_NAME_W, 
                              wszFileName,
                              dwMaxChars))
{
    //
    // The %userprofile% environment variable is expanded, if
    // there was an error and the variable is not found.
    // In this case an error would be returned before creating the 
    // file. If the file is created blindly with the name 
    // L"%userprofile\\MyDriverFile.ext"
    // a possibility exists that the file will be created in a 
    // different directory, e.g. the root.
    //
    hMyDriverFile = 
            CreateFileW(
            wszFileName,           // Contains file name and path
            dwDesiredAccess,       // E.g. GENERIC_WRITE
            dwShareMode,           // E.g. FILE_SHARE_WRITE
            lpSecurityAttributes,  // Don't forget to ACL your file            
                                   //   appropriately!
            dwCreationDisposition, // E.g. CREATE_ALWAYS
            dwFlagsAndAttributes,  // E.g. FILE_ATTRIBUTE_NORMAL
            NULL);                 // Template file
    if (hMyDriverFile != INVALID_HANDLE_VALUE)
    {
        //  Success!
    }
    else
    {
        // Failed.  Do error cleanup...
        .
        .
        .
    }
}
```

ドライバーは、以外のディレクトリに含まれるファイルに書き込む必要がある場合**%** <em>userprofile</em>ファイル/ディレクトリの適切なアクセス許可が設定されていること確認 %、します。 一般に適切なアクセス許可が与えられていることを意味、 **LocalService**アカウント。 WIA サービスの実行では、Windows XP、 **LocalSystem**アカウントでは、ローカル管理者グループに属しているし、アクセス レベルが大幅に増加します。

### <a name="wia-application-and-wia-driver-common-files"></a>WIA アプリケーションおよび WIA ドライバーの一般的なファイル

ドライバーと、バンドルされているアプリケーションの両方必要がある読み取り/書き込みアクセスを一般的なファイルに場合、Application Data ディレクトリのサブディレクトリに、すべてのユーザー プロファイル内のファイルが配置されるが推奨されます (CSIDL\_共通\_APPDATA)。 新しいサブディレクトリを適切な Acl を設定することを確認します。

 

 




