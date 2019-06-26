---
title: INF InboxVersionRequired ディレクティブ
description: INF InboxVersionRequired ディレクティブ
ms.assetid: 75a07ca7-d279-4815-b644-10b58753f885
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc6c21a886d3d7f4c7a1e0c037bde1278ed7c9b5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372377"
---
# <a name="inf-inboxversionrequired-directive"></a>INF InboxVersionRequired ディレクティブ


パッケージに対応したドライバーは、使用することができます、 **InboxVersionRequired** INF ディレクティブをドライバーの INF を参照するすべてのコアの最小許容バージョンを指定します。 使用することができます、 **UseDriverVer**最小バージョンを指定するキーワード。 この最小バージョンは、INF で参照されているコアのドライバーをすべてに適用されます。

次の例に注意してくださいドライバー パッケージ セクションに挿入する方法を示しています、 **InboxVersionRequired** INF ディレクティブ。

```cpp
[PrinterPackageInstallation.amd64]
PackageAware=TRUE
CoreDriverDependencies={D20EA372-DD35-4950-9ED8-A6335AFE79F0},{D20EA372-DD35-4950-9ED8-A6335AFE79F3}
InboxVersionRequired=UseDriverVer
```

場合、 **UseDriverVer**キーワードがの値として使用される**InboxVersionRequired**、 **UseDriverVer**クラスのインストーラーを使用することを通知、 **DriverVer**の中核となるドライバーの許容される最小バージョンとして解析される INF のディレクティブのバージョン文字列。 ドライバーを使用する際に注意が必要ですの注意を払う必要がありますが、 **UseDriverVer**キーワード。 INF によって参照されているすべてのコア ドライバーは正常にインストールの同じまたはそれ以降のバージョンである必要があります。

値として特定のバージョン文字列を指定することもできます。 **InboxVersionRequired**します。 これらのバージョン文字列と同じ書式に従う、 **DriverVer**文字列で指定されている、 [ **INF バージョン セクション**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-version-section)します。 詳細については、 **DriverVer**形式の文字列を参照してください[ **INF DriverVer ディレクティブ**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-driverver-directive)します。

次の例を設定する方法を示しています。 **InboxVersionRequired**を特定のバージョン文字列。

```cpp
InboxVersionRequired=09/28/1999,5.00.2136.1
```

 

 




