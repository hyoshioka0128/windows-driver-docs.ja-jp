---
title: インストールされているディスプレイ ドライバー ディレクティブ
description: インストールされているディスプレイ ドライバーのディレクティブは、ドライバー パッケージの一部としてインストールされている UMD の適切な名前を指定するソフトウェア デバイス設定です。
ms.assetid: 7104129C-57B1-4F37-B1E0-D86529C9866E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd4ae1908eb4589ebd56cf19beb949e994fadcbe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536355"
---
# <a name="installed-display-drivers-directive"></a>インストールされているディスプレイ ドライバー ディレクティブ


インストールされているディスプレイ ドライバーのディレクティブは、ドライバー パッケージの一部としてインストールされている UMD の適切な名前を指定するソフトウェア デバイス設定です。

``` syntax
HKR,, InstalledDisplayDrivers,              %REG_MULTI_SZ%, 
UserModeDriverName1, UserModeDriverName2, UserModeDriverNameWow1, UserModeDriverNameWow2
```

次に、例を示します。

``` syntax
For example:
X86:
HKR,, InstalledDisplayDrivers,              %REG_MULTI_SZ%, r200umd

X64:
HKR,, InstalledDisplayDrivers,              %REG_MULTI_SZ%, r200umd, r200umdva, r200umd64, r200umd64va
```

 

 





