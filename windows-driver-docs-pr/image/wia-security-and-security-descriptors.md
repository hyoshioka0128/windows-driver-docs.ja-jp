---
title: WIA セキュリティおよびセキュリティ記述子
description: WIA セキュリティおよびセキュリティ記述子
ms.assetid: 2919f3fc-1eb5-4801-a589-ae3000320763
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 010e7f0231a43ba1249a4a4fc829b858c76e219a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548984"
---
# <a name="wia-security-and-security-descriptors"></a>WIA セキュリティおよびセキュリティ記述子





表示されている問題の解決策の多くは[WIA セキュリティ上の一般的な問題](common-wia-security-problems.md)など、適切なエンティティへのアクセスを付与するセキュリティ記述子を対象となるオブジェクトを必要と**LocalService**アカウント。

一般に、 **LocalService**アカウントが持つ Acl によるアクセスを許可するリソースへのアクセス、 **LocalService**アカウント、Everyone、またはユーザーを認証します。 サービスはユーザーまたはグループのユーザー オブジェクトへのアクセスを許可する随意アクセス制御 list(DACL) を作成しない限り、他のアプリケーションとオブジェクト (パイプ、ファイルのマッピング、同期、およびなど) を共有することはできません。

次のコード例は、セキュリティ記述子を設定する方法を示しています。 アプリケーションとドライバーは、名前付きイベント オブジェクトを共有する必要がある場合、この方法を使用できます。

```cpp
//
//  Security descriptor in SDDL form:
//  D:           - Indicates what follows is a 
//                 Discretionary Access Control List (DACL)
//  (A;;GA;;;LS) - Grants generic all access to LocalService
//  (A;;GA;;;BA) - Grants generic all access to Built-in Admins
//  (A;;GA;;;IU) - Grants generic all access to Interactive User 
//
#define MY_EVENT_DACL TEXT("D:(A;;GA;;;LS)(A;;GA;;;BA)(A;;GA;;;IU)")

//
//  Allocate appropriate security attributes for the named event
//  to be shared between driver and app running under 
//  interactive user's account.
//
SECURITY_ATTRIBUTES sa = { sizeof(sa), FALSE, NULL };
if(ConvertStringSecurityDescriptorToSecurityDescriptor(
              MY_EVENT_DACL,
              SDDL_REVISION_1, 
              &(sa.lpSecurityDescriptor), NULL))
{
  h_MyEvent = CreateEvent(&sa,           // Our security descriptor 
                                         //  allowing access to 
                                         //  Admins, LocalService
                                         //  and the Interactive
                                         //  User
                          bManualReset,
                          bInitialState, 
                          tszName);
  if (h_MyEvent != NULL)
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
else
{
  // Failed.  Do error cleanup...
  .
  .
  .
}
```

レジストリ キーは、INF ファイルで、適切な Acl を作成することもします。 たとえば、管理者とで実行されているドライバーのみにアクセスできるソフトウェア キーにレジストリ キーを作成する**LocalService**、INF ファイルに次のエントリを追加します。

```INF
[DDInstallSection]
Addreg=MyAddReg

[DDInstallSection.MyAddReg]
HKLM,"SOFTWARE\MyCompany\MySpecialKey\"

[DDInstallSection.MyAddReg.Security]
"D:(A;CIOI;GA;;;BA)(A;CIOI;GA;;;LS)"
```

INF ファイルの詳細については、次を参照してください。 [WIA デバイスの INF ファイル](inf-files-for-wia-devices.md)します。

詳細については、Windows セキュリティ モデルは Windows セキュリティのドキュメントを参照してください。 ドライバーの作成者は、破壊的なユーザーが、ドライバーの脆弱性を悪用の可能性を低減する一般的なセキュリティのベスト プラクティスの対応もあります。 "*Writing Secure Code*"(ISBN 0-7356-1588-8) マイクロソフト プレスがいくつかの有用なリソースの利用可能です。

 

 




