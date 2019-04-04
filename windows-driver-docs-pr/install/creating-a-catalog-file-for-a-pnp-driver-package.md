---
title: PnP ドライバー パッケージ用のカタログ ファイルの作成
description: PnP ドライバー パッケージ用のカタログ ファイルの作成
ms.assetid: 2af431f1-a35d-4312-86f6-a928ef4148df
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 958bd97952c05b5cff884f34c476603dde0b563e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557673"
---
# <a name="creating-a-catalog-file-for-a-pnp-driver-package"></a>PnP ドライバー パッケージ用のカタログ ファイルの作成


ドライバー パッケージを符号なしのカタログ ファイルを作成するには、次の手順を実行します。

1. 追加の必要な INF **CatalogFile**=<em>FileName</em>**します。Cat**エントリまたは INF **CatalogFile** 。<em>PlatformExtension</em>=<em>一意のファイル名</em>**します。Cat**エントリを[ **INF バージョン セクション**](inf-version-section.md)の[ドライバー パッケージの](driver-packages.md)INF ファイル。 プラットフォームの拡張機能を使用する方法については、[クロスプラット フォーム対応の INF ファイル](cross-platform-inf-files.md)を参照してください。

2. 使用して、 [ **Inf2Cat** ](https://msdn.microsoft.com/library/windows/hardware/ff547089)ツールをターゲット プラットフォームのドライバー パッケージを署名できることを確認し、符号なしの生成を[カタログ ファイル](catalog-files.md)(*.cat*ファイル) のターゲット プラットフォームに適用されています。

符号なしのカタログ ファイルを作成するのにには、次の Inf2Cat コマンドを使用します。

```cpp
Inf2Cat /driver:DriverPath /os:WindowsVersionList
```

各項目の意味は次のとおりです。

- **/Driver:**<em>DriverPath</em>パラメーターにより、ディレクトリの名前を[ドライバー パッケージ](driver-packages.md)が配置されています。

- **/Os:**<em>WindowsVersionList</em>パラメーターがドライバー パッケージが Windows の一覧で指定されている Windows バージョンの署名の要件に準拠していることを確認する Inf2Cat を構成しますバージョン識別子。

### <a name="examples"></a>例

次の例は、トースターに適用[ドライバー パッケージ](driver-packages.md)にある*c:\\WindDDK\\5739\\src\\全般\\トースター\\toastpkg\\toastcd*します。 トースター パッケージの INF ファイルは*Toastpkg.inf*この INF ファイルには、次が含まれている**CatalogFile**ディレクティブをプラットフォーム拡張機能。

```cpp
[Version]
. . .
CatalogFile.NTx86  = tostx86.cat
CatalogFile.NTIA64 = tostia64.cat
CatalogFile.NTAMD64 = tstamd64.cat
. . .
```

生成する*Tostx86.cat*特定 x86 の場合、Windows のバージョンの Windows バージョンを指定する*WindowsVersionList*します。 次の Inf2Cat コマンドことを確認するなど、[ドライバー パッケージ](driver-packages.md)Windows 2000 と x86 署名できるは Windows Vista、Windows Server 2003、および Windows XP のバージョン。

```cpp
Inf2Cat /driver:c:\WindDDK\5739\src\general\toaster\toastpkg\toastcd /os:2000,XP_X86,Server2003_X86,Vista_X86
```

生成する*Tostamd64.cat* x64 の場合、Windows のバージョンの Windows バージョンを指定する*WindowsVersionList*します。 次の Inf2Cat コマンドは、x64 用のドライバー パッケージを署名することができますを確認など、Windows Vista、Windows Server 2003、および Windows XP のバージョン。

```cpp
Inf2Cat /driver:c:\WindDDK\5739\src\general\toaster\toastpkg\toastcd /os:XP_X64,Server2003_X64,Vista_X64
```

生成する*Tostamd64.cat* Windows Vista x64 Edition 用のみで"Vista_X64"のみを指定*WindowsVersionList します。* たとえば、次の Inf2Cat コマンドのみことを確認します、[ドライバー パッケージ](driver-packages.md)Windows Vista x64 Edition 用に署名することができます。

```cpp
Inf2Cat /driver:c:\WindDDK\5739\src\general\toaster\toastpkg\toastcd /os:Vista_X64
```

 

 





